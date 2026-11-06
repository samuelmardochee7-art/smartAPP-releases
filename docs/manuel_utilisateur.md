# Manuel utilisateur de SmartPresence

Version 1.0.0. De l'installation à l'utilisation quotidienne.

SmartPresence enregistre les présences des étudiants en scannant leur carte. Après chaque
scan, la photo de l'étudiant s'affiche en grand. Le surveillant la compare avec la personne
présente : la présence n'est enregistrée qu'après sa validation. Une carte prêtée à un
camarade est ainsi repérée.

Ce manuel suit l'ordre de la mise en service. Lisez-le une première fois du début à la fin,
puis gardez-le comme référence. Chaque rôle dispose aussi d'un **guide rapide** d'une ou deux
pages à imprimer, et la touche **F1** ouvre dans l'application l'aide de l'écran affiché.

## Sommaire

1. Comprendre SmartPresence
2. Préparer le matériel et les informations
3. Installer SmartPresence
4. Premier lancement
5. Découvrir l'interface
6. Régler l'application (administrateur)
7. Créer les comptes du personnel (administrateur)
8. Créer les filières et les classes
9. Créer les cours et l'emploi du temps
10. Enregistrer les étudiants et leurs photos (secrétariat)
11. Imprimer les cartes étudiant (secrétariat)
12. Préparer le poste de scan
13. Faire l'appel (enseignant, surveillant)
14. Justifier les absences (secrétariat)
15. Consulter les rapports
16. Sauvegardes, journal et sécurité (administrateur)
17. Routine conseillée
18. Dépannage
19. Changer d'ordinateur, mettre à jour, désinstaller
20. Protection des données personnelles
21. Assistance
22. Annexe : raccourcis clavier et vocabulaire

## 1. Comprendre SmartPresence

### 1.1 Le principe

1. Chaque étudiant reçoit une **carte** imprimée avec sa photo et un QR code.
2. Au début du cours, l'enseignant ou le surveillant **ouvre la séance** sur l'ordinateur.
3. Chaque étudiant présente sa carte à la **webcam** ou au **lecteur USB**.
4. La **photo** de l'étudiant s'affiche en grand. Le surveillant regarde la personne :
   **Entrée** si c'est bien elle, **Échap** sinon.
5. À la fin, la **clôture** de la séance marque absents les étudiants qui ne sont pas passés.
6. Le secrétariat **justifie** les absences, et chacun consulte les **rapports** d'assiduité.

### 1.2 Les rôles

| Rôle | Ce qu'il peut faire |
|---|---|
| **Administrateur** | Tout : comptes, classes, cours, emploi du temps, paramètres, sauvegardes, journal, sécurité |
| **Enseignant** | Ouvrir les séances de ses cours, scanner, valider, corriger, consulter les rapports de ses cours |
| **Surveillant** | Ouvrir une séance de n'importe quel cours, scanner, valider ou rejeter |
| **Secrétariat / scolarité** | Étudiants, photos, cartes, import Excel, justification des absences, rapports |

Chaque utilisateur ne voit dans le menu de gauche que les écrans de son rôle.

### 1.3 Le déroulé de la mise en service

| Étape | Qui | Section | Durée indicative |
|---|---|---|---|
| Préparer le matériel, les photos et la liste des étudiants | Administrateur, secrétariat | 2 | Variable |
| Installer et créer le compte administrateur | Administrateur | 3 et 4 | 15 min |
| Régler l'application | Administrateur | 6 | 10 min |
| Créer les comptes du personnel | Administrateur | 7 | 5 min par compte |
| Créer filières, classes, cours et emploi du temps | Administrateur | 8 et 9 | 1 à 2 h |
| Importer les étudiants et les photos | Secrétariat | 10 | 1 h pour quelques centaines |
| Imprimer et distribuer les cartes | Secrétariat | 11 | Variable |
| Tester le poste de scan | Enseignant ou surveillant | 12 | 15 min |
| Premier appel | Enseignant ou surveillant | 13 | Un cours |

## 2. Préparer le matériel et les informations

### 2.1 Matériel

| Élément | Exigence |
|---|---|
| Ordinateur | Windows 10 ou 11, **64 bits**, 4 Go de mémoire au moins, 1 Go d'espace libre (plus les photos) |
| Lecture des cartes | Une **webcam** (intégrée ou USB), ou un **lecteur de QR codes USB** réglé en mode « clavier » |
| Impression des cartes | Une imprimante, couleur de préférence, et du papier épais ou des pochettes à plastifier |
| Sauvegardes | Une **clé USB** ou un second disque, réservé aux sauvegardes |
| Son | Haut-parleurs ou son intégré, pour entendre les bips de lecture |

La webcam suffit pour démarrer. Le lecteur USB est plus rapide pour les grands effectifs, mais
avec lui l'aide automatique au visage n'est pas disponible (elle a besoin de voir l'étudiant).

### 2.2 Informations à réunir avant l'installation

- **Le nom de l'établissement**, tel qu'il doit apparaître sur les cartes et les rapports.
- **La liste des membres du personnel** qui utiliseront l'application, avec leur rôle.
- **Les filières et les classes** de l'année académique (par exemple `2026-2027`).
- **Les cours** : intitulé, classe, enseignant, jours, heures et salle.
- **La liste des étudiants** dans Excel : matricule, nom, prénoms, classe, et si possible date
  de naissance.
- **Une photo par étudiant** : portrait récent, de face, sur fond uni, au format JPG ou PNG.
  Nommez chaque fichier avec le matricule (par exemple `ETU2026001.jpg`) : l'import sera plus simple.

### 2.3 Choisir le poste et le compte Windows

SmartPresence fonctionne sur **un ordinateur**, sans serveur ni Internet. Ses données sont
liées au **compte Windows** sous lequel il est lancé la première fois : la clé de chiffrement
est protégée par ce compte, sur ce PC.

- Installez SmartPresence sur le poste qui servira à l'appel et à la gestion.
- Lancez toujours SmartPresence sous **le même compte Windows** sur ce poste. Chaque membre du
  personnel se connecte ensuite **dans SmartPresence** avec son propre identifiant.
- Protégez ce compte Windows par un mot de passe et verrouillez-le (**Win+L**) en quittant le poste.

## 3. Installer SmartPresence

### 3.1 Obtenir l'installateur

Le fichier d'installation s'appelle `SmartPresence-1.0.0-installation.exe`. Il est fourni par
l'auteur, ou téléchargé depuis la page des versions (« Releases ») du projet sur GitHub, avec
son empreinte SHA-256.

**Vérifier que le fichier est authentique (conseillé).** Dans l'Explorateur, faites un clic
droit dans le dossier du fichier, puis **Ouvrir dans le Terminal**, et tapez :

```
Get-FileHash .\SmartPresence-1.0.0-installation.exe
```

Comparez la valeur affichée avec l'empreinte publiée. Si elles diffèrent, n'installez pas le
fichier et prévenez l'assistance.

### 3.2 Lancer l'installation

1. Double-cliquez sur `SmartPresence-1.0.0-installation.exe`.
2. Si Windows affiche « Windows a protégé votre ordinateur », cliquez sur **Informations
   complémentaires**, puis **Exécuter quand même**. Ce message apparaît parce que l'installateur
   n'est pas signé par un éditeur commercial.
3. L'assistant demande pour qui installer. **Pour tous les utilisateurs** demande les droits
   d'administrateur de Windows ; **pour moi uniquement** n'en demande pas. Les deux conviennent.
4. Acceptez le dossier proposé, sauf consigne contraire de votre service informatique.
5. Cochez **Créer un raccourci sur le Bureau** si vous le souhaitez.
6. Cliquez sur **Installer**. À la fin, l'installateur **vérifie automatiquement** que
   l'application fonctionne (chiffrement, PDF, sauvegarde, lecture des QR codes).
7. Laissez cochée la case **Lancer SmartPresence** et cliquez sur **Terminer**.

### 3.3 Ce qui est installé

- L'application, dans `Program Files\SmartPresence` (ou dans votre profil si vous avez choisi
  « pour moi uniquement »).
- Dans le menu Démarrer, le dossier **SmartPresence** : l'application, et un sous-dossier
  **Documentation** avec ce manuel, les trois guides rapides et les questions fréquentes.
- Les **données** (base, photos, justificatifs, sauvegardes automatiques) sont créées au
  premier lancement dans `%LOCALAPPDATA%\SmartPresence`. Tout y est chiffré.

Une désinstallation ou une mise à jour ne supprime **jamais** ces données.

## 4. Premier lancement

### 4.1 Créer le compte administrateur

Au tout premier démarrage, la fenêtre **Premier lancement de SmartPresence** s'ouvre :

1. **Établissement** : le nom imprimé sur les cartes et les rapports. Il reste modifiable plus tard.
2. **Nom complet** : votre nom, tel qu'il apparaîtra dans le journal.
3. **Identifiant** : `admin` est proposé ; vous pouvez le changer.
4. **Mot de passe** puis **Confirmation** : voir les règles en 4.3.
5. Cliquez sur **Créer le compte**.

### 4.2 Mettre le code de récupération en lieu sûr

Juste après, SmartPresence affiche le **code de récupération** : 14 groupes de 4 caractères.
Toutes les données sont chiffrées, et ce code est le **seul** moyen de les retrouver après une
panne, une réinstallation de Windows ou sur un autre ordinateur.

1. Recopiez-le sur papier, ou enregistrez-le sur une clé USB.
2. Rangez-le **sous clé, hors de l'ordinateur** (coffre, armoire fermée de la direction).
3. Cochez **J'ai mis ce code en lieu sûr, hors de cet ordinateur** pour continuer.

Il reste consultable plus tard dans Administration → Sécurité, après saisie de votre mot de
passe. Ne l'envoyez jamais par e-mail ou par messagerie.

> **Sans ce code, des données perdues ne peuvent pas être récupérées**, même par l'assistance.

### 4.3 Les règles des mots de passe

- **10 caractères au moins**, avec au moins **3 types** parmi : minuscules, majuscules,
  chiffres et symboles. Les règles se cochent en direct pendant la saisie.
- Il ne doit contenir **ni votre identifiant ni votre nom**.
- Une phrase facile à retenir fonctionne bien, par exemple `Kola-Lagune-Teck-47!`.
- Après **5 essais erronés**, le compte est bloqué 5 minutes. Si les erreurs continuent, la
  durée double à chaque fois, jusqu'à 1 heure.

### 4.4 Se connecter

L'écran de connexion demande l'**identifiant** et le **mot de passe**. Après la connexion,
l'écran **Accueil** s'affiche. Un compte qui a reçu un **mot de passe provisoire** doit le
changer dès la première connexion : SmartPresence le demande automatiquement.

## 5. Découvrir l'interface

### 5.1 La fenêtre principale

- **Le menu de gauche** donne accès aux écrans de votre rôle : Accueil, Séances, Étudiants,
  Cartes, Classes, Cours, Absences, Rapports, Utilisateurs, Administration. Un trait jaune
  signale l'écran affiché.
- **En bas du menu** : **Aide**, **Thème** (automatique comme Windows, clair ou sombre),
  **Changer mon mot de passe**, **Verrouiller** et **Se déconnecter**.
- **L'Accueil** est un tableau de bord : chiffres clés, étudiants sans photo, alertes
  d'absences, assiduité par classe et par mois. Les tuiles sont cliquables et mènent à l'écran
  concerné. Une tuile en alerte indique l'action attendue (par exemple ajouter des photos).

### 5.2 L'aide intégrée

**F1**, ou le bouton **Aide**, ouvre l'aide de l'écran affiché. Elle donne aussi accès à ce
manuel, à votre guide rapide, aux questions fréquentes et au dossier des données, et indique
la version de SmartPresence.

### 5.3 Verrouiller la session

Sans activité pendant 10 minutes (réglable), ou avec **Ctrl+L** ou le bouton **Verrouiller**,
toutes les fenêtres se masquent. Votre mot de passe les rouvre ; un autre utilisateur peut
aussi se connecter à votre place. **Verrouillez toujours avant de quitter le poste.**

### 5.4 Confirmation par mot de passe

Certaines actions sensibles (restauration, réinitialisation d'un mot de passe, rôle
administrateur, affichage du code de récupération, anonymisation) demandent de **saisir à
nouveau votre mot de passe**. C'est normal.

## 6. Régler l'application (administrateur)

Écran **Administration**, onglet **Paramètres**. Modifiez les valeurs, puis cliquez sur
**Enregistrer les paramètres**.

| Paramètre | Rôle | Par défaut |
|---|---|---|
| **Délai de tolérance** | Au-delà, l'étudiant est « en retard » | 10 minutes |
| **Seuil d'alerte** | Nombre d'absences non justifiées qui déclenche une alerte | 3 |
| **Absences justifiées** | Les exclure ou non du taux d'assiduité | Selon votre règlement |
| **Nom de l'établissement** | Imprimé sur les cartes et les rapports | Celui saisi au premier lancement |
| **Verrouillage de session** | Durée d'inactivité avant verrouillage (2 à 60 minutes) | 10 minutes |
| **Conservation des données après le départ d'un étudiant** | Délai avant de pouvoir anonymiser un ancien étudiant | 5 ans |
| **Dossier des sauvegardes** | Où sont copiées les sauvegardes | Dans le dossier des données |

**Conseil :** avec **Parcourir…**, choisissez comme dossier des sauvegardes un **autre disque**
ou une **clé USB** dédiée. Une sauvegarde sur le même disque ne protège pas d'une panne de ce disque.

## 7. Créer les comptes du personnel (administrateur)

Écran **Utilisateurs** :

1. Cliquez sur **Nouveau compte**.
2. Saisissez le nom complet et l'identifiant (par exemple l'initiale du prénom suivie du nom :
   `bkouakou`).
3. Choisissez le **rôle** : enseignant, surveillant, secrétariat ou administrateur.
4. Cliquez sur **Générer un mot de passe sûr**, puis **Enregistrer**.
5. Le mot de passe provisoire s'affiche **une seule fois** : notez-le, transmettez-le **en main
   propre**, puis cliquez sur **J'ai transmis le mot de passe**. La personne le changera à sa
   première connexion.

**Créez un second compte administrateur** (par exemple pour la direction). Si l'unique
administrateur oublie son mot de passe, personne d'autre ne pourrait le réinitialiser.

Les autres boutons de l'écran :

- **Modifier** : nom, identifiant, rôle. Donner le rôle administrateur demande votre mot de passe.
- **Réinitialiser le mot de passe** : génère un nouveau mot de passe provisoire (mot de passe oublié).
- **Débloquer** : lève le blocage d'un compte après des essais erronés.
- **Activer / désactiver** : pour une personne qui quitte l'établissement. Le compte n'est pas
  supprimé, pour que l'historique reste lisible.

## 8. Créer les filières et les classes

Écran **Classes** :

1. Dans la partie **Filières**, cliquez sur **Nouvelle** et saisissez le libellé (Informatique,
   Gestion…). Recommencez pour chaque filière.
2. Cliquez sur **Nouvelle classe** : choisissez la filière, saisissez le libellé de la classe
   (par exemple `Licence 1 Informatique`) et l'**année académique** au format `2026-2027`.
3. Recommencez pour chaque classe.

Le libellé de la classe doit être **exactement** celui que vous utiliserez dans la colonne
`classe` du fichier d'import des étudiants (section 10.2).

## 9. Créer les cours et l'emploi du temps

Écran **Cours** :

1. **Nouveau cours** : intitulé, classe et enseignant. L'enseignant doit déjà avoir un compte
   (section 7).
2. Sélectionnez le cours, puis **Ajouter un créneau** : jour, heure de début, heure de fin et
   salle. Ajoutez autant de créneaux que de séances par semaine. SmartPresence refuse deux
   cours en même temps pour une même classe.
3. Si des étudiants d'une autre classe suivent ce cours (option, cours mutualisé), cliquez sur
   **Inscrire…** et saisissez leur matricule. **Retirer** annule une inscription.

L'emploi du temps sert à proposer le bon cours à l'ouverture d'une séance, à calculer les
retards et à clôturer les séances oubliées.

## 10. Enregistrer les étudiants et leurs photos (secrétariat)

### 10.1 Un étudiant à la fois

Écran **Étudiants**, bouton **Nouvel étudiant** : matricule, nom, prénoms, classe, date de
naissance, puis **Choisir une photo…**. Enregistrez.

### 10.2 Toute une liste à la fois (import)

1. Écran **Étudiants**, bouton **Importer CSV / Excel…**.
2. **Enregistrer un modèle CSV…** crée un fichier prêt à remplir dans Excel.
3. Remplissez une ligne par étudiant :

| Colonne | Obligatoire | Exemple |
|---|---|---|
| `matricule` | Oui | `ETU2026001` |
| `nom` | Oui | `KOUAMÉ` |
| `prenoms` | Oui | `Aya Grâce` |
| `classe` | Oui | `Licence 1 Informatique` (libellé exact, section 8) |
| `date_naissance` | Non | `14/03/2007` (JJ/MM/AAAA) |
| `photo` | Non | `photos\ETU2026001.jpg` (chemin relatif au fichier d'import) |

4. Enregistrez le fichier (CSV ou Excel) et placez le dossier `photos` à côté de lui.
5. **Choisir un fichier…** : SmartPresence **vérifie chaque ligne sans rien enregistrer**. Les
   erreurs s'affichent en rouge (classe inconnue, date illisible…), les matricules déjà
   enregistrés en gris.
6. Corrigez les erreurs dans le fichier et rechargez-le, ou continuez : **Importer** n'enregistre
   que les lignes correctes.

### 10.3 Les photos

> **La photo est indispensable.** Sans photo, la vérification visuelle est impossible et
> l'étudiant ne peut pas être pointé par scan. L'Accueil indique combien d'étudiants n'en ont pas.

- Portrait **récent, de face**, visage bien éclairé, **fond uni**, sans lunettes de soleil ni
  couvre-chef qui masque le visage.
- JPG ou PNG. SmartPresence réencode la photo sans ses métadonnées et la chiffre.
- Pour ajouter ou changer une photo : ouvrez la fiche de l'étudiant (double-clic), puis
  **Choisir une photo…**.

### 10.4 Bon à savoir

- Le **matricule n'est pas modifiable**, car il est inscrit dans le QR code de la carte.
- Un étudiant qui a déjà des présences ne peut pas être supprimé, seulement **désactivé**
  (fin de cursus, abandon).
- **Ctrl+F** place le curseur dans le champ de recherche.

## 11. Imprimer les cartes étudiant (secrétariat)

### 11.1 Générer le PDF

Écran **Cartes** :

1. Vérifiez la ligne **Établissement imprimé**. Si besoin, cliquez sur **Modifier le nom de
   l'établissement…**.
2. Choisissez une **classe**. La colonne Photo signale les étudiants sans photo : complétez-les
   d'abord.
3. Sélectionnez des étudiants (Ctrl+clic ou Maj+clic), puis **PDF de la sélection**, ou bien
   **PDF de toute la liste**.
4. Enregistrez le PDF : 10 cartes par page A4, avec traits de coupe.

### 11.2 Imprimer et découper

1. Ouvrez le PDF et imprimez à **100 %** (« taille réelle »), **sans** « ajuster à la page ».
2. Mesurez une carte : elle doit faire **85,6 × 54 mm** (format carte bancaire).
3. Découpez le long des traits de coupe. Plastifiez si possible : le QR code doit rester net,
   sans pli ni reflet.
4. **Testez quelques cartes** sur le poste de scan (section 12) avant de les distribuer toutes.

### 11.3 Carte perdue ou volée

Sélectionnez l'étudiant, puis **Nouvelle carte (perte, vol)…** et imprimez la nouvelle carte.
L'ancienne est **refusée dès le scan suivant**. Le numéro imprimé en bas à droite de la carte
augmente à chaque remplacement.

## 12. Préparer le poste de scan

### 12.1 Avec une webcam

- Placez la webcam face à l'endroit où les étudiants présenteront leur carte, à hauteur de main.
- Éclairage : une pièce bien éclairée, sans lampe ni fenêtre juste derrière la carte (les
  reflets gênent la lecture).
- Fermez les logiciels qui utilisent la caméra (Teams, Zoom, WhatsApp…).

### 12.2 Avec un lecteur de QR codes USB

- Branchez le lecteur : Windows le reconnaît comme un clavier, sans pilote.
- Ouvrez le Bloc-notes et scannez une carte : le texte lu doit commencer par `SP-`. Si des
  caractères étranges apparaissent, réglez le lecteur sur la disposition clavier du poste
  (AZERTY France) en suivant sa notice.

### 12.3 Faire un essai

1. Ouvrez une séance d'un vrai cours, en **Horaire libre** si aucun créneau n'est prévu
   (section 13.1).
2. Scannez la carte d'un étudiant de la classe.
3. Vérifiez : le bip aigu à la lecture, la photo en grand, deux notes montantes à la validation.
4. Montez le volume de Windows si les sons sont trop faibles.
5. Si cet essai ne doit pas compter, corrigez le pointage avec **Pointage manuel…** (motif :
   essai du poste).

## 13. Faire l'appel (enseignant, surveillant)

### 13.1 Ouvrir la séance

Écran **Séances**, bouton **Ouvrir une séance…** :

1. Choisissez le cours. Le créneau du jour est proposé d'après l'emploi du temps. Si aucun
   créneau n'est prévu ce jour-là, choisissez **Horaire libre** et saisissez les heures.
2. Cliquez sur **Ouvrir la séance** : la fenêtre de la séance s'ouvre en plein écran.

La fenêtre affiche l'horloge, les compteurs de présents, de retards et d'attendus, et la liste
des pointages. Une séance laissée ouverte se reprend avec **Reprendre ou consulter**.

### 13.2 Choisir la source et scanner

Dans la zone **Source**, choisissez :

- **Lecteur USB** : le champ de saisie est toujours actif. L'étudiant présente sa carte au lecteur.
- **Webcam 1** (ou **Webcam 2** si l'ordinateur en a plusieurs) : l'étudiant présente sa carte
  face à la caméra, à **15 à 25 cm**, immobile une seconde. Une carte restée devant la caméra
  n'est lue qu'une fois.

Chaque lecture émet un **bip aigu**. Une présence enregistrée joue **deux notes montantes**, un
rejet ou une anomalie **deux notes graves**. Seul le volume de Windows règle ces sons.

### 13.3 Vérifier : le moment clé

L'écran de vérification affiche la **photo en grand**, le nom, les prénoms, le matricule, la
classe et l'état **À l'heure** ou **En retard de N min**.

Avec la **webcam**, un bandeau **Aide automatique** indique si le visage filmé au moment de la
lecture ressemble à la photo : ressemblance **forte** (vert), **incertaine** (orange) ou
**faible** (rouge). C'est une indication, pas une décision : l'application ne valide ni ne
rejette jamais seule, et ne conserve aucune image. Avec le lecteur USB, ce bandeau n'apparaît pas.

**Regardez l'étudiant, puis :**

- **Entrée** : c'est bien lui. La présence est enregistrée.
- **Échap** : ce n'est pas lui. **Rien n'est enregistré** ; le rejet est inscrit au journal
  comme « tentative suspecte ». Gardez la carte et appliquez votre règlement intérieur.

**Garde-fous :**

- Entrée est sans effet pendant une fraction de seconde après l'ouverture de l'écran, pour
  éviter une validation par réflexe.
- Si un autre étudiant scanne sa carte pendant la vérification, son scan est ignoré et un
  message le signale. Terminez la vérification en cours, puis faites-le scanner à nouveau.

### 13.4 Messages en rouge

| Message | Que faire |
|---|---|
| Déjà pointé à HH:MM | La carte a déjà servi pour cette séance. Vérifiez qui est réellement l'étudiant. |
| Carte remplacée | La carte a été déclarée perdue. L'étudiant doit utiliser sa nouvelle carte. |
| Aucune photo | Contrôlez l'identité sur une pièce, puis utilisez **Pointage manuel…** (proposé à l'écran). |
| Carte non reconnue | Ce n'est pas une carte SmartPresence, ou le matricule est inconnu. |
| Étudiant non inscrit à ce cours | Seul l'enseignant du cours voit **Valider quand même (enseignant)**. Un surveillant ne peut que rejeter. |

### 13.5 Pointage manuel

**Pointage manuel…** sert pour une carte oubliée, une photo manquante ou la correction d'une
erreur. Choisissez l'étudiant, le statut (présent, en retard, absent) et l'heure d'arrivée. Le
**motif est obligatoire**. Chaque correction est tracée : auteur, date, ancienne valeur.

### 13.6 Clôturer la séance

Cliquez sur **Clôturer la séance** à la fin de l'appel ou du cours : les étudiants non pointés
passent **absents**. Un bandeau rappelle quand l'heure de fin est dépassée. Une séance oubliée
est clôturée automatiquement au lancement suivant de SmartPresence. Les corrections manuelles
restent possibles après la clôture.

## 14. Justifier les absences (secrétariat)

Écran **Absences** :

1. Choisissez la **période** et la **classe**.
2. Sélectionnez l'absence, puis **Justifier l'absence…**.
3. Choisissez le **motif** et, si besoin, joignez un document avec **Choisir…** (PDF ou image :
   certificat médical, convocation…). Le document est chiffré.
4. **Ouvrir la pièce jointe** affiche le document plus tard.

Selon le paramètre choisi par l'administrateur (section 6), une absence justifiée compte ou non
dans le taux d'assiduité.

## 15. Consulter les rapports

Écran **Rapports** :

1. Choisissez le type de rapport : **Par étudiant**, **Par cours**, **Par classe**,
   **Évolution mensuelle** ou **Alertes d'absences**.
2. Réglez les filtres : période (année académique, mois, semaine ou dates libres), classe, cours.
3. Double-cliquez sur un étudiant, ou cliquez sur **Fiche de l'étudiant**, pour le détail séance
   par séance. **← Retour au rapport** revient à la liste.
4. **Exporter en Excel…** ou **Exporter en PDF…** enregistre le rapport affiché.

Le **taux d'assiduité** = présences (retards compris) ÷ séances tenues × 100. Seules les séances
clôturées comptent. Couleurs : **vert** à partir de 90 %, **orange** de 75 à 90 %, **rouge** sous 75 %.

Les **alertes d'absences** listent les étudiants qui atteignent le seuil d'absences non
justifiées (section 6). Un enseignant ne voit que les rapports de ses cours.

## 16. Sauvegardes, journal et sécurité (administrateur)

### 16.1 Sauvegardes

Écran **Administration**, onglet **Sauvegardes** :

- Une sauvegarde **automatique** a lieu chaque jour. Les 14 dernières sont conservées.
- **Sauvegarder maintenant** crée une sauvegarde manuelle, jamais supprimée automatiquement.
  Faites-en une avant toute opération importante (import massif, fin d'année, réinstallation).
- **Ouvrir le dossier** affiche les fichiers de sauvegarde, pour les copier sur une clé USB.
- Les sauvegardes sont **chiffrées** : une clé USB perdue ne révèle rien.

**Restaurer une sauvegarde :**

1. Sélectionnez une sauvegarde de la liste et cliquez sur **Restaurer la sauvegarde
   sélectionnée…**, ou cliquez sur **Restaurer depuis un fichier…** pour un fichier venu
   d'ailleurs (clé USB).
2. SmartPresence vérifie la sauvegarde et affiche sa date et son contenu.
3. Saisissez votre mot de passe. L'état actuel est d'abord sauvegardé, par sécurité.
4. L'application se ferme puis rouvre l'écran de connexion.

Une sauvegarde faite sur un autre ordinateur demande le **code de récupération** de celui-ci.

### 16.2 Journal des actions

L'onglet **Journal des actions** liste les connexions, les rejets à la vérification, les
corrections, les suppressions, les sauvegardes… La case **Actions sensibles uniquement** ne
garde que ce qui mérite un contrôle. **Exporter en Excel…** enregistre le journal. Il ne peut
être ni modifié ni effacé, même hors de l'application.

### 16.3 Sécurité

L'onglet **Sécurité** affiche :

- **L'état du chiffrement** : base chiffrée, nombre de photos chiffrées, empreinte de la clé.
- **Le code de récupération** : **Afficher le code de récupération…**, après saisie de votre mot
  de passe.
- **L'intégrité du journal** (**Vérifier maintenant** relance le contrôle) : une alerte rouge
  signale une modification faite hors de l'application. Dans ce cas, ne touchez à rien, gardez
  une copie du dossier `%LOCALAPPDATA%\SmartPresence` et prévenez la direction.
- **Les données des anciens étudiants** : **Anonymiser les anciens étudiants…** efface le nom,
  les prénoms, la date de naissance, la photo et les pièces justificatives des étudiants
  désactivés depuis plus longtemps que la durée de conservation. Leurs présences restent
  comptées dans les statistiques. Votre mot de passe est demandé, et l'opération est
  **irréversible**.

## 17. Routine conseillée

| Quand | Qui | Quoi |
|---|---|---|
| Chaque séance | Enseignant, surveillant | Ouvrir, scanner, vérifier chaque photo, clôturer |
| Chaque jour | Secrétariat | Justifier les absences reçues |
| Chaque semaine | Administrateur | Consulter les alertes d'absences ; parcourir le journal en « actions sensibles uniquement » ; vérifier que la sauvegarde automatique existe |
| Chaque mois | Administrateur | **Sauvegarder maintenant** et ranger une copie hors du poste ; exporter les rapports du mois |
| Nouvel étudiant | Secrétariat | Fiche, photo, carte |
| Départ d'un membre du personnel | Administrateur | Désactiver son compte |
| Fin d'année | Administrateur, secrétariat | Sauvegarde manuelle ; désactiver les étudiants sortis ; créer les classes de la nouvelle année ; importer les nouveaux étudiants ; anonymiser les anciens au-delà de la durée de conservation |

## 18. Dépannage

| Problème | Solution |
|---|---|
| « Windows a protégé votre ordinateur » à l'installation | **Informations complémentaires**, puis **Exécuter quand même** (section 3.2). |
| La webcam ne s'ouvre pas | Fermez les autres logiciels qui l'utilisent (Teams, Zoom…), puis choisissez « Webcam 2 » si l'ordinateur en a plusieurs. Dans Paramètres Windows → Confidentialité → Caméra, autorisez les applications de bureau. SmartPresence revient au lecteur USB en cas d'échec. |
| La webcam lit mal | Éclairez la carte, évitez les reflets, rapprochez-la à 15 à 25 cm, tenez-la immobile une seconde. |
| Le lecteur USB affiche des caractères étranges | Réglez le lecteur sur la disposition clavier du poste (AZERTY France), selon sa notice. |
| On n'entend pas les bips | Montez le volume de Windows et vérifiez la sortie audio choisie. |
| Les cartes imprimées sont trop petites | Imprimez à 100 %, sans « ajuster à la page ». |
| Un étudiant ne peut pas être pointé par scan | Il n'a pas de photo : ajoutez-la (section 10.3), ou pointez-le manuellement après contrôle d'identité. |
| L'import refuse une classe | Le libellé de la colonne `classe` doit être exactement celui de l'écran Classes. |
| « Fichier ouvert dans un autre programme » à l'export | Fermez le fichier dans Excel ou dans le lecteur PDF, puis recommencez. |
| Mot de passe oublié | L'administrateur le réinitialise dans **Utilisateurs** : un mot de passe provisoire est généré. |
| « Compte bloqué jusqu'à… » | Attendez l'heure indiquée, ou demandez à l'administrateur de **débloquer** le compte. |
| Au démarrage : « clé introuvable », code de récupération demandé | Windows a été réinstallé, ou les données viennent d'un autre PC ou d'un autre compte Windows. Saisissez le code de récupération de l'administrateur. |
| L'application démarre comme au premier jour, sans données | Elle a été lancée sous un autre compte Windows. Fermez-la et reconnectez-vous à Windows avec le compte habituel (section 2.3). |
| « SmartPresence est déjà ouvert » | L'application est déjà lancée (barre des tâches) : une seule instance est autorisée. |
| Message « erreur imprévue » | L'opération a été annulée et les données sont intactes. Transmettez le fichier `erreurs.log` à l'assistance : **Aide** → **Ouvrir le dossier des données** l'affiche. |

D'autres réponses figurent dans les **questions fréquentes** (menu Démarrer → SmartPresence →
Documentation).

## 19. Changer d'ordinateur, mettre à jour, désinstaller

### 19.1 Installer une version plus récente

Faites d'abord **Sauvegarder maintenant**, puis lancez simplement l'installateur de la nouvelle
version. Les données sont conservées et, si besoin, mises à niveau au premier lancement.

### 19.2 Passer sur un nouvel ordinateur

1. Sur l'ancien poste : **Administration → Sauvegardes → Sauvegarder maintenant**, puis
   **Ouvrir le dossier** et copiez la sauvegarde sur une clé USB.
2. Sur le nouveau poste : installez SmartPresence (section 3) et créez un compte administrateur
   provisoire au premier lancement.
3. **Administration → Sauvegardes → Restaurer depuis un fichier…**, et choisissez le fichier de
   la clé USB.
4. Saisissez le **code de récupération** de l'ancien poste quand il est demandé.
5. Connectez-vous ensuite avec les comptes d'origine.

### 19.3 Désinstaller

Menu Démarrer → SmartPresence → **Désinstaller SmartPresence**, ou Paramètres Windows →
Applications. Le dossier des données `%LOCALAPPDATA%\SmartPresence` est **conservé**. Pour tout
effacer définitivement (fin d'utilisation), faites d'abord une dernière sauvegarde si votre
règlement l'exige, puis supprimez ce dossier à la main.

## 20. Protection des données personnelles

Toutes les données sont **chiffrées** sur le disque : base, photos, justificatifs et sauvegardes.
Les photos et identités ne sont accessibles qu'aux comptes autorisés. Les mots de passe sont
protégés par bcrypt.

Bonnes pratiques :

- **Poste :** un compte Windows protégé par mot de passe, verrouillé (**Win+L**) en quittant le
  poste ; dans SmartPresence, un compte personnel par membre du personnel, jamais partagé.
- **Exports :** les PDF et Excel exportés ne sont **pas** chiffrés. Rangez-les en lieu sûr et
  supprimez-les après usage.
- **Démonstrations publiques :** n'utilisez jamais de vraies données d'étudiants.
- **Départs :** désactivez les comptes des personnes qui quittent l'établissement, et les
  étudiants qui ont terminé leur cursus. Une fois la durée de conservation passée,
  anonymisez-les (section 16.3).
- **Loi applicable :** l'établissement qui utilise SmartPresence avec de vraies données doit
  respecter la loi de son pays sur la protection des données personnelles (information des
  étudiants, durée de conservation, formalités éventuelles).

## 21. Assistance

1. **Dans l'application :** **F1** ou **Aide**.
2. **La documentation :** menu Démarrer → SmartPresence → Documentation.
3. **L'administrateur de votre établissement** pour les comptes, mots de passe et paramètres.
4. **Assistance SmartPresence** (pour l'administrateur de l'établissement) :
   samuelmardochee7@gmail.com ou +225 01 72 75 57 07.

Indiquez la version (affichée dans l'aide, **F1**), l'écran concerné, le message exact et ce que
vous faisiez. Joignez le fichier `erreurs.log` si un message « erreur imprévue » est apparu.
Ne communiquez **jamais** de mot de passe, ni le code de récupération, ni des données d'étudiants.

## 22. Annexe : raccourcis clavier et vocabulaire

### 22.1 Raccourcis clavier

| Touche | Effet |
|---|---|
| **F1** | Aide de l'écran affiché |
| **Ctrl+F** | Aller au champ de recherche |
| **Ctrl+L** | Verrouiller la session |
| **Entrée** (vérification) | Valider : c'est bien l'étudiant |
| **Échap** (vérification) | Rejeter : ce n'est pas l'étudiant |
| **Win+L** | Verrouiller Windows |

### 22.2 Vocabulaire

| Terme | Sens |
|---|---|
| **Séance** | Une occurrence d'un cours, à une date donnée, pendant laquelle on fait l'appel |
| **Créneau** | Une ligne de l'emploi du temps : jour, heures et salle d'un cours |
| **Clôture** | Fin de l'appel : les non-pointés passent absents |
| **Délai de tolérance** | Minutes après le début du cours avant d'être compté en retard |
| **Code de récupération** | Code de secours qui permet de déchiffrer les données sur un autre poste ou après une réinstallation |
| **Anonymisation** | Effacement de l'identité, de la photo et des pièces d'un ancien étudiant, en gardant les statistiques |
| **Journal** | Liste infalsifiable des actions sensibles |
