# Scénario de la vidéo de démonstration (1 min 30)

La vidéo est générée automatiquement à partir des vrais écrans et des données fictives :
`docs/video/smartpresence_demo.mp4`. Pour la régénérer :

```powershell
.venv\Scripts\python scripts\seed_demo.py --force
```

```powershell
.venv\Scripts\python scripts\video_demo.py
```

Le scénario ci-dessous sert aussi à tourner une version filmée, avec de vrais figurants.

Objectif : montrer la fraude par substitution de carte bloquée par la vérification visuelle.
Utilisez uniquement la base de démonstration (données fictives), jamais de vraies photos.

**Préparation :**

1. Recréez la base de démonstration :

   ```powershell
   .venv\Scripts\python scripts\seed_demo.py --force
   ```

2. Imprimez deux cartes de `demo_data\cartes_demo.pdf` : celle de l'étudiant A et celle de
   l'étudiant B, de la même classe.
3. Choisissez deux figurants. Remplacez les photos de démonstration de A et B par les leurs
   (écran Étudiants → Modifier → Choisir une photo), avec leur accord.
4. Lancez l'application en enregistrant l'écran (Win+Alt+R ou OBS) :

   ```powershell
   $env:SMARTPRESENCE_HOME = "demo_data"; .venv\Scripts\python -m smartpresence
   ```

| Temps | Image | Commentaire (voix off ou sous-titres) |
|---|---|---|
| 0:00 à 0:10 | Logo, puis écran de connexion (compte enseignant) | « À l'université, l'appel papier est lent, et une carte peut être prêtée. » |
| 0:10 à 0:20 | Séances → Ouvrir une séance : créneau proposé, fenêtre de séance | « L'enseignant ouvre la séance en deux clics, depuis l'emploi du temps. » |
| 0:20 à 0:35 | A scanne sa carte à la webcam : photo en grand, « À L'HEURE », touche Entrée | « Chaque scan affiche la photo. Entrée : c'est bien lui, il est pointé. » |
| 0:35 à 0:55 | **B présente la carte de A** (déjà pointé) : alerte « Déjà pointé à 8 h 03 » | « Une carte ne sert qu'une fois par séance. » |
| 0:55 à 1:10 | **B présente la carte de C** (absent) : la photo de C ne correspond pas, touche Échap | « Le visage ne correspond pas : Échap. Rien n'est enregistré, et la tentative est journalisée. » |
| 1:10 à 1:20 | Compteur « 1 rejet », puis Administration → Journal, ligne rouge | « La direction voit chaque tentative suspecte. » |
| 1:20 à 1:30 | Clôture, puis Rapports → Par classe → export PDF | « À la clôture, les absents sont comptés. Les rapports sont prêts en un clic. » |

Pour finir, affichez le contact de l'auteur et la mention « Données fictives ».
