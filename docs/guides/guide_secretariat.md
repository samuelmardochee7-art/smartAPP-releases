# Guide rapide du secrétariat et de la scolarité

Pour SmartPresence 1.0 : étudiants, photos, cartes, absences et rapports.

## Inscrire les étudiants

Pour inscrire toute une promotion (méthode conseillée), ouvrez l'écran **Étudiants**, puis
**Importer CSV / Excel…**

1. **Enregistrer un modèle CSV…**, puis ouvrez-le dans Excel.
2. Remplissez une ligne par étudiant : `matricule`, `nom`, `prenoms`, `classe` (nom exact de la
   classe dans SmartPresence) et, si possible, `date_naissance` (JJ/MM/AAAA) et `photo`.
3. Pour les photos, placez-les dans un dossier `photos` à côté du fichier, et indiquez
   `photos/nom_du_fichier.jpg` dans la colonne `photo`.
4. **Choisir un fichier…** : chaque ligne est vérifiée, **rien n'est encore enregistré**. Les
   lignes en rouge sont à corriger dans le fichier ; celles en gris existent déjà.
5. **Importer** enregistre uniquement les lignes correctes. Corrigez les autres et recommencez.

Pour un étudiant isolé : **Nouvel étudiant**, puis **Choisir une photo…**.

> **Pas de photo, pas de scan.** La photo permet au surveillant de reconnaître l'étudiant.
> Utilisez un portrait récent, de face, sur fond uni. L'Accueil indique combien d'étudiants
> n'en ont pas encore.

Le matricule ne se modifie pas, car il est imprimé dans le QR code. Un étudiant qui a quitté
l'établissement est **désactivé**, jamais supprimé.

## Imprimer les cartes

1. Écran **Cartes** → choisissez la classe.
2. **PDF de toute la liste**, ou sélectionnez des étudiants (Ctrl+clic) → **PDF de la sélection**.
3. Imprimez à **100 %**, sans « ajuster à la page » : une carte mesure 85,6 × 54 mm.
4. Découpez le long des traits de coupe. Une plastification protège la carte.

**Carte perdue ou volée :** sélectionnez l'étudiant → **Nouvelle carte (perte, vol)…**, puis
imprimez-la. L'ancienne carte est refusée dès le scan suivant.

## Justifier une absence

Écran **Absences** → période et classe → sélectionnez l'absence → **Justifier l'absence…**.
Saisissez le motif (certificat médical, convocation…) et joignez le document scanné, en PDF
ou en image. Il est enregistré chiffré.

## Sortir un rapport

Écran **Rapports** → choisissez la vue (par étudiant, cours, classe, mois, **alertes
d'absences**), la période et la classe → **Exporter en Excel…** ou **Exporter en PDF…**.
Double-cliquez sur un étudiant pour voir sa fiche séance par séance.

> Les fichiers exportés ne sont pas chiffrés. Rangez-les dans un dossier protégé et
> supprimez-les quand ils ne servent plus.

## Raccourcis

**F1** ouvre l'aide, **Ctrl+F** cherche dans la liste, **Ctrl+L** verrouille la session.
