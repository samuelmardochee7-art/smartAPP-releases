# Sécurité de SmartPresence

Ce document décrit ce que l'application protège, contre qui, comment, et ce qui reste de la
responsabilité de l'établissement. Chaque protection est vérifiée par un test automatisé
(`tests/test_securite.py` et les autres fichiers de tests).

## 1. Ce que l'on protège, et contre qui

| Bien | Menace | Exemple |
|---|---|---|
| Présences | Fraude par un étudiant | Carte prêtée à un camarade, carte réutilisée, carte perdue puis retrouvée |
| Présences | Complaisance ou erreur d'un membre du personnel | Valider un absent, modifier une présence après coup |
| Données personnelles (identités, photos, absences) | Vol ou perte | PC volé, disque récupéré, clé USB de sauvegarde égarée |
| Comptes | Usurpation | Mot de passe deviné, poste laissé ouvert |
| Traces | Effacement | Suppression des rejets ou des corrections dans le journal |
| Poste de travail | Fichiers piégés | Photo ou import Excel malveillant, archive de restauration piégée |

## 2. Fraude au pointage

| Mesure | Détail |
|---|---|
| Vérification visuelle obligatoire | Aucune présence sans décision explicite du surveillant (Entrée). Échap ou la croix de la fenêtre n'enregistrent rien. |
| Garde-fous du clavier | Entrée est ignorée pendant 400 ms. Une saisie au clavier dans les 600 ms précédentes (lecteur USB qui envoie une autre carte) neutralise l'Entrée suivante. |
| Contrôles automatiques | Double scan, carte remplacée, carte inconnue et photo manquante sont bloquants. Seul l'enseignant du cours peut forcer la validation d'un étudiant hors cours. |
| Carte non falsifiable | Le QR code contient un jeton aléatoire de 50 bits, vérifié en base et comparé en temps constant. Une nouvelle carte invalide immédiatement l'ancienne. |
| QR codes étrangers | Un contenu de plus de 64 caractères, ou dont le matricule n'a pas le format d'un vrai matricule, est refusé avant toute requête : il n'atteint ni la base ni le journal. Le champ du lecteur USB accepte 128 caractères au plus. |
| Traçabilité | Rejets, forçages, cartes remplacées présentées et corrections manuelles (motif obligatoire, ancienne valeur, auteur) sont tous journalisés. |

## 3. Chiffrement des données au repos

| Élément | Protection |
|---|---|
| Base de données | **SQLCipher 4** (AES-256, HMAC par page) : le fichier est illisible sans la clé, y compris son journal WAL. `secure_delete` écrase les données supprimées. |
| Photos, justificatifs | **AES-256-GCM**. Le nom du fichier est authentifié : un fichier échangé, renommé ou altéré ne se déchiffre plus, et aucune photo trompeuse ne peut être substituée. |
| Sauvegardes | Elles ne contiennent que des données déjà chiffrées, avec l'empreinte publique de la clé. Une archive volée est inexploitable. |
| Clé maîtresse | 256 bits aléatoires. Sur disque, elle est protégée par **Windows DPAPI** (compte utilisateur courant) : seul ce compte Windows, sur ce PC, peut la déverrouiller. Des sous-clés distinctes sont dérivées par HKDF-SHA256 (base, fichiers, journal). |
| Code de récupération | C'est la clé elle-même, en 14 groupes de 4 caractères, avec une somme de contrôle qui détecte les fautes de frappe. Il est remis une seule fois à l'administrateur, qui doit confirmer l'avoir mis en lieu sûr. Il est ensuite consultable uniquement après ré-authentification, et chaque consultation est journalisée. |
| Copies temporaires | Une pièce jointe ouverte dans le lecteur de Windows est déchiffrée dans un dossier temporaire au nom aléatoire, qu'un autre programme ne peut ni deviner ni préparer à l'avance. Il est vidé à la fermeture et au lancement suivant. |
| Dialogues fermés | Les fenêtres de saisie de mot de passe, du mot de passe provisoire et du code de récupération sont détruites dès leur fermeture, et leur champ est vidé : ces secrets ne restent pas dans une fenêtre cachée pendant toute la session. |
| Presse-papiers | Le code de récupération copié est exclu de l'historique du presse-papiers de Windows (Win+V) et de sa synchronisation dans le nuage, puis effacé au bout de 2 minutes. |
| Anciens étudiants | Au-delà d'une durée de conservation réglable (5 ans par défaut), les étudiants désactivés peuvent être anonymisés : nom, prénoms, date de naissance, photo et pièces justificatives effacés, ancienne carte refusée. Les présences restent dans les statistiques. Le journal et l'historique des corrections, scellés, gardent le matricule d'origine : c'est une pseudonymisation, pas un effacement total. |
| Aide au visage (F17) | La comparaison est faite sur le poste, avec des modèles locaux. Aucune image de la webcam n'est enregistrée ni envoyée. Le résultat est une indication affichée ; il ne valide ni ne rejette rien. |
| Données existantes | Les bases et photos d'avant le chiffrement sont chiffrées automatiquement à l'ouverture, puis les copies en clair sont supprimées. |

## 4. Comptes et sessions

| Mesure | Détail |
|---|---|
| Hachage | bcrypt (coût 12, sel aléatoire). Les mots de passe de plus de 72 octets sont refusés (pas de troncature silencieuse). |
| Politique | 10 à 64 caractères, au moins 3 types parmi minuscules, majuscules, chiffres et symboles. Le mot de passe ne doit contenir ni l'identifiant ni le nom, et ne doit pas figurer dans la liste des mots de passe courants. Les règles sont cochées en direct pendant la saisie. |
| Mot de passe provisoire | Un mot de passe créé ou réinitialisé par l'administrateur est généré aléatoirement et doit être changé à la première connexion. Le nouveau mot de passe doit être différent de l'ancien. |
| Blocage progressif | Après 5 échecs consécutifs, le compte est bloqué 5 min. Si les échecs continuent, la durée double à chaque fois, jusqu'à 1 h. L'administrateur peut débloquer un compte. Après chaque échec, l'écran de connexion impose aussi 1,5 s d'attente. Le changement de mot de passe est refusé pendant un blocage, pour qu'un poste resté ouvert ne permette pas d'essayer des mots de passe sans limite. |
| Frein global | 20 échecs en 10 minutes, tous comptes confondus, suspendent les connexions pendant une minute. Cela arrête l'essai d'un même mot de passe sur tous les comptes, qui reste sous le seuil de blocage de chacun. La suspension est journalisée. |
| Pas de découverte des comptes | Le message est identique pour un identifiant inconnu, un mot de passe faux ou un compte désactivé, et le temps de réponse aussi (vérification bcrypt sur un hachage leurre). Un identifiant inconnu se bloque aussi après 5 essais, avec le même message qu'un vrai compte. Ce blocage est enregistré en base comme celui d'un vrai compte : fermer puis rouvrir l'application ne fait pas apparaître de différence. Seule une empreinte HMAC de l'identifiant tapé est conservée. |
| Ré-authentification | Le mot de passe est redemandé pour restaurer une sauvegarde, afficher le code de récupération, réinitialiser un mot de passe ou donner les droits d'administrateur. |
| Verrouillage automatique | La session est verrouillée après 10 min d'inactivité (réglable de 2 à 60 min) ou avec Ctrl+L. Toutes les fenêtres sont masquées jusqu'à la saisie du mot de passe du titulaire. Une carte lue par la webcam compte comme une activité. |
| Droits | Les droits sont vérifiés dans la couche métier, pas seulement dans l'interface. Un enseignant ne voit que ses cours, dans les séances comme dans les rapports. Il reste toujours au moins un administrateur actif. |
| Session revérifiée | Toutes les 30 secondes, l'application relit le compte connecté. S'il a été désactivé ou a changé de rôle, la session se ferme. |
| Hachages renforcés | Un hachage bcrypt plus faible que la politique actuelle est recalculé à la connexion suivante, sans action de l'utilisateur. |
| Instance unique | Un verrou empêche d'ouvrir deux fois l'application sur les mêmes données. |

## 5. Journal infalsifiable

- **Lecture seule imposée par la base :** des déclencheurs SQL refusent toute modification ou
  suppression dans le journal, l'historique des corrections et les décisions de vérification.
- **Chaînage des entrées :** chaque entrée du journal porte une empreinte **HMAC-SHA256** de son
  contenu et de l'empreinte précédente. Modifier, supprimer ou réordonner une entrée, même en
  contournant l'application, casse la chaîne.
- **Contrôle :** l'onglet Administration → Sécurité indique la première entrée altérée. La clé
  HMAC est dérivée de la clé maîtresse : sans elle, impossible de recalculer une chaîne valide.

## 6. Entrées et fichiers

| Risque | Parade |
|---|---|
| Injection de formule Excel (`=HYPERLINK(…)`) | Les textes sont toujours exportés comme texte, jamais comme formule. Les noms commençant par `=` sont de toute façon refusés à la saisie et à l'import. |
| HTML dans un nom (`<img …>`) | `<` et `>` sont refusés à la saisie. À l'affichage, les données sont en texte brut ou échappées : rien n'est interprété. |
| Noms invalides | Lettres de tous alphabets, espaces, apostrophes, tirets et points. Longueur bornée, caractères de contrôle supprimés, normalisation Unicode. |
| Image piégée | La signature du fichier est contrôlée, ainsi que sa taille (15 Mo) et son nombre de pixels (40 millions, contre les « bombes de décompression »). L'image est réencodée en JPEG, ce qui supprime les métadonnées EXIF, dont la géolocalisation. |
| Pièce jointe | PDF, JPEG ou PNG uniquement : extension et contenu doivent concorder. Taille limitée à 10 Mo. Le fichier est chiffré. |
| Import CSV/Excel | 20 Mo, 20 000 lignes et 50 colonnes au maximum. La lecture d'un classeur s'arrête dès que la limite est dépassée, même s'il déclare des millions de lignes. Le matricule et la date de naissance sont contrôlés dès l'analyse, avec les mêmes règles qu'à l'enregistrement. Une photo référencée hors du dossier du fichier importé est refusée (pas de lecture de fichiers arbitraires). |
| Archive de restauration | Seuls `smartpresence.db`, `manifeste.json`, `photos/*` et `justificatifs/*` sont acceptés. Les chemins avec `..` ou `\` et les archives de plus de 4 Go décompressés sont refusés. La base est vérifiée (`integrity_check`, version, clé) avant tout remplacement, et l'état courant est sauvegardé d'abord. Si une copie échoue en cours de route (disque plein, clé USB retirée), les données actuelles sont remises en place. |
| Injection SQL | Toutes les requêtes sont paramétrées. Les seuls fragments assemblés sont des constantes du code. |

## 7. Dépendances et livraison

- **Versions figées :** `requirements.lock` fixe la version exacte des 21 paquets d'exécution.
  Le 02/11/2026, `pip-audit` y signalait 39 vulnérabilités connues, toutes dans Pillow 12.3.0,
  qui décode les photos importées. Pillow est passé en 13.0.0 le 03/11/2026 ; il est désormais
  déclaré comme dépendance directe (`pillow>=13.0`). `pip-audit` ne signale plus aucune
  vulnérabilité connue (vérifié le 03/11/2026).
- **Auto-vérification :** l'installateur et l'exécutable passent l'auto-vérification
  `--verifier`, qui contrôle notamment que la base produite est bien chiffrée.
- **Erreurs imprévues :** elles sont consignées dans `erreurs.log`, sans mot de passe ni donnée
  saisie. L'utilisateur voit un message clair, sans fermeture brutale.

Pour relancer l'audit des dépendances :

```bash
.venv\Scripts\python -m pip_audit -r requirements.lock
```

## 8. Risques résiduels et recommandations

| Risque | Recommandation |
|---|---|
| Une personne connectée sous **le même compte Windows** peut déverrouiller la clé (principe de DPAPI). | Un compte Windows personnel par membre du personnel, avec mot de passe. Verrouiller Windows (Win+L) en quittant le poste. |
| Perte du code de récupération et panne du PC = données irrécupérables. | Conserver le code imprimé dans un coffre, et une copie chez la direction. |
| Les **exports** (PDF, Excel) et les cartes imprimées sont en clair, par nature. | Les ranger dans un dossier protégé et les supprimer après usage. |
| La vérification du visage reste humaine. | C'est un choix assumé : l'écran est conçu pour que la décision soit délibérée et tracée. |
| Exécutable non signé (avertissement SmartScreen). | Signer l'installateur avec un certificat de signature de code si l'application est diffusée largement. |
| Vol du PC allumé, session Windows ouverte. | Activer **BitLocker** et le verrouillage automatique de Windows : défense en profondeur. |
| Un détenteur de la clé (code de récupération) qui modifie la base avec un outil SQLCipher peut supprimer les dernières entrées du journal sans casser la chaîne HMAC, car la clé du journal dérive de la même clé maîtresse. | Conserver le code de récupération sous clé, hors du poste, et exporter le journal régulièrement (Administration, Journal, « Exporter en Excel »). |
