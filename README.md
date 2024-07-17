# SUPER STR TRK BETA-6

### A simple text Star-Trek inspired game coded in Applesoft BASIC

#### WARNING: This game is in *beta*, so there may be bugs and/or missing features. If you notice an issue, please notify me with the "Issues" tab.

Hey guys! This is Super Str Trk, a simple passion project I spent about 30 minutes on and was made in [Applesoft BASIC](https://calormen.com/jsbasic/ "Applesoft BASIC Emulator"). (Read a little bit more about Applesoft BASIC from my other repository README, [here](https://github.com/EgamerCreations/APPLESOFT_BASIC/blob/main/README.md "My other Applesoft BASIC repository").)

To use this program, you take the old-school approach and type in **text commands**, e.g. "NAV". (There's no `split()` function in BASIC, so you can't even do something like "NAV 2 1", you have to do "NAV", then "2", then "1".) (You can view a list of commands below.) You can move, shoot, and dock while fighting Klingons, who are invading the solar system! There are 9 sectors, which you have to navigate through and destory the Klingons. The game is pretty easy, and very simple, but I built it. Also, you can only name variables with up to ***two letters***, so the variables are pretty... uh, scrambled and unobvious as to what they stand for at first glance. Here are some important ones, in case you want to remix/remake/experiment with the code. (If not, you can skip this.) By the way, the "$" indicates it's a **string**, and it doesn't count towards the name limit.

- **GI$**: General Input String. Used whenever you just need to store a user input (or any string) for a few lines of code. **It should never be used to store important data, or for a long amount of time.**
- **GN**: General Number. Same as **GI$**, but a) for numbers, and b) probably not as useful for user inputs. **It should never be used to store important data, or for a long amount of time.**
- **CO$**: Command. Stores the user command (e.g. "NAV", "SHE", "PHA".)
- **EN**: Energy. Stores the ship's energy as an integer value.
- **ME**: Max Energy. Stores the **max** amount of energy you can have.
- **KN**: Klingon Number. Stores the **initial** amount of Klingons.
- **KD**: Klingons Destroyed. Stores the amount of Klingons you've destroyed. (You can find the **current** amount of Klingons on the board by subtracting `kn - kd`)
- **KH**: Stores the active Klingon's health. (It resets every time you leave and come back to that Klingon; presumably, they fix themselves while you're gone.)
- **S1, S2, S3... S9**: Sector [number]. Stores the data of the respective sector. (10 means *one Klingon*, 1 means *one starbase*, 11 means *one starbase and one Klingon*, 0 means the sector is empty.)
- **ES**: Enterprise (ship) Sector. Stores the ship's current sector as an integer.
- **CS**: Course. Used only in the **NAV** command. Stores the ship's course as an integer (1 - 4).
- **WA**: Warp. Used only in the **NAV** command. Stores the ship's warp factor as an integer.
- **MW**: Max Warp. The max warp the ship can use.
- **CD**: Can Dock. Used only in the **DOK** command. Stores whether the player can dock in the current sector (1, 0).
- **DC**: Dock Cooldown. Stores the amount of stardates you have to wait until docking again.
- **ZC**: ihdk what this is supposed to stand for XD. This stores how many stardates it's been since you last docked. (You can calculate whether or not you can dock by taking `zc < dc`. If this returns `true`, you have to wait another few stardates to dock. You can find out how many stardates you have to wait by calculating `(dc - zc) + 1`)
- **SH**: Stores the amount of energy amounted in the shields.
- **LW**: LRS Working. Stores whether the LRS is online (1, 0).
- **SW**: SRS Working. Stores whether the SRS is online (1, 0).
- **SN$**: Ship Name. The ship's name.
- **NA$**: Name. Stores the player's name.
- **ME**: Stores the *max energy*. Different from `en`, which shows the *current energy*.
- **I**: Increment. Classic variable used for loops.

All of the other variables I either forgot what they were (lol) or they aren't really important or only show up once or twice.

#### Game Loop (again, for remixing or remaking code)


The (over-simplified) game loop looks something like this:

1. Ask user for difficulty, name, and ship name.
2. Initalize variables based on provided difficulty.
3. Display mission brief.
4. **Ask user for command.**
5. Execute command.
6. Check for win. If there is a win (all klingons destroyed, or `kd = kn`) then skip 7 and 8 and go to 9.
7. Check for loss. If there is a loss (klingons destroyed you, you ran out of energy, you ran out of time) then skip 8 and go to 10.
8. Go to 4.
9. Display win message.
10. Display appropriate loss message.
11. Ask user if they want to play again. If they answer "Y", then skip 12 and go to 1.
12. End game.

### Alright!


So now let's take a look at some **commands**. The first, **bold**, word, is the **root command**. This is the first command you will need to type. The other words, seperated by commas and in *italics*, are **arguments**. These are inputs you'll have to input after the root command. If there are no arguments, you don't need to type them in, and you just need to type the **root** to activate the command.


- **NAV**, *Course, Warp*: Moves your ship. A **course** of 1 is right. 2 is up; 3 is left, and 4 is down. **Warp** is how many sectors to move in that direction. How many sectors you can move is controlled by the `mw` variable in the code.
- **SRS**: Shows your immediate surroundings - that is to say, inside the sector you're currently in. A "K" is a Klingon ship, ! is a starbase, "E" is your ship, and an * is an empty space. (The placement doesn't matter - you can't move around *inside* the sector at all... *yet. ;)* )
- **LRS**: Shows each sector as a number. The tens digit (left number) is how many Klingons are in that sector; the ones digit (right number) is how many starbases are in that sector. Additionally, it'll show your position with a coordinate (x, y).
- **PHA**, *Power*: Shoots a Klingon in your sector with **power** energy (taken from the ship's total energy).
- **DOK**: Docks your ship at a starbase in your sector **IF** a) there is a starbase in your sector (duh), b) there are no Klingons in said sector, and c) enough stardates have past since your last docking (exactly how many is controlled by the `dc` variable in the code.) When your ship docks, it replenishes your health, energy, and systems. 
- **SHE**, *Power*: Adds/removes **power** from the Shields. Shields subtract damage from a Klingon phaser.
- **STAT**: Shows your ship's stats.
- **DAM**: Shows a list of systems and whether they're online (working) or not.


(I've provided *some* comments about what subroutines do what, but they're few and far between, so you'll probably just have to work things out on your own. Sorry :/)
