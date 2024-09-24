# DnD 5e LaTeX Monster References

This is a LaTeX package for quickly generating page-correct references to monsters
for D&amp;D from various published sources.  It is designed to be used alongside
the [DnD 5e LaTeX Template](https://github.com/rpgtex/DND-5e-LaTeX-Template/).

The content of this package was generated from the 'Monsters' pane of the Dnd 5e
Complete Index, which [can be found here](https://docs.google.com/spreadsheets/d/1sccR7HgoHGB0Mq24k5K-O-tqJZG8D3Z66Ig7UloukNY/edit?usp=sharing).
At present it contains data from sometime in mid-2021 or so, but expect it to be
updated soon.

## Installation

There are three options for using this project; choose the one that's
right for you.

### User install using `TEXMFHOME` (recommended)

This will install the template for your current user in one of the following locations:

* Linux: `~/.texmf/tex/latex`
* OS X / macOS: `~/Library/texmf/tex/latex`
* Windows: `C:\Users\{username}\texmf\tex\latex`

LaTeX will find the package automatically.

1. Prepare your `TEXMFHOME` directory.

    ```sh
    mkdir "$(kpsewhich -var-value TEXMFHOME)/tex/latex/"
    ```

2. Download the [latest release](https://github.com/AlanQuatermain/DND-5e-LaTeX-monsters/releases/latest)
   and extract it in `$TEXMFHOME/tex/latex/`.

    ```sh
    wget https://github.com/rpgtex/DND-5e-LaTeX-Template/archive/main.zip
    unzip -d "$(kpsewhich -var-value TEXMFHOME)/tex/latex/" main.zip
    cd "$(kpsewhich -var-value TEXMFHOME)/tex/latex/"
    mv DND-5e-LaTeX-monster-main dnd
    ```

    Alternatively, clone the repo to the same location:

    ```sh
    git clone https://github.com/AlanQuatermain/DND-5e-LaTeX-monsters.git "$(kpsewhich -var-value TEXMFHOME)/tex/latex/dndmonsters"
    ```

### Using Overleaf

[Overleaf](https://overleaf.com) is an online TeX editor -- think
about it like Google Docs for TeX documents.  This option does not
require a local TeX installation and is an ideal approach for one-off
projects.

1. Download this GitHub repository as a ZIP archive using the *Clone
   or download* link above.
2. On Overleaf, click the *New Project* button and select *Upload
   Project*.  Upload the ZIP archive you downloaded from this
   repository.

### Project install using `TEXINPUTS`

You can also clone a copy of the repository to each LaTeX project. For example, to
clone the repository to a `lib/` directory in your project:

```sh
mkdir lib/
git clone https://github.com/rpgtex/DND-5e-LaTeX-Template.git lib/dnd
```

LaTeX will not find the template automatically. Set `TEXINPUTS` when compiling your
project to locate the package:

```sh
TEXINPUTS=./lib//: pdflatex project.tex
```

## Usage

To reference a monster from another publication, in almost all cases you need only
type its name, capitalized and preceded by `\Dnd`. For instance:

```tex
Hiding in the darkness of the deep water is a fearsome \DndAboleth.
```

This will yield:

> Hiding in the darnkness of the deep water is a fearsome **aboleth** (*MM*, p. 13).

### Capitalization

There are a few cases where you'll want to make some adjustments, however. Firstly,
you may want to have the monster's name capitalized, either because it's a proper
noun or because it's within a table of some kind. To achieve this, use the starred
version of the same command.

```tex
\begin{DndTable}{cX}
  d4 & Item \\
  1  & \DndWorg*
  2  & \DndHookHorror*
  3  & \DndFireGiant*
  4  & \DndHobgoblin*
\end{DndTable}
```

This will produce something similar to:

| d4   | Item                          |
| :--: | ----------------------------- |
| 1    | **Worg** (*MM* p. 341)        |
| 2    | **Hook horror** (*MM* p. 189) |
| 3    | **Fire giant** (*MM* p. 154)  |
| 4    | **Hobgoblin** (*MM* p. 186)   |

### Pluralization

Lastly, plurals are available by specifying an optional token stream to be appended
to the name portion of the output (within the bolded section):

```tex
Around the dining area are 7 \DndHobgoblin[s]\ at rest.
```

This produces:

> Around the dining area are 7 **hobgoblins** (*MM* p. 186) at rest.

## Options

The package accepts a variety of options to specify exactly what sources you'd like
to include.  There are separate options for each published source, and a few that
group several sources together.  You'll most likely want to use one of the latter,
and typically you'll want either `wotc` or `wotcbase` to use official sourcebooks
published by Wizards of the Coast.

### Groups

| Code       | Content                 |
| ---------- | ----------------------- |
| `wotc`     | All published sourcebooks from WotC. |
| `wotcbase` | As `wotc`, but without campaign setting sourcebooks. |
| `wotcadv`  | All adventures published by WotC. |
| `wotcmtg`  | WotC's Magic: The Gathering cross-over sourcebooks. |
| `wotcall`  | Everything published by WotC. |
| `eberron`  | All Eberron sourcebooks from WotC and Keith Baker. |
| `tpp`      | Third-party publishers: everything not from WotC. |
| `all`      | Literally everything. |

#### Base Wizards of the Coast Sources

The `wotcbase` option includes the following individual sources:

| Code     | Content  |
| -------- | -------- |
| `phb` | Player's Handbook (2014) |
| `dmg` | Dungeon Master's Guide (2014) |
| `mm` | Monster Manual (2014) |
| `mfolioI` | Mordenkainen's Fiendish Folio Vol. 1 |
| `mtof` | Mordenkainen's Tome of Foes |
| `vgtm` | Volo's Guide to Monsters |
| `xgte` | Xanathar's Guide to Everything |

#### Official Campaign Settings

The `wotc` option adds the following to the content of `wotcbase`:

| Code     | Content  |
| -------- | -------- |
| `erftlw` | Eberron: Rising from the Last War |
| `egtw` | Explorer's Guide to Wildemount |
| `gtr` | Guildmaster's Guide to Ravnica |
| `moot` | Mythic Oddyseys of Theros |

#### M:TG Crossover Settings

The `wotcmtg` option will add the Magic: The Gathering setting sourcebooks:

| Code     | Content  |
| -------- | -------- |
| `ggtr` | Guildmaster's Guide to Ravnica |
| `moot` | Mythic Oddyseys of Theros |


#### Official WotC Adventures

The `wotcadv` option grants access to all monsters from the published adventures.
You can also use `wotcall` to access `wotc` and `wotcadv` at the same time.

| Code     | Content  |
| -------- | -------- |
| `bgdia` | Baldur's Gate: Descent into Avernus |
| `cos` | Curse of Strahd |
| `gos` | Ghosts of Saltmarsh |
| `hotdq` | Hoard of the Dragon Queen |
| `oota` | Out of the Abyss |
| `pota` | Princes of the Apocalypse |
| `rot` | Rise of Tiamat |
| `ssa` | Lost Mines of Phandelver (starter adventure) |
| `skt` | Storm King's Thunder |
| `tftyp` | Tales from the Yawning Portal |
| `toa` | Tomb of Annihilation |
| `wdh` | Waterdeep: Dragon Heist |
| `wddotmm` | Waterdeep: Dungeon of the Mad Mage |

#### Everything Eberron

| Code     | Content  |
| -------- | -------- |
| `erftlw` | Eberron: Rising from the Last War |
| `ee` | Exploring Eberron |

#### Plane Shift (M:TG cross-over content)

| Code     | Content  |
| -------- | -------- |
| `psdom` | Plane Shift: Dominaria |
| `psinn` | Plane Shift: Innistrad |
| `psixa` | Plane Shift: Ixalan |
| `pskal` | Plane Shift: Kaladesh |

#### Third-Party Sourcebooks

| Code     | Content  |
| -------- | -------- |
| `cc` | Creature Codex |
| `fef` | Fifth Edition Foes |
| `lm` | Limitless Monsters |
| `tob` | Tome of Beasts |
| `toh` | Tome of Horrors |
| `tpkb` | Total Party Kill Bestiary |
| `ee` | Exploring Eberron |
