# Star Border Animation (x86 Assembly)

A small 16-bit x86 assembly program that draws a border on the screen and animates a group of three stars moving around it. Built for the **Computer Organization and Assembly Language** course.

## Description

The program runs in DOS real mode and writes directly to text-mode video memory (`0xB800`). It:

1. Clears the screen (80x25 text mode).
2. Draws a border using `-` for the top and bottom edges and `|` for the left and right edges.
3. Animates three `*` characters travelling clockwise around the inside of the border:
   - **Phase 1:** left to right along the top
   - **Phase 2:** top to bottom along the right side
   - **Phase 3:** right to left along the bottom
   - **Phase 4:** bottom to top along the left side
4. Waits for a key press, then exits to DOS.

## Concepts Demonstrated

- Direct video memory access (`0xB800` segment, 2 bytes per character: character and attribute)
- Screen offset calculation: `offset = (row * 80 + column) * 2`
- Procedures with `call` / `ret`
- Loops, conditional jumps, and comparisons
- Stack usage (`push` / `pop`) to preserve registers
- Division (`div`) to extract row and column from an offset
- Software delay loops for animation timing
- BIOS keyboard interrupt (`int 0x16`) and DOS exit (`int 0x21`, function `4Ch`)

## Requirements

- [NASM](https://www.nasm.us/) (assembler)
- [DOSBox](https://www.dosbox.com/) (or any DOS emulator)

## How to Assemble and Run

1. Assemble the source into a `.com` file:

   ```
   nasm Star_Border_Animation.asm -f bin -o Star_Border_Animation.com
   ```

2. Open DOSBox, mount the folder that contains the file, and run it:

   ```
   mount c c:\your\folder
   c:
   Star_Border_Animation.com
   ```

3. Watch the animation, then press any key to exit.

> Replace `Star_Border_Animation.asm` with the actual name of your source file.

## Project Structure

```
.
├── Star_Border_Animation.asm      # Source code
├── README.md     # Project documentation
```

## Code Overview

| Label / Procedure | Purpose |
|-------------------|---------|
| `clrscr` | Fills video memory with spaces to clear the screen |
| `delay` | Nested loop that slows the animation |
| `start` | Main program: draws the border, then runs the animation |
| `phase1_right` | Moves the stars along the top edge |
| `phase2_down_loop` | Moves the stars down the right edge |
| `phase3_left_loop` | Moves the stars along the bottom edge |
| `phase4_up_loop` | Moves the stars up the left edge |
| `end_animation` | Waits for a key press and exits |

## Notes

- The animation speed depends on the CPU speed or the DOSBox cycle setting. To change it, adjust the values in the `delay` procedure.
- The program uses the `.com` format, so it starts at `org 0x100`.

## Author

Siraj U Din

BSCS FAST Student

## License

This project was created for educational purposes.
