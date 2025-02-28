# GZDoom3DConveyorBelts
A technical demo of working 3D floor conveyor belts in GZDoom. ACS Scripts and the demo wad file.

## How to try this out?
This is a project based on the GZDoom source port of Id Software's 1993 video game Doom. To try this project out, you will need a working copy of Doom 2 ([Available for purchase e.g. at GOG](https://www.gog.com/en/game/doom_doom_ii)). Namely you will need the file DOOM2.WAD that comes with a copy of the game to run with GZDoom. Additionally you will require the latest stable version of [GZDoom](https://zdoom.org/downloads). This project was developed and tested with version g4.14.0. I also recommend grabbing the [Ultimate Doom Builder](https://github.com/UltimateDoomBuilder/UltimateDoomBuilder) or other Doom editing tool such as [Slade](https://slade.mancubus.net/index.php?page=downloads) to be able to muck about with the contents of the wad.

The .wad file included here entails a demo map, conveyor belt scripts included, where the concept and script can be experimented with. You can run the .wad file on a properly configured GZDoom executable or open it with Ultimate Doom Builder.

The scripts.acs file is here just as a more accessible version of the code for those without Doom mapping tools or the source port.

## So what exactly is this?

A little background. You may know that Doom is a "2.5 -D" game, meaning among other things that two floors can't exist in the game on top of each other. This limitation can be worked around with GZDoom or some other modern source ports by rendering solid 3D sectors into the map from dummy rooms outside the actual level geometry in a way that the dummy room's interiors become negative space inside the actual level geometry. Thus the player can, while moving in the actual game level, stand on the ceiling of the dummy sector that is represented in the level as a platform.

GZDoom also supports features from later Id software games, such as scrolling floors that move objects on top of it, creating a sort of conveyor belt effect. However, this conveyor belt effect has been impossible to combine with 3D sectors, as moving objects on top of the 3D platform would require scrolling objects along the scrolling ceiling of a room sector - a feature understandably unimplemented.

This script and demo map acts as a workaround, creating an illusion of a 3D floor moving objects along the scrolling of its textures. 

The scripting language ACS that GZDoom supports accepts three parameters that can be passed on from the map as it is played. The conveyor belt script takes as parameters the XYZ coordinates of the conveyor belt's start and end points (represented by map markers in the level layout) as well as the width of the conveyor belt. The script is activated by an game object touching on the ceiling of the dummy sector (3D platform in the level) and then continuously moves the objects in the correct direction while checking the object's XYZ coordinates to evaluate whether the object has moved outside the boundaries of the conveyor belt. The script takes into account the activating object's width, meaning that wider objects (larger demons) need to move farther to not be moved by the conveyor belt.

The script also takes into account the expected height of a conveyor belt traversing on the Z axis, meaning the player can jump (or rocket jump!) and not be moved by the moving platform while airborne.
