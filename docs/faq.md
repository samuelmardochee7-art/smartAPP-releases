# Questions fréquentes sur SmartPresence

Réponses courtes aux questions les plus posées. Pour le pas-à-pas, voir le manuel utilisateur
et les guides rapides. Dans l'application, la touche **F1** ouvre l'aide de l'écran affiché.

## Installation et démarrage

**Windows affiche « Windows a protégé votre ordinateur ».**
L'installateur n'est pas signé numériquement par un éditeur commercial. Cliquez sur
« Informations complémentaires », puis « Exécuter quand même ». Si vous avez téléchargé
l'installateur, vous pouvez vérifier qu'il est authentique grâce à son empreinte SHA-256,
publiée avec la version :

```
Get-FileHash .\SmartPresence-1.3.0-installation.exe
```

**Quel ordinateur faut-il ?**
Windows 10 ou 11 (64 bits), 4 Go de mémoire, une webcam ou un lecteur de QR codes USB, et
une imprimante pour les cartes.

**Où sont mes données ?**
Dans `%LOCALAPPDATA%\SmartPresence` : base, photos, justificatifs et sauvegardes
automatiques. Tout y est chiffré. Désinstaller ou mettre à jour SmartPresence n'y touche pas.

**Comment mettre à jour ?**
Lancez simplement l'installateur de la nouvelle version. Les données sont conservées et, si
besoin, mises à niveau au premier lancement. Faites une sauvegarde manuelle avant, par prudence.

**« SmartPresence est déjà ouvert ».**
Une seule fenêtre est autorisée par compte Windows. Cherchez l'icône dans la barre des tâches.

## Comptes et mots de passe

**J'ai oublié mon mot de passe.**
Demandez à l'administrateur : il vous donne un mot de passe provisoire, à changer à la
connexion suivante. Personne, pas même l'administrateur, ne peut lire votre mot de passe.

**L'administrateur a oublié le sien.**
Un second compte administrateur peut le réinitialiser. Prévoyez donc **deux comptes
administrateur**, détenus par deux personnes différentes.

**Mon compte est bloqué.**
Après 5 essais erronés, le compte est bloqué 5 minutes, puis plus longtemps si les erreurs
continuent. Attendez l'heure affichée, ou demandez à l'administrateur de le débloquer.

**Pourquoi mon mot de passe est-il refusé ?**
Il faut au moins 10 caractères et 3 types parmi minuscules, majuscules, chiffres et
symboles. Il ne doit contenir ni votre identifiant ni votre nom. Les règles se cochent en
direct pendant la saisie. Une courte phrase convient bien : `Mangue-Bleue-Lundi-8`.

**L'écran s'est verrouillé tout seul.**
C'est voulu : après quelques minutes sans activité, la session se verrouille pour protéger
les données. Saisissez votre mot de passe pour reprendre là où vous étiez.

## Appel et scan

**La webcam ne lit pas les cartes.**
Éclairez la carte, évitez les reflets, tenez-la à 15 à 25 cm et immobile une seconde. Si
l'ordinateur a plusieurs caméras, essayez « Webcam 2 ». Fermez Teams, Zoom ou tout logiciel
qui utilise déjà la caméra.

**Le lecteur USB écrit des caractères étranges.**
Le lecteur doit utiliser la disposition clavier du poste (AZERTY France). Elle se règle en
scannant un code de configuration fourni dans la notice du lecteur.

**J'ai validé par erreur (Entrée au lieu d'Échap).**
Ouvrez **Pointage manuel…** dans la séance et corrigez le statut, avec un motif. L'erreur et
sa correction restent tracées.

**Un étudiant a oublié sa carte.**
Vérifiez son identité, puis **Pointage manuel…**. Le motif « carte oubliée » est proposé.

**Pourquoi n'y a-t-il pas de reconnaissance faciale automatique ?**
C'est un choix : la comparaison du visage reste faite par une personne. Elle est plus
fiable dans une salle de cours et ne crée pas de données biométriques à protéger.

**J'ai oublié de clôturer la séance.**
Elle est clôturée automatiquement au prochain lancement de SmartPresence, après son heure de
fin. Les corrections restent possibles ensuite.

## Cartes

**Les cartes imprimées ne font pas la bonne taille.**
Dans la fenêtre d'impression, choisissez **Taille réelle** ou **100 %**, jamais « Ajuster ».
Une carte mesure 85,6 × 54 mm, comme une carte bancaire.

**Un étudiant a perdu sa carte.**
Écran **Cartes** → **Nouvelle carte (perte, vol)…**. L'ancienne carte est aussitôt refusée,
même si quelqu'un la retrouve.

**Une photo est floue ou ancienne.**
Écran **Étudiants** → **Modifier** → **Choisir une photo…**. Inutile de réimprimer la carte :
la photo affichée au scan vient de SmartPresence, pas de la carte.

## Sauvegardes et récupération

**Où trouver mon code de récupération ?**
Administration → Sécurité → **Afficher le code de récupération…** (votre mot de passe vous
est demandé). Le code doit aussi exister **sur papier, hors de l'ordinateur**.

**L'ordinateur est en panne. Ai-je perdu les données ?**
Non, si vous avez une sauvegarde et le code de récupération. Installez SmartPresence sur le
nouvel ordinateur, créez un compte administrateur provisoire, puis Administration →
Sauvegardes → **Restaurer depuis un fichier…**. Choisissez la sauvegarde et saisissez le code.
Gardez donc toujours une copie récente des sauvegardes **hors de l'ordinateur** (clé USB).

**J'ai perdu le code de récupération.**
Tant que l'ordinateur fonctionne, affichez-le à nouveau depuis Administration → Sécurité et
recopiez-le. Si l'ordinateur ne démarre plus et que le code est perdu, les données ne
peuvent pas être récupérées : c'est le prix d'un vrai chiffrement.

## Confidentialité

**Qui peut voir les photos et les présences ?**
Seuls les comptes SmartPresence, selon leur rôle. Un enseignant ne voit que les rapports de
ses cours. Hors de l'application, les fichiers sont chiffrés et illisibles.

**Les exports Excel et PDF sont-ils protégés ?**
Non : une fois exportés, ce sont des fichiers ordinaires. Rangez-les dans un dossier protégé
et supprimez-les quand ils ne servent plus.

## Obtenir de l'aide

1. Appuyez sur **F1** dans l'application, puis consultez ce document et le manuel.
2. Si le problème persiste, signalez-le à l'administrateur de SmartPresence de votre
   établissement, avec :
   - ce que vous faisiez, et le message exact affiché (une capture d'écran suffit) ;
   - la version, affichée dans l'aide (**F1**) ;
   - le fichier `erreurs.log` en cas de message « erreur imprévue ». **Aide** → **Ouvrir le
     dossier des données** l'affiche.
3. Si l'administrateur ne peut pas résoudre le problème, il contacte l'assistance
   SmartPresence : **samuelmardochee7@gmail.com** ou **+225 01 72 75 57 07**.

> **Ne communiquez jamais** votre mot de passe, le code de récupération, ni des noms ou
> photos d'étudiants, que ce soit dans un ticket, un e-mail ou une capture d'écran.
