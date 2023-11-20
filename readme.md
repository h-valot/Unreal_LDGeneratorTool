Notion link: https://onahime.notion.site/UNREAL-LD-TOOL-1b5c23e97b704d3e83a713f27c0f3904?pvs=4

# ETUDE DE FAISABILITE

Est-ce que vous savez déjà comment vous allez faire ? Qu’est-ce qu’il vous manque ? Qu’est-ce que vous allez chercher ?

## INTERFACE

- Créer tool dans unreal sous forme de Editor Utility Widget
- Ajouter un switcher pour naviger entre “Perlin Noise 2D Map generator” et le “Random generator”
- Ajouter un bouton “Generate” et d’autre paramètre à l’aide d’un slider à ce widget
- Implémenter la fonctionnalité de la fonction de génération procédurale
- Dans un second temps, faire en sorte que ce bouton “Generate” soit accessible depuis la menu bar à l’aide d’un Editor Utility Blueprint

## FONCTIONNALITE

- Gérer la suppression de tous les actors d’une scène : avec Get All Actors Of Class (Actor)
- Gérer l’instantiation de actors dans la scène : choisir la classe générer de façon procedurale
- Faire en sorte que les objects soient les uns à la suite des autres : garde une yOffset qui s’incrémente de la taille de l’actor instantié, positionner les nouveaux actors à cette yOffset

## PROCEDURALITE

### RANDOM

- Gérer le choix de la classe à l’aide d’un random :

### PERLIN NOISE

- Générer un nomber “aléatoire” à l’aide d’un bruit de perlin 2d. Prendre la valeur abolue de cette valeur de bruit de perlin (actuellement comprise entre -1 et 1) puis la multiplié par le nombre d’actors différents et l’arrondir pour avoir un int compris entre 0 et le nombre d’actors différents
- (Coder la function Perlin Noise 2D en Blueprint car Unreal ne l’a pas fait)

## ACTORS LD BRICKS

- Faire des cubes de couleur de différente taille sans les scales → faire des assemblages de primitives de la taille de base

# DEFINITION DU PROCESSUS DE DEVELOPEMENT

Une fois le problème dégrossi le sujet, comment architecturer votre projet ?

## TOOL

### Tool/WBP_Level_Generator

VARIABLES

- int seed
- int scale
- int amplitude
- int lineSize
- int rowSize
- int xPos
- int yPos

WIDGET

- switcher tabs pour échanger entre la génération d’un terrain 2d à l’aide du bruit de perlin et de la génération à l’aide d’un simple random
- int slider field pour changer “seed”
- int slider field pour changer “scale”
- int slider field pour changer “amplitude”
- int slider field pour changer “lineSize”
- int slider field pour changer “rowSize”
- button “Generate” pour créer une nouvelle map

FUNCTION

- DestroyAllActorsOnScene

- GeneratePerlin2DMap
- GenerateBrickMap
- GetRandomHeightBrick
- CalculatePerlinNoise2D

- GenerateBrickMap
- GenerateRandomLevel
- GetRandomWidthBrick

### Tool/EBP_Level_Generator_Menu

- ajouter le blueprint widget à la main menu editor tool bar

## DATA

### Data/S_Level_Bricks

struct pour sauvegarder le template des data tables
- parent brick class

### Data/DT_Level_HeightBricks

stocke toutes les briques de 1x1 à 1x9

### Data/DT_Level_WidthBricks

stocke toutes les briques de 1x1 à 3x1

## LEVEL DESIGN

- empty parent brick
- child brick 1x1
- child brick 1x2
- child brick 1x3
- child brick 1x4
- child brick 1x5
- child brick 1x6
- child brick 1x7
- child brick 1x8
- child brick 1x9
- child brick 2x1
- child brick 3x1