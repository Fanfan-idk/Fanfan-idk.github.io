# Guide d'installation Archipelago

Site officiel : https://archipelago.gg/ \
Discord principal : https://discord.gg/YN34tHmGGG \
Discord secondaire : https://discord.gg/VQkMugneDk \
Liste des jeux supportés : https://docs.google.com/spreadsheets/d/1iuzDTOAvdoNe8Ne8i461qGNucg5OuEoF-Ikqs8aUQZw/edit?gid=1086876441#gid=1086876441


## Fonctionnement d'Archipelago

### Principe général
Jouer une partie d'Archipelago revient à générer un **multiworld** à partir d'une configuration qui défini les jeux qui vont être joués et les joueurs qui vont jouer à ces jeux (grâce aux **fichier d'options YAML**). Le fichier généré est utilisé pour créer un serveur qui gère le multiworld. Le serveur peut être host sur le site d'Archipelago ou par un joueur sur son PC. Chacun des joueurs se connecte au serveur grâce au client Archipelago de son jeu (l'implémentation du client dépend de chaque jeu, c'est souvent un mod à installer, ou un launcher spécifique pour les émulateurs par exemple) et en renseignant son **slot**.  
Pendant la partie, chaque joueur qui atteint une **location** va, au lieu de débloquer quelque chose pour son jeu dans le gameplay normal, envoyer un **item** à un autre joueur sur un jeu différent.


### Glossaire

#### Multiworld 
Ensemble de **slots** et de leur **items**, **locations** et logique de progression. Un **multiworld** est généré pour chaque "run" d'Archipelago. La génération prend en compte les règles de progression et le **fichier d'option** de chaque jeux pou répartir les **items** de chaque jeu aléatoirement dans les **locations** disponibles, en s'assurant qu'il existe une suite logique d'unlocks permettant de finir tous les jeux.

#### Slot
Un **slot** correspond à une instance d'un jeu liée à un joueur dans le multiworld. Chaque slot est configuré par son **fichier d'options** (les fichiers YAML), qui défini le nom du **slot** (c'est à dire le joueur qui va jouer dessus) ainsi que la configuration du jeu associé (par exemple, modifier l'objectif final, les compétences débloquées, la manière de randomiser, etc). Lors de la génération, tous les fichiers YAML sont rassemblés et le générateur génère le **multiworld** à partir de ceux-ci.
Quand on lance la run, chaque joueur se connecte au serveur via son **slot**.

#### Item
Les **items** sont les éléments échangés entre les jeux. Cela peut être une pièce d'équipement, une augmentation de stats, une compétence, une clé, ou n'importe quoi d'autre qu'on peut obtenir dans le jeu.

#### Location
Les locations sont les endroits où sont normalement placé les **items** dans le jeu. Par exemple, un coffre, un drop d'ennemi ou un marchand. Cela peut également être finir un niveau, atteindre une cutscene ou débloquer un succès. Atteindre une **location** va généralement envoyer un **item** dans le multiworld pour un autre joueur.

#### Core/Custom Games
La liste des jeux disponibles est sur la google sheet en haut de page.
Les jeux indiqués comme "core" sont les jeux directement implémentés dans l'installation d'Archipelago. Les autres jeux sont dits "custom" et nécessitent une étape supplémentaire pour les configurer.


## Installation 

### Installation du launcher Archipelago
Le launcher Archipelago est un ensemble d'utilitaires permettant de générer, host et se connecter aux multiworlds, éditer les YAML, lancer des outils de visualisation pendant les runs, etc.

Lien du guide officiel : https://archipelago.gg/tutorial/Archipelago/setup_en

- Aller sur https://github.com/ArchipelagoMW/Archipelago/releases/tag/0.6.8
- Descendre tout en bas de la page et télécharger le Setup.Archipelago.X.X.X.exe
- Lancer l'exécutable et installer le launcher comme un programme classique

Le launcher contient plein d'éléments, mais les plus importants sont :
- **Install APWorld** : permet d'installer des outils supplémentaires et des jeux customs
- **Generate Template Options** : créer des fichiers d'options YAML par défaut pour tous les jeux installés
- **Text Client** : ouvrir une fenêtre textuelle qui permet de se connecter au serveur via un slot. Il affiche les événements qui se produisent pendant la partie (par exemple : *Joueur1* a envoyé *item* à *Joueur2*) et permet de lancer des commandes (listes des commandes : https://archipelago.gg/tutorial/Archipelago/commands_en)

Et pour gérer les multiworlds : 
- Generate : Génère un multiworld à partir des YAMLs
- Host : lancer le serveur à partir du fichier généré

### Setup du jeu

#### Installer le client Archipelago pour le jeu
Chaque jeu nécessite un client Archipelago qui va permettre de connecter le jeu au multiworld pour envoyer et recevoir les items. La plupart des jeux nécessitent également des mods pour s'adapter au mode randomizer. En général, les informations pour l'installation sont dans la colonne "Setup Guide" du google sheet contenant la liste des jeux. La colonne "Support" envoie vers le channel/thread du Discord Archipelago correspondant au jeu, il y a potentiellement plus d'infos là bas.

#### Ajouter un jeu custom au launcher Archipelago
/!\ Si le jeu n'est pas dans les core games (sinon, skip cette section) :
- Télécharger le fichier APWorld (généralement depuis le github, les liens sont sur le google sheet)
- Lancer le launcher Archipelago et sélectionner **Install APWorld**
- Sélectionner le fichier APWorld téléchargé; il va être installé et placé dans le dossier *custom_worlds*
- Depuis le launcher Archipelago également, lancer **Generate Template Options** : cela va générer les fichiers YAML de tous les jeux installés

#### Editer les options du jeu dans le YAML
Pour les core games, il est possible de générer les fichiers YAML directement depuis le site plutôt que de les éditer à la main :
- Aller sur la [liste des jeux](https://archipelago.gg/games)
- Sélectionner son jeu puis **Options Page**
- Entrer son nom (ce qui correspond au nom du slot), choisir les options puis cliquer sur **Export Options** en bas à gauche pour télécharger le ficher YAML.

Sinon, éditer le fichier YAML avec un éditeur de texte (genre notepad) :
- Depuis le dossier d'installation Archipelago, aller dans *Players*->*Templates*, copier le fichier YAML correspondant et ouvrir la copie pour la modifier.
- IMPORTANT : ne pas oublier de modifier la ligne "name" avec le nom de votre slot.
- Modifier le reste des options pour adapter le jeu (ou tout laisser par défaut, ça va fonctionner aussi)
- Une fois le fichier édité, il suffit de l'envoyer à la personne qui va générer le multiworld, il n'y a pas besoin de le conserver à un endroit spécifique.

### (BONUS) Installation de Universal Tracker et PopTracker
On verra plus tard

## Rejoindre un multiworld
Une fois que le host a lancé le serveur contenant le multiworld, les infos nécessaires à la connexion sont :
- adresse et port : Si le serveur est host manuellement, ça correspond à l'adresse IP de l'host et le port utilisé (38281 par défaut). Si le serveur est host sur le site, l'adresse est archipelago.gg et le port est donné sur la page de host.
- Slot name : le nom du slot renseigné dans le fichier YAML
- Mot de passe s'il est configuré

La méthode de connexion dépend du client de chaque jeu et nécessite de se référer au guide d'installation de chaque jeu. Certains vont ajouter un menu de connexion directement dans le jeu ou demander ces informations en option de lancement par exemple.
