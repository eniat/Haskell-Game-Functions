# Haskell Game Map and Player Utilities
A small Haskell project implementing core logic for a grid-based game world.

The project demonstrates functional programming through custom data types, pattern matching,
recursion, safe return types, file parsing and simple route calculation.

## Overview
The code models a 2D game map made from terrain tiles such as floors, walls, water and doors.
A player can be created, moved through the map, equipped with items and displayed through a
formatted status line.

The repository also includes text map files used for loading, rendering and validation tests.

## Features
- Represents a grid-based game map using Haskell algebraic data types.
- Supports floor, wall, water, open-door and closed-door terrain.
- Checks map width, height and coordinate bounds.
- Reads terrain at a coordinate using `Maybe` for invalid positions.
- Validates whether a tile is passable.
- Moves coordinates north, south, east and west.
- Returns successful or blocked movement using `Either`.
- Creates players with default health, position and equipment.
- Builds readable player status strings.
- Handles item pickup and one-item-per-slot replacement.
- Updates map tiles immutably.
- Opens and closes adjacent doors.
- Renders maps as ASCII grids.
- Loads maps from text files.
- Rejects invalid map characters.
- Calculates routes across passable tiles.
- Includes a lightweight built-in test harness.

## Technologies Used
- Haskell
- GHC / GHCi
- Functional programming
- Pattern matching
- Recursion
- Higher-order functions
- File I/O

## Repository Structure
```text
.
├── game_functions.hs
├── map1.txt
├── map2.txt
├── map3.txt
├── map4broken.txt
└── map5.txt
```

## Files
- `cwsub.hs` - main implementation, data types and built-in tests.
- `map1.txt` - small test map containing multiple terrain types.
- `map2.txt` - simple empty floor map.
- `map3.txt` - enclosed map with walls and water.
- `map4broken.txt` - invalid map used to test parser failure behaviour.
- `map5.txt` - larger map for manual loading, rendering and pathfinding checks.

## Terrain Format
Text maps use the following symbols:

| Character | Meaning |
|---|---|
| `.` | Floor |
| `#` | Wall |
| `~` | Water |
| `-` | Open door |
| `+` | Closed door |

Floors and open doors are passable. Walls, water, closed doors and out-of-bounds positions
are not passable.

## Core Data Types
```haskell
type Coord = (Int, Int)
data Dir = North | South | East | West
data DoorState = Open | Closed
data Terrain = Floor | Wall | Water | Door DoorState
data GameMap = GameMap [[Terrain]]
data Slot = Helm | Weapon | Armour | Boots
data Item = Item String Slot Int
data Player = Player String Coord Int [Item]
```

## How to Run
Install GHC if needed:

```bash
sudo apt update
sudo apt install ghc
```

Open the project in GHCi:

```bash
ghci cwsub.hs
```

Run all built-in tests:

```haskell
testAll
```

## Example Commands
```haskell
newPlayer "Ray"
isInBounds testMap1 (2, 3)
move testMap1 (2, 0) South
putStrLn (renderMap testMap1)
loadMap "map1.txt"
calculateRoute testMap2 (0, 0) (2, 2)
```

## Testing
The source file includes a built-in test harness. Run all tests with:

```haskell
testAll
```

The tests cover map dimensions, movement, bounds checks, player formatting, item pickup,
map updates, door toggling, rendering and file loading.

## Project Purpose
This project demonstrates practical Haskell development in a compact game-style problem.

It uses pure functions for most behaviour and avoids unsafe failure patterns by returning
`Maybe` or `Either` where operations may fail.

## Limitations
- Route calculation is not guaranteed to return the shortest path.
- The parser validates terrain characters but does not fully enforce rectangular maps.
- The test harness is lightweight and not a full Haskell testing framework.
- There is no interactive game loop or graphical interface.

## Skills Demonstrated
- Haskell type design.
- Functional decomposition.
- Recursive list processing.
- Safer error handling with `Maybe` and `Either`.
- Text-file parsing and rendering.
- Basic pathfinding logic.

- ## Usage Notice

This repository is provided for portfolio and review purposes only.

All rights are reserved. No permission is granted to copy, redistribute, submit, or reuse this work, in whole or in part, for academic coursework, assessment, or commercial purposes.

Where this repository relates to university coursework, it is shared only to demonstrate my own technical work and should not be used by other students as a submission or solution.
