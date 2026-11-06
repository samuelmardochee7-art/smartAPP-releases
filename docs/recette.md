# Bilan de recette de SmartPresence

SmartPresence est un projet personnel. Ce bilan compare l'application à son cahier des charges
(v1.0, section 10) et liste les contrôles qui restent à faire sur du vrai matériel.

| | |
|---|---|
| Date | 5 novembre 2026 |
| Version | 1.0.0 |
| Référence | Cahier des charges v1.0, section 10 |
| Environnement | Windows 11, Python 3.14.2, PySide6 6.12.0, SQLCipher 4.12.0, Pillow 13.0.0, OpenCV 5.0.0 |
| Tests automatisés | **287 réussis sur 287** : `.venv\Scripts\python -m pytest` (2 à 3 minutes selon la charge du poste) |
| Auto-vérification | `python -m smartpresence --verifier` réussie (chiffrement de la base, PDF, sauvegarde, décodeur QR) |
| Dépendances | 21 paquets figés (`requirements.lock`), aucune vulnérabilité connue (`pip-audit`) |

## 1. Critères de validation

| Critère (cahier des charges) | Seuil | Résultat | Preuve |
|---|---|---|---|
| Fonctionnalités indispensables (I) | 100 % testées et validées | ✅ F01 à F09 implémentées et testées | sections 2 et 3 |
| Lecture des cartes | ≥ 99 % en éclairage normal | ✅ En simulation : 200 QR codes imprimés sur 200 décodés à 300 dpi ; webcam simulée en conditions dégradées (inclinaison jusqu'à 20°, flou, bruit), au moins 95 % des images isolées lues et chaque carte lue en 3 images au plus. Avec une vraie webcam : lecture validée par l'auteur, taux non mesuré | `test_qr_imprime_se_lit_et_permet_le_pointage`, `test_taux_de_lecture_webcam` |
| Vérification anti-fraude | Aucune présence sans validation explicite ; 100 % des rejets journalisés | ✅ Le scan n'enregistre rien. Échap rejette et journalise. La croix de la fenêtre et une saisie parasite ne valident pas. L'aide au visage n'enregistre rien non plus | `test_scan_n_enregistre_rien_avant_validation`, `test_echap_rejette_et_journalise`, `test_aide_au_visage_affichee_seulement_pour_la_webcam` |
| Contrôles automatiques | Double scan, hors cours, photo manquante : 100 % détectés | ✅ | `test_rg01_*`, `test_rg02_*`, `test_rg03_*` |
| Performance | Identification < 2 s ; rapport < 10 s avec 5 000 étudiants | ✅ Identification : quelques millisecondes, plus environ 40 ms de décodage d'image. Rapports sur 5 000 étudiants et 120 000 présences : moins d'une seconde chacun. Export Excel puis PDF de 5 000 lignes : 4,3 s | `test_performance_5000_etudiants` |
| Sauvegarde | Aucune perte lors des tests de sauvegarde et de restauration | ✅ Restauration complète, sauvegarde de sécurité avant remplacement, archives altérées refusées, restauration interrompue remise en place | `test_restauration_*`, `test_sauvegarde_*` |
| Qualité | Aucune anomalie bloquante ou majeure non corrigée | ✅ Aucune anomalie connue non corrigée (section 1.1) | |
| Données personnelles (section 4) | Accès réservé aux personnes autorisées | ✅ Données chiffrées au repos, droits par rôle, comptes bloqués après 5 échecs, sessions verrouillées et revérifiées, anonymisation des anciens étudiants | `tests/test_securite.py`, `tests/test_ui_securite.py`, [securite.md](securite.md) |
| Journal des actions (F13) | Actions sensibles tracées | ✅ Journal en ajout seul, chaîné par HMAC : toute falsification est détectée | `test_journal_ni_modifiable_ni_supprimable`, `test_falsification_du_journal_detectee` |

### 1.1 Anomalies corrigées

| Anomalie | Gravité | Correction |
|---|---|---|
| Le bip de lecture ne s'entendait pas : l'application utilisait les sons système de Windows, très discrets avec certains modèles de sons | Majeure (F06 : signal sonore à chaque lecture) | L'application joue ses propres sons, nets et distincts |
| « Institut Universitaire d'Abidjan » s'imprimait par défaut sur les cartes et les rapports de toute nouvelle installation | Mineure | Nom demandé au premier lancement, « Mon établissement » par défaut |
| Une restauration interrompue pouvait laisser l'application sans base | Majeure | Données actuelles mises de côté et remises en place en cas d'échec |
| Export Excel puis PDF de 5 000 lignes en 21 s, au-delà du critère de 10 s | Majeure | Styles nommés pour Excel, PDF découpé page par page : 4,3 s |
| Pillow 12.3.0 avait 39 vulnérabilités connues | Majeure | Pillow 13.0.0 |
| Le message « compte bloqué » révélait quels identifiants existent | Mineure | Identifiants inconnus bloqués de la même façon, en base |
| L'import annulait tout pour une ligne refusée ensuite | Mineure | Mêmes contrôles dès l'analyse |

Ces anomalies ont été trouvées et corrigées pendant la recette, avant la publication de la version 1.0.0.

## 2. Scénarios de test clés (section 10)

| Scénario | Attendu | Résultat | Test |
|---|---|---|---|
| Carte d'un camarade | Rejet, aucun pointage, rejet journalisé | ✅ | `test_fraude_carte_d_un_camarade_rejetee_et_journalisee` |
| Même carte scannée deux fois | Alerte « déjà pointé à HH:MM » | ✅ | `test_rg01_double_scan_alerte_avec_heure` |
| Étudiant hors de son cours | Alerte ; seul l'enseignant du cours peut forcer | ✅ | `test_rg02_*`, `test_hors_cours_seul_l_enseignant_peut_forcer` |
| Étudiant sans photo | Validation refusée, pointage manuel proposé | ✅ | `test_rg03_*`, `test_seance_pointage_manuel_depuis_l_ecran_bloquant` |
| Pointage après la tolérance | Statut « retard » | ✅ | `test_rg04_*` |
| Clôture de séance | Les non-pointés deviennent absents | ✅ | `test_rg05_*`, `test_cloture_depuis_la_fenetre` |
| Fermeture brutale | Présences validées conservées | ✅ | `test_presence_validee_survit_a_une_fermeture_brutale` |

## 3. Couverture fonctionnelle

| Réf. | Fonctionnalité | Prio. | État |
|---|---|---|---|
| F01 à F09 | Authentification, étudiants, classes et cours, cartes, séances, scan, vérification, contrôles, retards et absences, pointage manuel, rapports | I | ✅ |
| F10 à F14 | Justifications, exports, alertes, journal, sauvegardes | S | ✅ |
| F15 | Tableau de bord graphique | O | ✅ |
| F16 | Notifications e-mail ou SMS | O | ❌ non réalisé, par choix |
| F17 | Comparaison faciale automatique | O | ✅ comme aide : une indication sur l'écran de vérification, jamais une décision |

## 4. Écarts par rapport au cahier des charges

Choix expliqués dans le [README](../README.md#écarts-par-rapport-au-cahier-des-charges-v10).

| Cahier des charges | Réalisation | Raison |
|---|---|---|
| Base locale SQLite | SQLCipher, c'est-à-dire SQLite chiffré (AES-256) | Protection des données en cas de vol du PC ou d'une sauvegarde |
| Lecture QR par OpenCV et pyzbar | OpenCV seul | Pas de DLL zbar à installer |
| Comparaison faciale avec face_recognition | Modèles YuNet et SFace d'OpenCV Zoo | face_recognition demande dlib, indisponible pour Python 3.14 ; OpenCV est déjà utilisé |
| QR code lié au matricule | QR code `SP-<matricule>-<jeton>` | Une carte remplacée est réellement invalidée (RG08) |
| Rôles administrateur, enseignant, secrétariat | Un rôle surveillant en plus | Seul l'enseignant du cours peut forcer un étudiant hors cours (RG02) |

## 5. Contrôles restants sur du vrai matériel

- [x] **Webcam réelle :** les cartes se lisent (contrôle de l'auteur).
- [ ] **Son :** réécouter le bip de lecture, la validation et le rejet.
- [ ] **Impression :** à 100 %, une carte mesure 85,6 × 54 mm à la règle ; le QR code est lisible par un téléphone.
- [ ] **Installateur :** installation, lancement et désinstallation de la 1.0.0 ; les données restent dans `%LOCALAPPDATA%\SmartPresence`.
- [ ] **Aide au visage :** un étudiant avec une vraie photo de vous, puis une lecture à la webcam ; la ressemblance doit être forte. Les photos de la démonstration sont des aplats sans visage : l'aide y indique « aucun visage net ».
- [ ] **Poste modeste :** un PC sous Windows 10 avec 4 Go de mémoire ; les écrans restent fluides et la police Bahnschrift s'affiche.
- [ ] **Animations désactivées :** avec Paramètres, Accessibilité, Effets visuels, « Effets d'animation » désactivé, l'application fonctionne sans animation.
- Lecteur USB : contrôle reporté, le lecteur USB est laissé de côté pour l'instant.

## 6. Données personnelles

SmartPresence est distribué comme un logiciel. La personne ou l'établissement qui l'utilise
avec de vraies données doit respecter la loi de son pays sur la protection des données
personnelles : information des étudiants sur l'usage de leur photo, durée de conservation,
formalités éventuelles auprès de l'autorité compétente. L'application fournit les moyens
techniques (chiffrement, droits, journal, anonymisation), pas ces démarches.

## 7. Décision

| Rôle | Nom | Décision | Date | Signature |
|---|---|---|---|---|
| Auteur | Avenié Kissi Samuel Mardochée | | | |
