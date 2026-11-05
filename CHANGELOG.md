# Historique des versions

Les changements notables de SmartPresence, du plus récent au plus ancien.
Format inspiré de [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) ; numérotation
[SemVer](https://semver.org/lang/fr/).

## [Non publié]

### Modifié

- **Cahier d'appel :** fond papier (thème clair), filet de marge rouge le long des écrans, et
  tableaux réglés comme un cahier (une ligne fine sous chaque rangée) au lieu des lignes
  alternées.
- **Tampons :** dans les tableaux, les statuts Présent, En retard et Absent s'affichent comme
  des tampons encreurs à la couleur du statut. Sur l'écran de vérification, le statut du scan
  (« À l'heure », « En retard de 6 min ») tombe en tampon sur le coin de la photo, loin du visage.
- **Signalétique :** libellés en capitales espacées (tuiles, fiche de vérification, bandeau de
  séance) et très grands chiffres à chasse fixe pour les tuiles et l'horloge de séance, qui ne
  tremble plus à chaque seconde.

### Corrigé

- Accessibilité : les contours des champs et des boutons atteignent 3:1 dans les deux thèmes ;
  la coche des cases est foncée en thème sombre (elle était blanche sur bleu clair) ; une tuile
  en alerte dit l'action attendue, le contour jaune seul se voyant mal en thème clair.
- L'accent d'une capitale (« Étudiants ») était rogné en haut des titres de page.

## [1.3.0] - 2026-11-04

### Ajouté

- **Aide à la comparaison faciale (F17) :** à la webcam, le visage filmé au moment de la
  lecture est comparé à la photo de l'étudiant, et l'écran de vérification affiche une
  ressemblance forte, incertaine ou faible. C'est une indication : l'application ne valide ni
  ne rejette jamais seule, et ne conserve aucune image. Modèles YuNet et SFace d'OpenCV Zoo,
  récupérés par `scripts/telecharger_modeles.py` (empreintes vérifiées) et embarqués dans
  l'installateur.
- **Anonymisation des anciens étudiants :** au-delà d'une durée de conservation réglable
  (5 ans par défaut), l'administrateur efface l'identité, la photo et les pièces
  justificatives des étudiants désactivés. Les statistiques restent justes.
- **Nom de l'établissement demandé au premier lancement.**

### Corrigé

- Le bip de lecture ne s'entendait pas : les sons système de Windows sont très discrets avec
  certains modèles de sons. L'application joue maintenant ses propres sons : bip aigu à la
  lecture, deux notes montantes à la validation, deux notes graves en cas de rejet.
- « Institut Universitaire d'Abidjan » s'imprimait par défaut sur les cartes et les rapports de
  toute nouvelle installation. Le nom par défaut est « Mon établissement ».

### Modifié

- Documentation : projet personnel, bilan de recette signé par l'auteur seul, rappel des
  obligations de chaque utilisateur sur les données personnelles.

## [1.2.0] - 2026-11-04

### Modifié

- **Interface repensée :** identité « registre d'appel » (encre bleue sur papier, trait de
  surligneur jaune sur l'écran actif, le titre de la page et la zone de scan), chiffres et noms
  en Bahnschrift. L'indicateur de navigation glisse d'un écran à l'autre, les pages arrivent en
  fondu, les compteurs de l'accueil défilent jusqu'à leur valeur et les tuiles mènent à l'écran
  concerné. La zone de scan montre un viseur et une ligne de balayage quand la caméra lit, le
  dernier pointage s'allume à chaque décision, le cadre de la photo prend la couleur du résultat.
  Les animations s'arrêtent si Windows les a désactivées.
- **Textes :** libellés en casse normale, phrases complètes au lieu de fragments séparés par
  des tirets ou des points médians.

### Sécurité

- Pillow 12.3.0 passe en 13.0.0 : 39 vulnérabilités connues de décodage d'image corrigées.
  Pillow devient une dépendance directe (`pillow>=13.0`).
- Un identifiant inconnu se bloque comme un vrai compte : le message « bloqué » ne révèle plus
  quels comptes existent. Le blocage est enregistré en base (empreinte HMAC de l'identifiant,
  schéma version 4) et survit donc à un redémarrage de l'application.
- Frein global : 20 échecs en 10 minutes suspendent les connexions pendant une minute.
- Le changement de mot de passe est refusé pendant un blocage.
- Session revérifiée toutes les 30 secondes : un compte désactivé ou changé de rôle est déconnecté.
- Les hachages bcrypt plus faibles que la politique sont recalculés à la connexion.
- QR codes étrangers refusés avant la base ; jeton comparé en temps constant.
- Code de récupération exclu de l'historique et du nuage du presse-papiers de Windows.
- Copies déchiffrées dans un dossier temporaire au nom aléatoire ; fichier de clé en lecture
  réservée au propriétaire hors Windows.
- Import Excel borné pendant la lecture (lignes et colonnes).
- Les dialogues fermés sont détruits : un mot de passe saisi, le mot de passe provisoire ou le
  code de récupération ne restent plus en mémoire, dans une fenêtre cachée, jusqu'à la déconnexion.

### Corrigé

- Une restauration interrompue (disque plein, clé USB retirée) pouvait laisser l'application
  sans base. Les données actuelles sont désormais remises en place.
- Une erreur système pendant une restauration fermait l'application au lieu de rouvrir les données.
- L'import annonçait valides des lignes au matricule ou à la date de naissance refusés ensuite,
  ce qui annulait tout l'import.
- Export Excel puis PDF d'un rapport de 5 000 lignes : 21 s avant, 4,3 s après, sur le poste de test.
  Le PDF est découpé page par page au lieu d'un seul grand tableau.
- Changement de thème plus rapide (le style Fusion n'est plus recréé, la feuille de style ne
  vise plus chaque widget), et masqué par un fondu.
- L'écran Administration décompressait chaque sauvegarde à chaque affichage ; seul le manifeste
  est lu désormais.
- Une sauvegarde interrompue laissait un fichier partiel.
- Les fenêtres de séance ouvertes et l'avatar gardaient les couleurs de l'ancien thème.
- Plusieurs notifications s'empilaient au même endroit.

## [1.1.0] - 2026-10-16

### Ajouté

- **Aide intégrée :** bouton **Aide** et touche **F1**. L'aide de l'écran affiché, les
  raccourcis, la version, et l'accès au manuel, aux guides rapides et au dossier des données.
- **Documentation utilisateur :** guides rapides par rôle (administrateur, appel, secrétariat),
  questions fréquentes, historique des versions. Ils sont installés avec l'application et
  accessibles depuis le menu Démarrer.
- **Chiffrement au repos :** base SQLCipher (AES-256). Photos, justificatifs et sauvegardes
  en AES-256-GCM. La clé est protégée par Windows (DPAPI), et un code de récupération est
  remis à l'administrateur.
- **Comptes :**
  - politique de mots de passe avec règles affichées en direct ;
  - mots de passe provisoires générés, à changer à la première connexion ;
  - blocage progressif après 5 échecs, et déblocage par l'administrateur.
- **Session :**
  - verrouillage après inactivité (réglable) ou par **Ctrl+L** ;
  - ré-authentification pour les actions sensibles ;
  - une seule instance de l'application à la fois.
- **Journal scellé :** entrées chaînées par HMAC et tables d'audit en ajout seul. Un contrôle
  d'intégrité est affiché dans Administration → Sécurité.
- **Interface :**
  - thèmes clair et sombre (contrastes WCAG AA) ;
  - icônes, tableau de bord avec indicateurs et notifications discrètes ;
  - raccourci **Ctrl+F**.
- Vidéo de démonstration (`docs/video/smartpresence_demo.mp4`).

### Modifié

- Les bases, photos et justificatifs de la version 1.0 sont **chiffrés automatiquement** au
  premier lancement.
- Imports et exports contrôlés : noms validés, photos réencodées sans métadonnées, signatures
  de fichiers vérifiées, exports Excel sans formule.
- Dépendances figées (`requirements.lock`) et auditées (`pip-audit`).

## [1.0.0] - 2026-10-15

Première version, conforme au cahier des charges.

- Appel par scan de la carte (webcam ou lecteur USB) avec **vérification visuelle** de la
  photo : Entrée valide, Échap rejette et journalise.
- Gestion des étudiants, des photos, des filières, des classes, des cours, de l'emploi du
  temps et des comptes, avec quatre rôles.
- Import CSV/Excel vérifié ligne par ligne.
- Cartes étudiant en PDF avec QR code, et remplacement des cartes perdues.
- Rapports d'assiduité, alertes d'absences, fiche étudiant, exports Excel et PDF.
- Justification des absences avec pièce jointe.
- Sauvegarde quotidienne automatique, restauration vérifiée, journal des actions.
- Installateur Windows, manuel utilisateur, documentation technique et procès-verbal de recette.

[1.1.0]: https://github.com/samuelmardochee7-art/smartAPP/releases/tag/v1.1.0
[1.0.0]: https://github.com/samuelmardochee7-art/smartAPP/commit/5af5f2c
