# Scénario de la vidéo de démonstration

Vidéo de SmartPresence 1.0.0 : `docs/video/smartpresence_demo.mp4` (1080p, 30 images par
seconde, voix off en français, sous-titres incrustés). Toutes les données présentées sont
**fictives**.

## Régénérer la vidéo

La vidéo est générée automatiquement à partir des vrais écrans de l'application, rendus sur la
base de démonstration, puis mis en scène : zooms sur l'élément commenté, carte présentée au
lecteur, touches Entrée et Échap, sons de l'application.

```powershell
.venv\Scripts\python -m pip install -r requirements-video.txt
```

```powershell
.venv\Scripts\python scripts\seed_demo.py --force
```

```powershell
.venv\Scripts\python scripts\video_demo.py
```

- **Voix off :** voix neuronale française `fr-FR-RemyMultilingualNeural`, obtenue avec edge-tts.
  Ce service de Microsoft est en ligne : seul le texte de la narration lui est envoyé. Les
  phrases sont mises en cache dans `build\video_cache` ; une nouvelle génération sans
  modification du texte se fait donc hors ligne.
- **Sons :** le bip de lecture, les deux notes de validation et les deux notes de rejet sont les
  sons de l'application.
- **Habillage :** l'identité « cahier d'appel » de l'application (papier, réglure, marge rouge,
  trait de surligneur jaune, titres en Bahnschrift).
- **Modifier la narration :** les phrases sont dans la fonction `scenario()` de
  `scripts/video_demo.py`. La durée de chaque plan s'adapte à la voix.

## Déroulé et narration

| Plan | Image | Voix off |
|---|---|---|
| Ouverture | Constats en grand, puis logo, « SmartPresence », « Version 1.0.0 » | « Dans beaucoup d'établissements, l'appel se fait encore sur papier. C'est long, et une carte d'étudiant peut se prêter. Voici SmartPresence, version un point zéro. » |
| 01 · Connexion | Écran de connexion, zoom sur le formulaire | « Chaque membre du personnel se connecte avec son propre compte. Après cinq mauvais mots de passe, le compte se bloque. » |
| 02 · Tableau de bord | Accueil de l'administrateur, zoom sur les tuiles et les alertes | « L'accueil résume la situation : les effectifs, les photos manquantes, les alertes d'absences. » |
| 03 · Ouverture de la séance | Écran Séances, puis la fenêtre « Ouvrir une séance » avec le créneau proposé | « Au début du cours, l'enseignant ouvre la séance, directement depuis l'emploi du temps. » |
| 04 · Scan de la carte | Fenêtre de la séance ; une carte glisse vers la zone de scan, un trait lumineux la lit, bip | « Chaque étudiant présente sa carte, à la webcam ou au lecteur USB. » |
| 05 · Vérification visuelle | Écran de vérification, zoom sur la photo et le tampon « À l'heure » ; touche **Entrée**, deux notes montantes | « Aussitôt, sa photo s'affiche en grand. C'est bien lui ? Touche Entrée : il est pointé. » |
| 05 · Mise à jour | Fenêtre de la séance, zoom sur les compteurs et la liste | « La liste et les compteurs se mettent à jour en temps réel, et les retards sont calculés automatiquement. » |
| 06 · Fraude n° 1 | La même carte est présentée à nouveau ; alerte « déjà pointé à 08:03 », deux notes graves | « Un camarade tente de réutiliser la même carte. SmartPresence l'arrête aussitôt : déjà pointé à huit heures trois. » |
| 07 · Fraude n° 2 | La carte d'une étudiante absente ; sa photo ne correspond pas ; touche **Échap**, deux notes graves | « Il présente maintenant la carte d'une étudiante absente. La photo ne correspond pas à la personne. Touche Échap : rien n'est enregistré. » |
| 07 · Signalement | Fenêtre de la séance : « 1 rejet » et le message de rejet | « Et la tentative est aussitôt signalée. » |
| 08 · Journal scellé | Administration → Journal des actions, actions sensibles | « La direction retrouve chaque tentative suspecte dans le journal. Il est scellé : toute modification est détectée. » |
| 09 · Données protégées | Administration → Sécurité | « La base, les photos et les sauvegardes sont chiffrées, et la clé est protégée par Windows. » |
| 10 · Cartes étudiant | Écran Cartes, zoom sur l'aperçu de la carte | « Le secrétariat imprime les cartes en PDF : dix cartes par page, avec photo et QR code. » |
| 11 · Rapports | Rapport par classe, puis le rapport exporté en PDF | « À la clôture, les absents sont comptés automatiquement. Les rapports d'assiduité sont prêts : par étudiant, par cours, par classe ou par mois. Et ils s'exportent en PDF ou en Excel, en un clic. » |
| Fin | Logo, « Version 1.0.0 », Scan · Vérification visuelle · Chiffrement · Rapports, contact de l'auteur, « données entièrement fictives » | « SmartPresence : des présences vérifiées, et la fraude bloquée. » |

## Tourner une version filmée

Le même déroulé peut servir à filmer une démonstration réelle, avec de vrais figurants.
Utilisez uniquement la base de démonstration, jamais de vraies photos d'étudiants.

1. Recréez la base de démonstration :

   ```powershell
   .venv\Scripts\python scripts\seed_demo.py --force
   ```

2. Imprimez deux cartes de `demo_data\cartes_demo.pdf` : celle de l'étudiant A et celle de
   l'étudiante C, de la même classe.
3. Choisissez deux figurants, A et B. Remplacez la photo de démonstration de A par celle du
   figurant A (écran Étudiants → Modifier → Choisir une photo), avec son accord.
4. Lancez l'application en enregistrant l'écran (Win+Alt+R ou OBS) :

   ```powershell
   $env:SMARTPRESENCE_HOME = "demo_data"; .venv\Scripts\python -m smartpresence
   ```

5. Suivez le tableau ci-dessus : A scanne sa carte et est validé ; B présente la carte de A
   (alerte « déjà pointé »), puis la carte de C (rejet par Échap).

Pour finir, affichez le contact de l'auteur et la mention « Données fictives ».
