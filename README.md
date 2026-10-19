# Maze Race

A maker for printable race mazes for two young kids (around age 5). One sheet, two players: one sits at the top
edge of the page and one at the bottom, each with their own coloured pen. Each starts at their own picture (two
mice, two bees, two rockets…) and races to the prize they both want in the middle (cheese, a flower, the moon…).
The sheets have no words, so they work for kids who can't read yet, and they're made for a black-and-white
printer. The answer is hidden in a QR code: scan it with a phone camera to watch both ways race to the middle.

Live at **https://tb-x.github.io/maze-race/**

## How it plays

- Print a sheet and lay it flat between two kids, one at each short end. Each start picture is turned to face
  its player.
- Each player colours the empty circle next to their picture with their pen, so everyone knows whose line is
  whose.
- On "go", both draw a line from their picture, through the gaps, to the prize in the room in the middle, without
  crossing a wall. First one there wins.
- It's a fair race: each player has a maze of their own, so the two ways never meet or share a corridor, and the
  two ways are the same length (or within a square or two on the biggest mazes).
- Each player's way is the only way through their half.
- Scan the QR code at the top right. The answer page draws both ways at the same speed, red from the top and
  blue from the bottom, and the prize hops when the first line gets there. Tap the maze to race again.

## The maker page

- **Size**: how many squares across, from Small (6) through Giant (18) up to Mega (24) and Monster (30) for big
  kids and grown-ups. How many rows the maze has depends on how much room there is on the page.
- **Pictures**: mice → cheese, bees → flower, rockets → moon, cars → house, bunnies → carrot, or A mix (each page
  gets different ones). Every picture is a black outline, so it can be coloured in.
- **Pages**: how many pages to print at once (up to 20), one race on each.
- **New races** makes new mazes for every page, ↻ at the bottom left of a page makes a new one for that page only, and **Print**
  prints them. Changing the pictures keeps the same mazes. The settings are remembered in this browser.
- Clicking a QR code on screen opens its answer page.

How the fair race is made: the room in the middle is fenced off, then two mazes grow at the same time, one from
each start, taking turns so they end up about the same size, and never breaking through into each other. Each
then gets one door into the room, picked so the two ways are as long as each other. The maker carves a few dozen
and keeps the fairest, longest one.

The QR code holds the whole maze in the link: its width and height, the top player's start column (the bottom
player's is the same, turned round), the room's size, the pictures, then every inner wall as one bit, 13 bits to
each 4 digits, e.g. `#8x8a0r2t4.0337776444…`. The digits go into the QR code in its numeric mode, which packs
them almost as tightly as raw bits. Nothing is stored anywhere, so a printed sheet keeps working for as long as
this page is online. The QR always points at the published page on GitHub Pages, even when the maker runs on a
local server.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5222
```

Then go to http://localhost:5222/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs. The
pictures are the same as [Maze Maker](https://tb-x.github.io/maze-maker/)'s.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | Medium, a mix, 1 page | Starting settings |
| `SIZES` | 6, 8, 11, 14, 18, 24, 30 across | The sizes in the Size list, and their names |
| `SHEETS_MAX` | 20 | Most pages printed at once |
| `MAX_CELL` | 26 mm | Widest corridor |
| `PIC_CELLS`, `PIC_MIN` / `PIC_MAX` | 1.7 squares, 20 / 30 mm | Size of the start pictures |
| `PEN` | 0.45 | Size of the circle to colour, as a share of the picture |
| `GOAL_MM` | 24 mm | Smallest goal room (always at least 2 × 2 squares) |
| `WALL` | 0.1 | Wall thickness, as a share of a square |
| `NEWEST` | 0.75 | 1 makes long winding corridors with few dead ends, 0 makes lots of short dead ends |
| `FAIR` | 0.06 | How much longer one way may be than the other (1 square is always fine) |
| `TRIES` | 60 | Most mazes carved for one race, keeping the fairest |
| `QR_SIZE` / `QR_MODULE` | 24 mm / 0.4 mm | Smallest answer QR code, and its smallest dot (big mazes get a bigger QR code) |
| `STEP_S` / `RACE_MAX_S` | 0.12 s / 9 s | Answer page: how fast the lines draw, and the longest a race takes |
| `PUBLIC_URL` | `https://tb-x.github.io/maze-race/` | Where the QR codes point |
