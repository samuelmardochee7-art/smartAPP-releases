# Historique des versions

Les changements notables de SmartPresence, du plus récent au plus ancien.
Format inspiré de [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) ; numérotation
[SemVer](https://semver.org/lang/fr/).

## [1.0.0] - 2026-11-05

Première version publique de SmartPresence.

### Appel et anti-fraude

- Ouverture d'une séance depuis l'emploi du temps, ou en horaire libre.
- Lecture des cartes par **webcam** ou par **lecteur de QR codes USB**, avec un son à chaque
  lecture, à chaque validation et à chaque rejet.
- **Vérification visuelle** : après chaque scan, la photo de l'étudiant s'affiche en grand.
  Entrée valide, Échap rejette et inscrit une « tentative suspecte » au journal.
- Contrôles automatiques : double scan, étudiant hors de son cours, photo manquante, carte
  remplacée. Seul l'enseignant du cours peut valider un étudiant non inscrit.
- **Aide à la comparaison faciale** à la webcam : ressemblance forte, incertaine ou faible
  entre le visage filmé et la photo. C'est une indication ; la décision reste humaine et
  aucune image n'est conservée.
- Pointage manuel avec motif obligatoire, corrections tracées, clôture qui passe les
  non-pointés « absents », clôture automatique des séances oubliées.

### Gestion

- Étudiants avec photo, import CSV/Excel vérifié ligne par ligne avant enregistrement.
- Filières, classes, cours, emploi du temps, inscriptions hors classe.
- Comptes et quatre rôles : administrateur, enseignant, surveillant, secrétariat.
- **Cartes étudiant** en PDF (85,6 × 54 mm, 10 par page A4) avec QR code ; une carte perdue
  est remplacée et l'ancienne refusée aussitôt.
- Justification des absences avec motif et pièce jointe.

### Rapports

- Assiduité par étudiant, par cours, par classe et par mois ; alertes d'absences ; fiche
  individuelle ; tableau de bord.
- Exports Excel et PDF.

### Sécurité et données personnelles

- Données **chiffrées** : base SQLCipher (AES-256), photos, justificatifs et sauvegardes en
  AES-256-GCM. Clé protégée par Windows et code de récupération remis à l'administrateur.
- Mots de passe bcrypt, politique affichée en direct, mots de passe provisoires, blocage
  progressif après 5 échecs.
- Verrouillage de session (inactivité ou Ctrl+L), ré-authentification pour les actions
  sensibles, une seule instance de l'application.
- Journal des actions scellé : toute modification faite hors de l'application est détectée.
- Anonymisation des anciens étudiants au-delà d'une durée de conservation réglable.
- Sauvegarde automatique quotidienne, sauvegarde manuelle, restauration vérifiée.

### Interface et documentation

- Identité « cahier d'appel » : encre bleue sur papier, marge rouge, lignes de cahier,
  statuts en tampons encreurs, grands chiffres lisibles de loin.
- Thèmes clair et sombre (contrastes WCAG AA), animations qui respectent le réglage
  d'accessibilité de Windows, raccourcis Ctrl+F, Ctrl+L et F1.
- Aide intégrée (**F1**), manuel utilisateur complet de l'installation à l'utilisation,
  guides rapides par rôle et questions fréquentes, installés avec l'application.
- Installateur Windows avec auto-vérification.

[1.0.0]: https://github.com/samuelmardochee7-art/smartAPP/releases/tag/v1.0.0
