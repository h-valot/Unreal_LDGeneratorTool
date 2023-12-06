[French translation on Notion](https://onahime.notion.site/UNREAL-LD-TOOL-1b5c23e97b704d3e83a713f27c0f3904?pvs=4)

# FEASIBILITY STUDY

Do you already know how you are going to do it? What are you missing? What are you going to look for?

## INTERFACE

- Create tool in Unreal as an Editor Utility Widget
- Add a switcher to navigate between “Perlin Noise 2D Map generator” and the “Random Map generator”
- Add a “Generate” button and other parameters using a slider to this widget
- Implement the functionality of the procedural generation function
- Secondly, ensure that this “Generate” button is accessible from the menu bar using an Editor Utility Blueprint

## FUNCTIONALITY

- Manage the deletion of all actors from a scene: with Get All Actors Of Class (Actor)
- Manage the instantiation of actors in the scene: choose the class to generate procedurally
- Ensure that the objects are one after the other: keep a yOffset which increments by the size of the instantaneous actor, position the new actors at this yOffset

## PROCEDURALITY

### RANDOM

- Manage the choice of class using a random:

### PERLIN NOISE

- Generate a “random” number using 2d perlin noise. Take the absolute value of this perlin noise value (currently between -1 and 1) then multiply it by the number of different actors and round it to have an int between 0 and the number of different actors
- (Code the Perlin Noise 2D function in Blueprint because Unreal did not do it)

## ACTORS LD BRICKS

- Make colored cubes of different sizes without scales → make assemblies of primitives of the base size

# DEFINITION OF THE DEVELOPMENT PROCESS

Once the problem has been sorted out, how can you architect your project?

## TOOL

### Tool/WBP_Level_Generator

#### VARIABLES

- int seed
- int scale
- int amplitude
- int lineSize
- int rowSize
- int xPos
- int yPos

#### WIDGET

- switcher tabs to switch between the 2d land generator based on perlin noise and 1d land generator based on a random seed 
- int slider field to change “seed”
- int slider field to change “scale”
- int slider field to change “amplitude”
- int slider field to change “lineSize”
- int slider field to change “rowSize”
- button “Generate” to create a new map

#### FUNCTION

- DestroyAllActorsOnScene
- GeneratePerlin2DMap
- GenerateBrickMap
- GetRandomHeightBrick
- CalculatePerlinNoise2D
- GenerateBrickMap
- GenerateRandomLevel
- GetRandomWidthBrick

### Tool/EBP_Level_Generator_Menu

- add a blueprint widget in the main menu editor tool bar

## DATA

### Data/S_Level_Bricks

struct to save data table template
- parent brick class

### Data/DT_Level_HeightBricks

store all bricks from 1x1 to 1x9

### Data/DT_Level_WidthBricks

store all bricks from 1x1 to 3x1

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
