# SmartPresence

Application Windows de gestion des présences des étudiants par **scan de carte** (QR code),
avec **vérification visuelle anti-fraude**. Après chaque scan, la photo de l'étudiant
s'affiche en grand. Le surveillant la compare avec la personne présente, puis valide
(Entrée) ou rejette (Échap). Une carte prêtée à un camarade absent est ainsi repérée, et la
tentative est inscrite dans un journal infalsifiable. Toutes les données sont **chiffrées**.

> Projet personnel d'Avenié Kissi Samuel Mardochée, réalisé en 12 semaines.
> Version 1.3.0. Toutes les données et photos présentées sont **fictives**.

![Écran de vérification](docs/captures/clair_verification.png)

🎬 **Vidéo de démonstration** (1 min 30) : [`docs/video/smartpresence_demo.mp4`](docs/video/smartpresence_demo.mp4)

## Fonctionnalités

| | |
|---|---|
| **Appel en séance** | Ouverture depuis l'emploi du temps ; scan par **webcam** (OpenCV, dans un thread) ou **lecteur USB** ; suivi en temps réel ; clôture qui passe les non-pointés « absents » |
| **Anti-fraude** | Photo en grand et validation explicite. Un double scan, un étudiant hors cours, une photo manquante ou une carte remplacée sont bloqués. Garde-fous contre les validations involontaires ; chaque rejet est journalisé. À la webcam, une aide automatique compare le visage filmé à la photo (indication seulement, la décision reste humaine) |
| **Cartes étudiant** | PDF prêt à imprimer (85,6 × 54 mm, 10 par page A4). Une carte perdue est remplacée, et l'ancienne est refusée immédiatement |
| **Gestion** | Étudiants avec photos, import CSV/Excel vérifié ligne par ligne, filières, classes, cours, emploi du temps, comptes et rôles |
| **Rapports** | Assiduité par étudiant, cours, classe et mois ; alertes d'absences ; fiche individuelle ; exports **Excel et PDF** ; tableau de bord |
| **Absences** | Justification avec motif et pièce jointe (chiffrée) |
| **Données personnelles** | Anonymisation des anciens étudiants au-delà d'une durée de conservation réglable : identité, photo et pièces effacées, statistiques conservées |
| **Fiabilité** | Écriture immédiate en base (WAL), sauvegarde automatique quotidienne, restauration vérifiée |
| **Interface** | Identité « registre d'appel » : encre bleue sur papier, marge rouge et lignes de cahier, trait de surligneur jaune sur l'élément actif, statuts posés comme des tampons encreurs, libellés et grands chiffres en Bahnschrift lisibles de loin. Thèmes **clair et sombre** (contrastes WCAG AA), animations courtes qui répondent aux actions et respectent le réglage d'accessibilité de Windows, tableau de bord cliquable, raccourcis (Ctrl+F, Ctrl+L), **aide intégrée (F1)** |

## Sécurité

| | |
|---|---|
| **Chiffrement au repos** | Base **SQLCipher** (AES-256). Photos, justificatifs et sauvegardes en **AES-256-GCM**. Clé protégée par Windows (DPAPI) et code de récupération remis à l'administrateur |
| **Comptes** | bcrypt, politique de mots de passe, mot de passe provisoire à changer, **blocage progressif** après 5 échecs, temps de réponse constant |
| **Sessions** | Verrouillage automatique après inactivité, ré-authentification pour les actions sensibles, compte revérifié en cours de session, frein contre les essais en rafale, instance unique |
| **Journal** | Entrées **chaînées par HMAC** et tables d'audit en ajout seul : toute falsification est détectée |
| **Entrées** | Noms validés ; photos réencodées sans métadonnées ; signatures de fichiers contrôlées ; exports Excel sans formule ; données jamais interprétées comme du HTML ; archives de restauration contrôlées |
| **Dépendances** | Versions figées (`requirements.lock`) ; aucune vulnérabilité connue (`pip-audit`, 03/11/2026) |

Le détail, les menaces couvertes et les risques résiduels sont dans [docs/securite.md](docs/securite.md).

<details>
<summary>Captures d'écran (thème clair et thème sombre)</summary>

| Thème clair | Thème sombre |
|---|---|
| ![Connexion](docs/captures/clair_connexion.png) | ![Connexion](docs/captures/sombre_connexion.png) |
| ![Tableau de bord](docs/captures/clair_accueil.png) | ![Tableau de bord](docs/captures/sombre_accueil.png) |
| ![Séance en cours](docs/captures/clair_seance.png) | ![Séance en cours](docs/captures/sombre_seance.png) |
| ![Vérification](docs/captures/clair_verification.png) | ![Vérification](docs/captures/sombre_verification.png) |
| ![Étudiants](docs/captures/clair_etudiants.png) | ![Étudiants](docs/captures/sombre_etudiants.png) |
| ![Cartes](docs/captures/clair_cartes.png) | ![Cartes](docs/captures/sombre_cartes.png) |
| ![Rapports](docs/captures/clair_rapports.png) | ![Rapports](docs/captures/sombre_rapports.png) |
| ![Absences](docs/captures/clair_absences.png) | ![Absences](docs/captures/sombre_absences.png) |
| ![Utilisateurs](docs/captures/clair_utilisateurs.png) | ![Utilisateurs](docs/captures/sombre_utilisateurs.png) |
| ![Journal](docs/captures/clair_journal.png) | ![Journal](docs/captures/sombre_journal.png) |
| ![Sécurité](docs/captures/clair_administration.png) | ![Sécurité](docs/captures/sombre_administration.png) |
| ![Code de récupération](docs/captures/clair_code.png) | ![Session verrouillée](docs/captures/sombre_verrou.png) |
| ![Aide intégrée (F1)](docs/captures/clair_aide.png) | ![Aide intégrée (F1)](docs/captures/sombre_aide.png) |

<img src="docs/captures/carte_exemple.png" alt="Carte étudiant" width="420"> <img src="docs/captures/rapport_pdf.png" alt="Rapport PDF" width="420">
</details>

## Documentation

### Pour les utilisateurs

Dans l'application, **F1** (ou le bouton **Aide**) ouvre l'aide de l'écran affiché. Les
documents ci-dessous sont aussi installés avec l'application (menu Démarrer → SmartPresence →
Documentation).

| Document | Pour qui |
|---|---|
| [Guide rapide : faire l'appel](docs/guides/guide_appel.md) ([PDF](docs/guides/guide_appel.pdf)) | Enseignants, surveillants : une page à garder près du poste de scan |
| [Guide rapide : secrétariat](docs/guides/guide_secretariat.md) ([PDF](docs/guides/guide_secretariat.pdf)) | Secrétariat : import, photos, cartes, absences, rapports |
| [Guide rapide : administrateur](docs/guides/guide_administrateur.md) ([PDF](docs/guides/guide_administrateur.pdf)) | Mise en service, préparation de l'année, routine, incidents |
| [Questions fréquentes](docs/faq.md) ([PDF](docs/faq.pdf)) | Tout le monde |
| [Manuel utilisateur](docs/manuel_utilisateur.md) ([PDF](docs/manuel_utilisateur.pdf)) | Référence complète : installation, appel, rapports, sauvegardes, sécurité, dépannage |
| [Obtenir de l'aide](SUPPORT.md) | Signaler un problème ou poser une question |
| [Historique des versions](CHANGELOG.md) | Nouveautés de chaque version |

### Pour le projet

| Document | Contenu |
|---|---|
| [Sécurité](docs/securite.md) | Menaces, protections, preuves par les tests, risques résiduels |
| [Documentation technique](docs/documentation_technique.md) | Architecture, modèle de données, règles de gestion, tests, construction |
| [Bilan de recette](docs/recette.md) | Critères du cahier des charges, résultats et contrôles restants |
| [Scénario de la vidéo](docs/scenario_video.md) | Déroulé de la démonstration ; la vidéo est régénérable avec `scripts/video_demo.py` |

## Technologies

Python 3.11+, PySide6 (Qt), SQLCipher, cryptography, OpenCV, reportlab, openpyxl, bcrypt, PyInstaller et Inno Setup.

```
smartpresence/
├── ui/      Interface PySide6 : thème, écrans, scan (thread webcam), vérification, sécurité
├── core/    Logique métier : règles RG01 à RG08, rapports, cartes, sauvegardes, droits, audit
└── data/    Données chiffrées : SQLCipher, coffre de clés, fichiers chiffrés, migrations
tests/       287 tests automatisés (règles, sécurité, scan, rapports, performance, interface)
packaging/   PyInstaller et Inno Setup
scripts/     Données de démonstration, construction, manuel PDF, vidéo, icône
```

## Démarrage rapide (développement)

```bash
python -m venv .venv
```

```bash
.venv\Scripts\python -m pip install -r requirements.lock -r requirements-dev.txt
```

```bash
.venv\Scripts\python scripts\telecharger_modeles.py
```

Cette commande récupère les deux modèles de l'aide au visage (38 Mo, OpenCV Zoo, empreintes
vérifiées). Ils ne sont pas dans le dépôt ; sans eux, l'application fonctionne sans cette aide.

```bash
.venv\Scripts\python -m pytest
```

Pour créer la base de démonstration (90 étudiants fictifs, cartes PDF, 4 semaines d'historique) :

```bash
.venv\Scripts\python scripts\seed_demo.py --force
```

Pour lancer l'application sur cette base (PowerShell) :

```powershell
$env:SMARTPRESENCE_HOME = "demo_data"; .venv\Scripts\python -m smartpresence
```

Les comptes de démonstration sont `admin`, `bkouakou` et `rdiomande` (enseignants),
`pahoua` (surveillant) et `akone` (secrétariat). Leur mot de passe est la constante
`MOT_DE_PASSE_DEMO` de `scripts/seed_demo.py`.

## Construire l'installateur Windows

```powershell
powershell -ExecutionPolicy Bypass -File scripts\construire.ps1
```

Le script enchaîne les tests, PyInstaller, l'auto-vérification de l'exécutable, le manuel
PDF, puis l'installateur Inno Setup (si [Inno Setup 6](https://jrsoftware.org/isdl.php) est
installé). Résultat : `dist\SmartPresence-1.3.0-installation.exe`.

## Licence et contact

© 2026 Avenié Kissi Samuel Mardochée. **Tous droits réservés** : toute copie, modification
ou diffusion du code, de la documentation ou de l'application nécessite l'accord écrit de
l'auteur (voir [LICENSE](LICENSE)).

Contact et assistance : samuelmardochee7@gmail.com ou +225 01 72 75 57 07
(voir [SUPPORT.md](SUPPORT.md)).

## Écarts par rapport au cahier des charges v1.0

1. **QR code `SP-<matricule>-<jeton>`** : le jeton aléatoire permet d'invalider réellement
   une carte remplacée (RG08). Avec le matricule seul, l'ancienne carte resterait valide.
2. **Tables `inscription` et `creneau`** : cours suivis hors de sa classe, et emploi du
   temps (qui fournit l'heure de fin pour la clôture automatique).
3. **Rôles enseignant et surveillant séparés** : seul l'enseignant du cours peut forcer la
   validation d'un étudiant hors cours (RG02).
4. **Photos et justificatifs dans des dossiers chiffrés**, et non dans la base : les
   sauvegardes incluent ces dossiers.
5. **`presence_historique`** : chaque correction garde l'ancienne valeur, l'auteur et la date (RG06).
6. **Paramètre « exclure les absences justifiées »** du taux d'assiduité (RG07).
7. **Désactivation plutôt que suppression** dès qu'un historique existe (étudiant, cours,
   classe), pour ne pas fausser les rapports.
8. **OpenCV seul** pour lire les QR codes, au lieu de pyzbar : pas de DLL zbar à embarquer.
9. **Sécurité renforcée** au-delà du cahier des charges : chiffrement au repos, journal
   scellé, blocage des comptes, verrouillage de session (voir [docs/securite.md](docs/securite.md)).

La fonctionnalité optionnelle F17 (comparaison faciale) est réalisée comme une **aide** : elle
affiche une indication sur l'écran de vérification et ne décide jamais. Elle utilise les modèles
YuNet et SFace d'OpenCV Zoo plutôt que la bibliothèque face_recognition, qui demande dlib et
n'existe pas pour Python 3.14. F16 (notifications e-mail/SMS) n'est pas réalisée.

## Données personnelles

SmartPresence traite des données personnelles : identités et photos d'étudiants. La personne ou
l'établissement qui l'utilise avec de vraies données doit respecter la loi de son pays sur la
protection des données (information des étudiants, durée de conservation, éventuelles
formalités auprès de l'autorité compétente). L'application aide à le faire : données chiffrées,
accès par rôle, journal des actions, anonymisation des anciens étudiants (Administration,
onglet Sécurité). Les données de démonstration fournies sont entièrement fictives.
