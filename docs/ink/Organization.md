# File Directory Structure

It helps to break apart a complex script into separate ink files by location, time, and character/object. 
- Locations should be directly accessible by either their parent location (a hotel on main street) or a sibling location (the lobby and main hall in a hotel)
- A daytime directory contains ink scripts for location, character, and object interactions available during the day at the parent location
- A character or object file describes all interactions that can be made with that character or object in the parent location/time directory

It may also help to start with a [Mind Map chart](https://mm.tt/1281196741?t=4MDoVGC64f) to get a sense of how deeply nested your scripts will be:

![mindmap](img/FileMap.png)


## File Includes

Inside each directory, include a `_Main.ink` file that holds everything together. For example,

### Chapter-01/ _Main.ink
Top level locations for the game as of `Chapter 1`. Interactions that might occur anywhere are also included in the `Shared` directory.

```ink
INCLUDE Town/_Main.ink
INCLUDE Forest/_Main.ink
INCLUDE Cottage/_Main.ink
INCLUDE Shared/_Main.ink

```

### Chapter-01/ Town/ _Main.ink
All top-level locations that exist inside of the `Town` location.

```ink
INCLUDE MainStreet/_Main.ink
INCLUDE BackAlley/_Main.ink
INCLUDE TownCenter/_Main.ink

```

### Chapter-01/ Town/ TownCenter/ _Main.ink
Some `TownCenter` locations, characters, and objects may only be available during certain hours or conditions. Some might exist during both times, but with different dialogue and/or positions.

```ink
INCLUDE Day/_Main.ink
INCLUDE Night/_Main.ink
INCLUDE Always/_Main.ink
INCLUDE Event/_Main.ink

```

### Chapter-01/ Town/ TownCenter/ Always/ _Main.ink
These locations, characters, and objects are `always` accessible in `TownCenter`. It is still possible for some of these to have different dialogue/positions based on time.

```ink
INCLUDE TownHall/_Main.ink
INCLUDE Hotel/_Main.ink
INCLUDE Fountain.ink
INCLUDE Watchdog.ink

```

## Note

No matter how your INK files are organized, you can jump from any script to any other script as long as:
- All relevant script files are included in the project
- The line you want to `divert` to has a unique label within its `scope` (see [Basics/Scopes](Basics.md#Scopes))
- You reference the correct label in your `divert` (see [Basics/Diverts](Basics.md#Diverts))
