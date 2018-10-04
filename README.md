# MineFriff - A Blocky Esolang
**MineFriff** brings the joy of traditional esolangs such as `Befunge` and `><>` into the blocky pixelated world of _Minecraft_.  Much like fungeoid languages, MineFriff allows code to be set out in a 2D code area, which can range from a 100*100 grid (allowing for 10,000 instructions) to any size of square (or cube).

As aforementioned, MineFriff allows for free-form code to be written in any size cube (meaning that 3D code is allowed).

**MineFriff** comes in three flavours: Strict, Freeform and Textual. _Strict_ MineFriff is contained in a 100 by 100 block grid, and can be exported to a `.mf` file. However, strict MineFriff is only avaliable in the offical MineFriff interpreter world. _Freeform_ MineFriff is avaliable in any world, but is unexportable to an actual file -- code is run using.
```
/py MineFriff
```

_Textual_ MineFriff is a text based ascii version of the blocky esolang, which is avaliable to everyone -- all one needs is the python based MineFriff interpreter.

## Concepts
### Code Box
Like most fungeoidal esolangs, MineFriff has a code box in which the program is placed. In strict MineFriff, this code box is as shown:

![100 * 100 block code grid]()

In freeform MineFriff, this code box is essentially non-existant; programs can take any form they want and can be even 3d.

In textual MineFriff, the code box spans an infinite amount of space, both vertically and horizontally.

### Instruction Pointer (IP)
The _instruction pointer_ is what drives the interpreting of MineFriff programs. It starts in the top left corner of the program (strict and textual) or wherever the player is standing in freeform. It can move left, right, up, down, and in the case of freeform MineFriff, up layers and down layers. In strict MineFriff, when the IP reaches the edge of the code box, the IP "wraps around" to the other side (e.g. if it reaches the far right side, it will go to the far left side and continue). This doesn't in happen in freeform MineFriff, as there isn't any code box to wrap around. This functionality is being worked on for textual MineFriff.

### The Temporary Register
Rather than having literals pushed directly onto the stack, MineFriff has a _temporary register_ (temp reg) in which literals are constructed. This allows for any value to be created without having to worry about impacting the stack. The temp reg can be treated as either an `int`eger, a `char`acter or a `float`.

### The Stack
The stack in MineFriff is like the stack in most other fungeoids -- it can have values pushed to it, it can have stack operations performed, it can be shifted left and right -- all of the usual stuff. However, when popping values from the stack, they are placed back into the temp reg (hence, overwriting the current value), rather than deleted into nowhere.

## Instructions
|                                                 Command                                                |       Symbol       |  Minecraft Block Equivalent |
|:------------------------------------------------------------------------------------------------------:|:------------------:|:---------------------------:|
| Move the IP left.                                                                                      |         `<`        | Oak Wood Planks             |
| Move the IP right.                                                                                     |         `>`        | Spruce Wood Planks          |
| Move the IP up.                                                                                        |         `^`        | Birch Wood Planks           |
| Move the IP down.                                                                                      |         `v`        | Jungle Wood Planks          |
| Print the top value on the stack.                                                                      |         `o`        | Sponge                      |
| Add a literal to the temp reg.                                                                         | `0123456789abcdef` | Wool (Data gives the value) |
| Reverse the contents of the stack.                                                                     |         `r`        | Netherrack                  |
| Push the temp reg onto the stack and reset it to 0.                                                    |         `,`        | Piston                      |
| Pop the top item from the stack and place it in the temp reg.                                          |         `.`        | Sticky Piston               |
| Push the length of the stack onto the stack.                                                           |         `l`        | Stone                       |
| Pop `x` and `y` off the stack. Push `y == x` back on (1 if true, 0 if false).                          |         `=`        | Bedrock                     |
| Duplicate the top item of the stack.                                                                   |         `:`        | Hopper                      |
| Swap the top two items of the stack.                                                                   |         `$`        | Obsidian                    |
| Skip the next instruction (trampoline).                                                                |         `#`        | Slime Block                 |
| Pop the top value from the stack and skip the next instruction if it is zero (conditional trampoline). |         `?`        | Redstone Lamp (off)         |
| End the program                                                                                        |         `;`        | Glass Block                 |
| Pop `x` and `y` off the stack. Push `y > x` back on (1 if true, 0 if false).                           |         `)`        | Diamond Block               |
| Pop `x` and `y` off the stack. Push `y < x` back on (1 if true, 0 if false).                           |         `(`        | Coal Block                  |
| Pop `x` and `y` off the stack. Push `y * x` back on.                                                   |         `*`        | Podzol                      |
| Pop `x` and `y` off the stack. Push `y / x` back on.                                                   |         `/`        | Diorite (raw)               |
| Pop `x` and `y` off the stack. Push `y + x` back on.                                                   |         `+`        | Andesite (raw)              |
| Pop `x` and `y` off the stack. Push `y - x` back on.                                                   |         `-`        | Granite (raw)               |
| Change the direction of the IP to a random direction.                                                  |         `x`        | Dispenser                   |
| Go back to the start of the current line in the same direction.                                        |         `~`        | Hay Block                   |
| Go to the start of the next line.                                                                      |        `\``        | End Bricks                  |
| Treat the temp reg as an integer.                                                                      |         `I`        | Packed Ice                  |
| Treat the temp reg as a character.                                                                     |         `C`        | Birch Wood                  |
| Treat the temp reg as a float.                                                                         |         `F`        | Furnace                     |
| Right shift the stack by 1.                                                                            |         `]`        | Dirt Block                  |
| Left shift the stack by 1.                                                                             |         `[`        | Cobblestone                 |
| Pop `x` and `y` off the stack. Push `y % x` back on.                                                   |         `%`        | Sand (normal)               |


