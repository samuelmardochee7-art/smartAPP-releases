# Guide rapide de l'administrateur

Pour SmartPresence 1.3, à garder près du poste d'administration. Le détail de chaque écran est
dans le manuel utilisateur.

## Mise en service (une seule fois)

1. **Installer :** lancez `SmartPresence-1.3.0-installation.exe`. Si Windows affiche
   « Windows a protégé votre ordinateur », cliquez sur « Informations complémentaires », puis
   « Exécuter quand même ».
2. **Créer votre compte administrateur :** il est demandé au premier lancement. Choisissez une
   phrase de passe d'au moins 10 caractères, par exemple `Kola-Lagune-Teck-47!`.
3. **Ranger le code de récupération :** il s'affiche juste après, en 14 groupes de 4
   caractères. Recopiez-le sur papier et rangez-le **sous clé, hors de l'ordinateur**. Sans ce
   code, une panne de Windows rend les données illisibles, définitivement.
4. **Régler les paramètres :** Administration → Paramètres. Renseignez le nom de
   l'établissement, le délai de tolérance des retards, le seuil d'alerte d'absences et le
   **dossier des sauvegardes**, de préférence sur un autre disque ou une clé USB.

## Préparer l'année

| Étape | Écran | Action |
|---|---|---|
| 1 | Classes | Créer les filières, puis les classes (année au format `2026-2027`) |
| 2 | Utilisateurs | Créer un compte par enseignant, surveillant et agent du secrétariat (**Générer un mot de passe sûr**) |
| 3 | Cours | Créer chaque cours (intitulé, classe, enseignant), puis **Ajouter un créneau** pour l'emploi du temps |
| 4 | Étudiants | Le secrétariat importe la liste (modèle CSV) et ajoute les photos |
| 5 | Cartes | Le secrétariat imprime les cartes à 100 % et les distribue |

L'Accueil signale les étudiants sans photo : ils ne peuvent pas être pointés par scan.

## Gérer les comptes

- **Nouveau compte :** le mot de passe provisoire s'affiche **une seule fois**. Remettez-le en
  main propre ; il devra être changé à la première connexion.
- **Mot de passe oublié :** sélectionnez le compte, puis **Réinitialiser le mot de passe**.
- **Compte bloqué** (5 essais erronés) : **Débloquer**.
- **Départ d'un membre du personnel :** **Activer / désactiver**. Le compte n'est jamais
  supprimé, pour que l'historique reste lisible.

## Routine conseillée

| Quand | Quoi |
|---|---|
| Chaque jour | Rien : la sauvegarde automatique se fait seule, une fois par jour |
| Chaque semaine | Rapports → **Alertes d'absences** ; Accueil : séances restées ouvertes |
| Chaque mois | Administration → Sécurité : le journal doit être **intègre** (pas d'alerte rouge) |
| Chaque mois | **Sauvegarder maintenant**, puis copier la sauvegarde sur une clé USB rangée ailleurs |
| Fin d'année | Désactiver les comptes des personnes parties ; exporter les rapports en PDF |

## En cas d'incident

| Situation | Action |
|---|---|
| Ordinateur en panne ou remplacé | Installer SmartPresence sur le nouveau PC, puis Administration → Sauvegardes → **Restaurer depuis un fichier…** avec la dernière sauvegarde et le **code de récupération** |
| Au démarrage, le code de récupération est demandé | Windows a été réinstallé ou les données ont changé de PC : saisissez le code |
| Alerte rouge « intégrité du journal » | Ne touchez à rien, gardez une copie du dossier `%LOCALAPPDATA%\SmartPresence` et prévenez la direction |
| Message « erreur imprévue » | Les données sont intactes. Transmettez le fichier `erreurs.log` à l'assistance (ci-dessous) |

**Assistance SmartPresence :** samuelmardochee7@gmail.com ou +225 01 72 75 57 07. Ne transmettez
jamais de mot de passe, le code de récupération ni des données d'étudiants.

## Raccourcis

**F1** ouvre l'aide, **Ctrl+F** lance une recherche, **Ctrl+L** verrouille la session.
