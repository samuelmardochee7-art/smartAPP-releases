# Manuel utilisateur de SmartPresence

Version 1.3

SmartPresence enregistre les présences des étudiants en scannant leur carte. Après chaque
scan, la photo de l'étudiant s'affiche en grand. Le surveillant la compare avec la personne
présente : la présence n'est enregistrée qu'après sa validation. Une carte prêtée à un
camarade est ainsi repérée.

**Pour aller vite :** chaque rôle dispose d'un **guide rapide** d'une ou deux pages, à imprimer
(administrateur, appel, secrétariat), et les **questions fréquentes** répondent aux cas
courants. Ils sont dans le menu Démarrer → SmartPresence → Documentation. Dans
l'application, la touche **F1** ouvre l'aide de l'écran affiché.

## 1. Installation

1. Lancez `SmartPresence-1.3.0-installation.exe` et suivez l'assistant. Windows peut afficher
   « Windows a protégé votre ordinateur » : cliquez sur « Informations complémentaires », puis
   « Exécuter quand même ».
2. À la fin, l'installateur vérifie automatiquement que l'application fonctionne.
3. Un raccourci **SmartPresence** est créé dans le menu Démarrer (et sur le Bureau si vous l'avez demandé).

Les données (base, photos, justificatifs, sauvegardes) sont enregistrées dans
`%LOCALAPPDATA%\SmartPresence`. Une désinstallation ou une mise à jour ne les supprime jamais.

**Matériel :**

- **Ordinateur :** Windows 10 ou 11, 4 Go de mémoire.
- **Lecture des cartes :** une webcam, ou un lecteur de QR codes USB en mode « clavier ».
- **Impression des cartes :** une imprimante.

## 2. Premier lancement

Au tout premier démarrage, SmartPresence demande de créer le **compte administrateur** :
nom, identifiant et mot de passe. Ce compte sert ensuite à créer les autres comptes.

Juste après, SmartPresence affiche le **code de récupération** (14 groupes de 4 caractères).
Toutes les données sont chiffrées, et ce code est le seul moyen de les retrouver après une
panne, la réinstallation de Windows ou sur un autre ordinateur.

- Recopiez-le sur papier, ou enregistrez-le sur une clé USB, et rangez-le **sous clé, hors de
  l'ordinateur**.
- Cochez « J'ai mis ce code en lieu sûr » pour continuer.
- Il reste consultable plus tard, dans Administration → Sécurité, après saisie de votre mot de passe.

## 2 bis. Connexion et mots de passe

- **Mot de passe :** 10 caractères au moins, avec au moins 3 types parmi minuscules,
  majuscules, chiffres et symboles. Il ne doit contenir ni votre identifiant ni votre nom. Les
  règles se cochent en direct pendant la saisie. Une phrase facile à retenir fonctionne bien,
  par exemple `Kola-Lagune-Teck-47!`.
- **Mot de passe provisoire :** un compte créé ou réinitialisé par l'administrateur reçoit un
  mot de passe provisoire. Il faut le changer dès la première connexion.
- **Compte bloqué :** après 5 essais erronés, le compte est bloqué pendant 5 minutes. Si les
  erreurs continuent, la durée double à chaque fois, jusqu'à 1 heure. L'administrateur peut
  le débloquer dans **Utilisateurs**.
- **Session verrouillée :** sans activité pendant 10 minutes (réglable), ou avec **Ctrl+L**,
  toutes les fenêtres se masquent. Votre mot de passe les rouvre ; un autre utilisateur peut
  aussi se connecter à votre place. Verrouillez toujours avant de quitter le poste.
- **Thème :** en bas du menu, le bouton **Thème** fait alterner les modes automatique (comme
  Windows), clair et sombre.
- **Recherche :** **Ctrl+F** place le curseur dans le champ de recherche de l'écran affiché.
- **Aide :** **F1**, ou le bouton **Aide** en bas du menu, ouvre l'aide de l'écran affiché.
  Elle donne aussi accès à ce manuel, à votre guide rapide, aux questions fréquentes et au
  dossier des données. La version de SmartPresence y est indiquée.

## 3. Les rôles

| Rôle | Ce qu'il peut faire |
|---|---|
| **Administrateur** | Tout : comptes, classes, cours, emploi du temps, paramètres, sauvegardes, journal |
| **Enseignant** | Ouvrir les séances de ses cours, scanner, valider, corriger, consulter les rapports de ses cours |
| **Surveillant** | Ouvrir une séance de n'importe quel cours, scanner, valider ou rejeter |
| **Secrétariat / scolarité** | Étudiants, photos, cartes, import Excel, justification des absences, rapports |

Chaque utilisateur ne voit dans le menu de gauche que les écrans de son rôle. Le bouton
**Changer mon mot de passe** se trouve en bas du menu.

## 4. Préparer l'année (administrateur et secrétariat)

### 4.1 Comptes

Écran **Utilisateurs**, bouton **Nouveau compte**. Choisissez le rôle, puis cliquez sur
**Générer un mot de passe sûr**. Le mot de passe provisoire s'affiche une seule fois :
transmettez-le en main propre. Il sera changé à la première connexion.

- **Réinitialiser le mot de passe** : génère un nouveau mot de passe provisoire. Votre propre
  mot de passe vous est demandé.
- **Débloquer** : lève le blocage d'un compte après des essais erronés.
- **Désactiver** : pour un compte qui ne doit plus servir. Il n'est pas supprimé, pour que
  l'historique reste lisible.
- **Donner les droits d'administrateur** : votre mot de passe vous est demandé.

### 4.2 Filières et classes

Écran **Classes** : créez d'abord les filières (Informatique, Gestion…), puis les classes
avec leur année académique au format `2026-2027`.

### 4.3 Cours et emploi du temps

Écran **Cours** :

1. **Nouveau cours** : intitulé, classe et enseignant.
2. Sélectionnez le cours, puis **Ajouter un créneau** : jour, heure de début, heure de fin
   et salle. SmartPresence refuse deux cours en même temps pour une même classe.
3. Si des étudiants d'une autre classe suivent ce cours (option, cours mutualisé), utilisez
   **Inscrire…** et saisissez leur matricule.

### 4.4 Étudiants

Écran **Étudiants**, une à une avec **Nouvel étudiant**, ou en nombre avec **Importer CSV / Excel…** :

1. **Enregistrer un modèle CSV…** crée un fichier prêt à remplir dans Excel.
2. Remplissez les colonnes `matricule`, `nom`, `prenoms`, `classe` et, si vous le souhaitez,
   `date_naissance` (JJ/MM/AAAA) et `photo` (chemin de la photo, relatif au fichier).
3. **Choisir un fichier…** : SmartPresence vérifie chaque ligne sans rien enregistrer. Les
   erreurs s'affichent en rouge (classe inconnue, date illisible…), et les matricules déjà
   enregistrés en gris.
4. **Importer** n'enregistre que les lignes correctes.

> **La photo est indispensable.** Sans photo, la vérification visuelle est impossible et
> l'étudiant ne peut pas être pointé par scan. L'Accueil indique combien d'étudiants n'en ont
> pas. Utilisez un portrait sur fond uni.

Le matricule n'est pas modifiable, car il est inscrit dans le QR code de la carte. Un
étudiant qui a déjà des présences ne peut pas être supprimé, seulement **désactivé**.

### 4.5 Cartes étudiant

Écran **Cartes** :

1. Choisissez une classe. Sélectionnez des étudiants (Ctrl+clic ou Maj+clic), ou prenez
   toute la liste.
2. **PDF de la sélection** ou **PDF de toute la liste** : 10 cartes par page A4, avec traits de coupe.
3. Imprimez à **100 %**, sans « ajuster à la page ». Une carte doit mesurer 85,6 × 54 mm.

**Carte perdue ou volée :** sélectionnez l'étudiant, puis **Nouvelle carte (perte, vol)…**.
L'ancienne carte est refusée dès le scan suivant. Le numéro imprimé en bas à droite de la
carte augmente à chaque remplacement.

## 5. Faire l'appel (enseignant, surveillant)

### 5.1 Ouvrir la séance

Écran **Séances**, bouton **Ouvrir une séance…** :

1. Choisissez le cours : le créneau du jour est proposé d'après l'emploi du temps. Si aucun
   créneau n'est prévu ce jour-là, choisissez **Horaire libre** et saisissez les heures.
2. **Ouvrir la séance** : la fenêtre de la séance s'ouvre en plein écran.

Une séance laissée ouverte se reprend avec **Reprendre / consulter**.

### 5.2 Scanner

Dans la fenêtre de la séance, la zone **Source** propose deux façons de lire les cartes :

- **Lecteur USB** : le champ de saisie est toujours actif. Il suffit de présenter la carte au lecteur.
- **Webcam** : présentez la carte face à la caméra, à 15 à 25 cm, bien éclairée. Une carte
  restée devant la caméra n'est lue qu'une fois.

Chaque lecture émet un **bip aigu**. Une présence enregistrée joue **deux notes montantes**, un
rejet ou une anomalie **deux notes graves**. Ces sons sont ceux de SmartPresence : ils ne
dépendent pas des sons de Windows. Seul le volume de Windows les règle.

### 5.3 Vérifier : le moment clé

L'écran de vérification affiche la **photo en grand**, le nom, les prénoms, le matricule et
la classe, ainsi que l'état « À l'heure » ou « En retard de N min ».

Avec la **webcam**, un bandeau **« Aide automatique »** indique en plus si le visage filmé au
moment de la lecture ressemble à la photo : ressemblance forte (vert), incertaine (orange) ou
faible (rouge). C'est une indication, pas une décision : l'application ne valide ni ne rejette
jamais seule. Elle ne conserve aucune image. Avec le lecteur USB, qui ne voit pas l'étudiant,
ce bandeau n'apparaît pas.

**Regardez l'étudiant, puis :**

- **Entrée** : c'est bien lui. La présence est enregistrée.
- **Échap** : ce n'est pas lui. **Rien n'est enregistré** ; le rejet est inscrit au journal
  comme « tentative suspecte ».

**Garde-fous :**

- Entrée est sans effet pendant une fraction de seconde après l'ouverture de l'écran, pour
  éviter une validation par réflexe.
- Si un autre étudiant scanne sa carte pendant la vérification, son scan est ignoré et un
  message le signale. Terminez la vérification en cours, puis faites-le scanner à nouveau.

**Messages en rouge :** dans ces cas, la validation est impossible.

| Message | Que faire |
|---|---|
| Déjà pointé à HH:MM | La carte a déjà servi pour cette séance. Vérifiez qui est réellement l'étudiant. |
| Carte remplacée | La carte a été déclarée perdue. L'étudiant doit utiliser sa nouvelle carte. |
| Aucune photo | Contrôlez l'identité sur une pièce, puis utilisez **Pointage manuel…** (proposé à l'écran). |
| Carte non reconnue | Ce n'est pas une carte SmartPresence, ou le matricule est inconnu. |

**Étudiant non inscrit à ce cours :** seul l'enseignant du cours voit le bouton
**Valider quand même**. Un surveillant ne peut que rejeter.

### 5.4 Pointage manuel

**Pointage manuel…** sert dans les cas suivants : carte oubliée, photo manquante,
correction d'une erreur. Choisissez l'étudiant, le statut et l'heure d'arrivée. Le
**motif est obligatoire**. Chaque correction est tracée : auteur, date, ancienne valeur.

### 5.5 Clôturer

Bouton **Clôturer la séance** : les étudiants non pointés passent « absents ». Un bandeau
rappelle quand l'heure de fin est dépassée. Une séance oubliée est clôturée automatiquement
au lancement suivant de SmartPresence. Les corrections manuelles restent possibles après la
clôture.

## 6. Absences et justifications (secrétariat)

Écran **Absences** : choisissez la période et la classe, sélectionnez une absence, puis
**Justifier l'absence…**. Saisissez le motif et joignez éventuellement un document (PDF ou
image). **Ouvrir la pièce jointe** affiche le document plus tard.

Selon le paramètre choisi par l'administrateur, une absence justifiée ne compte pas dans le
taux d'assiduité.

## 7. Rapports

Écran **Rapports** :

- **Par étudiant, Par cours, Par classe, Évolution mensuelle** : séances, présents, retards,
  absents et taux d'assiduité.
- **Alertes d'absences** : étudiants qui atteignent le seuil d'absences non justifiées.
- **Fiche de l'étudiant** (ou double-clic sur un étudiant) : le détail séance par séance.

Filtres disponibles : période (année académique, mois, semaine ou dates libres), classe et
cours. **Exporter en Excel…** ou **Exporter en PDF…** enregistre le rapport affiché.

Le **taux d'assiduité** se calcule ainsi : présences (retards compris) ÷ séances tenues ×
100. Seules les séances clôturées comptent. Les couleurs indiquent le niveau : vert à partir
de 90 %, orange de 75 à 90 %, rouge sous 75 %.

L'**Accueil** affiche un tableau de bord : l'assiduité par classe et par mois sur l'année
académique.

## 8. Administration (administrateur)

### 8.1 Paramètres

- **Délai de tolérance :** au-delà, l'étudiant est « en retard ». Par défaut : 10 minutes.
- **Seuil d'alerte :** nombre d'absences non justifiées qui déclenche une alerte. Par défaut : 3.
- **Absences justifiées :** exclues ou non du taux d'assiduité.
- **Nom de l'établissement :** imprimé sur les cartes et les rapports.
- **Verrouillage de session :** durée d'inactivité avant verrouillage (2 à 60 minutes).
- **Dossier des sauvegardes :** de préférence sur un autre disque ou une clé USB.

### 8.2 Sauvegardes

- Une sauvegarde **automatique** a lieu chaque jour. Les 14 dernières sont conservées.
- **Sauvegarder maintenant** crée une sauvegarde manuelle, qui n'est jamais supprimée automatiquement.
- **Restaurer…** : SmartPresence vérifie la sauvegarde, affiche sa date et son contenu, puis
  demande votre mot de passe. L'état actuel est d'abord sauvegardé, par sécurité.
  L'application se ferme puis rouvre l'écran de connexion.
- Les sauvegardes sont **chiffrées**. Une sauvegarde faite sur un autre ordinateur demande le
  code de récupération de celui-ci.

### 8.3 Journal des actions

L'onglet **Journal des actions** liste les connexions, les rejets à la vérification, les
corrections, les suppressions, les sauvegardes… L'option **Actions sensibles uniquement**
ne garde que ce qui mérite un contrôle. Le journal peut être exporté en Excel.

Le journal ne peut être ni modifié ni effacé, même hors de l'application.

### 8.4 Sécurité

L'onglet **Sécurité** donne les informations suivantes :

- **État du chiffrement :** base chiffrée, nombre de photos chiffrées et empreinte de la clé.
- **Code de récupération :** il s'affiche avec **Afficher le code de récupération…**, après
  saisie de votre mot de passe.
- **Intégrité du journal :** une alerte rouge signale toute modification faite hors de
  l'application. Dans ce cas, conservez une copie de la base et prévenez la direction.
- **Données des anciens étudiants :** **Anonymiser les anciens étudiants…** efface le nom, les
  prénoms, la date de naissance, la photo et les pièces justificatives des étudiants désactivés
  depuis plus longtemps que la durée de conservation (onglet Paramètres, 5 ans par défaut). Leurs
  présences restent comptées dans les statistiques. Votre mot de passe est demandé, et
  l'opération est irréversible.

## 9. Dépannage

| Problème | Solution |
|---|---|
| La webcam ne s'ouvre pas | Fermez les autres logiciels qui l'utilisent (Teams, Zoom…), puis choisissez « Webcam 2 » si l'ordinateur en a plusieurs. SmartPresence revient au lecteur USB en cas d'échec. |
| La webcam lit mal | Éclairez la carte, évitez les reflets, rapprochez-la à 15 à 25 cm, tenez-la immobile une seconde. |
| Le lecteur USB affiche des caractères étranges | Configurez le lecteur sur la disposition clavier du poste (AZERTY France), selon sa notice. |
| Les cartes imprimées sont trop petites | Imprimez à 100 %, sans « ajuster à la page ». |
| « Fichier ouvert dans un autre programme » à l'export | Fermez le fichier dans Excel ou dans le lecteur PDF, puis recommencez. |
| Mot de passe oublié | L'administrateur le réinitialise dans **Utilisateurs** : un mot de passe provisoire est généré. |
| « Compte bloqué jusqu'à… » | Attendez l'heure indiquée, ou demandez à l'administrateur de **débloquer** le compte. |
| Au démarrage : « clé introuvable », code de récupération demandé | Windows a été réinstallé, ou les données viennent d'un autre PC ou d'un autre compte. Saisissez le code de récupération de l'administrateur. |
| « SmartPresence est déjà ouvert » | L'application est déjà lancée (barre des tâches) : une seule instance est autorisée. |
| Message « erreur imprévue » | L'opération a été annulée et les données sont intactes. Transmettez le fichier `erreurs.log` à l'assistance : **Aide** → **Ouvrir le dossier des données** l'affiche. |

D'autres réponses figurent dans les **questions fréquentes** (`docs/faq.md`, ou menu
Démarrer → SmartPresence → Documentation). Pour obtenir de l'aide, ne communiquez jamais de mot
de passe, ni le code de récupération, ni des données d'étudiants.

**Assistance SmartPresence** (pour l'administrateur de l'établissement) :
samuelmardochee7@gmail.com ou +225 01 72 75 57 07.

## 10. Protection des données personnelles

Toutes les données sont **chiffrées** sur le disque : base, photos, justificatifs et
sauvegardes. Les photos et identités ne sont accessibles qu'aux comptes autorisés. Les mots de
passe sont protégés par bcrypt.

Bonnes pratiques :

- **Comptes Windows :** un compte Windows personnel par membre du personnel, et le verrouillage
  de Windows (**Win+L**) en quittant le poste.
- **Exports :** les PDF et Excel exportés ne sont pas chiffrés. Rangez-les en lieu sûr et
  supprimez-les après usage.
- **Démonstrations publiques :** utilisez uniquement les **données fictives** de la base de
  démonstration.
- **Départs :** désactivez les comptes des personnes qui quittent l'établissement, et les
  étudiants qui ont terminé leur cursus. Une fois la durée de conservation passée, anonymisez-les
  (section 8.4).
- **Loi applicable :** l'établissement qui utilise SmartPresence avec de vraies données doit
  respecter la loi de son pays sur la protection des données personnelles (information des
  étudiants, durée de conservation, formalités éventuelles).

Le détail des protections figure dans `docs/securite.md`.
