# monop

[![Language](https://img.shields.io/badge/language-Macro10-blue.svg?style=plastic)](https://en.wikipedia.org/wiki/MACRO-10)
[![Build](https://img.shields.io/github/actions/workflow/status/nigeleke/monop/acceptance.yml?style=plastic)](https://github.com/nigeleke/monop/actions/workflows/acceptance.yml)
![Version](https://img.shields.io/github/v/tag/nigeleke/monop?style=plastic)

  [Site](https://nigeleke.github.io/monop) \| [GitHub](https://github.com/nigeleke/monop)

This is a nostalgic and dutifully typed in copy [1, 2] of a [Monopoly](https://en.wikipedia.org/wiki/Monopoly)-like program written in the summer of 1975 by myself and a school friend. It is written in [Macro-10](https://en.wikipedia.org/wiki/MACRO-10) and designed to run on a [PDP-10](https://en.wikipedia.org/wiki/PDP-10) if you happen to have one handy.

It's safe to say my friend and I were Monopoly fanatics, playing a dual board, figure of eight version of Monopoly every Saturday when we returned from our geek-out time at [Hatfield Polytechnic](https://en.wikipedia.org/wiki/University_of_Hertfordshire) (as it was then). We were privileged to have ample opportunity to use time on their DecSystem-10.

It's intended to reincarnate this on a [PiDP-10](https://hackaday.io/project/170111-pidp-10) as soon as the kit becomes publically available.

**This project is very likely absolutely no use to anyone at all in any way shape or form.**

|  | Hatfield Polytechnic |
|--|--|
| [1970](https://www.herts.ac.uk/about-us/the-history-of-our-university) | _"The best equipped and staffed Computer Centre in the public sector in education is formed, and, following the purchase of a DEC PDP-10 costing £256,500, the first multi-access computer system in education – linking schools, colleges and the Polytechnic – goes live."_ |
| 1975 | Two [Sir Fredric Osborn]() students getting told off by an operator because they'd printed out `monop.mac` on the line-printer. On telling the operator that they'd written it, he replied _"Oh, yes, I've written one too"_. We're yet to find it. |

## Development

Pre-requisite requires:

  1. Text editor of choice.
  2. [simh v4+](https://github.com/open-simh/simh); `make pdp10`
  3. [disk image](https://steubentech.com/~talon/pdp10/tops10-1.4.tar.bz2); Expand and copy `t10.dsk` to `./simh/disks/`

All source code compilation is performed on the simulator.

## Run Simulator

```
> cd simh
> <path_to_simh>/BIN/pdp10

PDP-10 simulator Open SIMH V4.1-0 Current        git commit id: c077c22d+uncommitted-changes
/home/nigel/Documents/monop/simh/pdp10.ini-3> attach rp0 disks/t10.dsk
%SIM-INFO: RP0: Amount of data in use in disk container 'disks/t10.dsk' cannot be determined, skipping autosizing
Logging to file "logs/pdp10.log"
BOOT V4(76)

BOOT>
[Loading from DSKB:SYSTEM.EXE[1,4]]

KS10 07-Oct-88
Why reload: NEW
Date: 
Time: 
Startup option: GO
[Rebuilding the system search list from the HOM blocks]

[Rebuilding the active swapping list from the HOM blocks]

[Rebuilding the system dump list from the HOM blocks]


KS10 14:08:40 CTY system 4097
Connected to Node CENTRA(0) Line # 42
.LOGIN 1,2
.R OPR

[CCPWFD Waiting for file daemon to start]
%%TTY STOMPER - Starting
OPR>
14:08:51          -- Message from the Accounting System --
                Account validation is not required

14:08:51        -- Begin auto take file --
                File: SYS:SYSTEM.CMD[1,4]

14:08:51        -- End auto take file --
                17 lines processed

OPR>EXIT
.
```

## Load & run source

Copy the complete content of `monop.mac` source code to the clipboard.

```
.R PIP
*MONOP.MAC=TTY:
<CTRL-SHIFT-V>
	TITLE   MONOP - MONOPOLY PLAYING PROGRAM
	SUBTTL  DEFINITIONS
	PRINTX  MONOP-DEFINITIONS
  ...
```
... and wait...

```
  ...
	PRINTX  MONOP-END OF PASS
  END     MONOP
<CTRL-Z>
*<CTRL-C>
.
.COMPILE MONOP.MAC /DLIST
.
.LOAD MONOP
LINK:   Loading

EXIT

.SAVE
MONOP saved
.RUN


MONOPOLY.
=========

WOULD YOU LIKE TO PLAY ?Y

PLEASE TYPE IN YOUR CHRISTIAN NAME: NIGEL
WOULD YOU LIKE SOME INSTRUCTIONS NIGEL ?Y

THIS PROGRAM ENABLES YOU TO HAVE A GAME OF MONOPOLY AGAINST ME.
TYPE ONE OF THE FOLLOWING INSTRUCTIONS EACH TIME `##` IS OUTPUT
BUY:    TO BUY HOUSES OR PROPERTY.
CASH:   TO FIND OUT HOW MUCH CASH YOU HAVE LEFT.
EXIT:   TO CREATE A CONTINUATION FILE AND EXIT.
GETOUT: TO GET OUT OF JAIL.
HELP:   TO OBTAIN A BRIEF SUMMARY OF THESE INSTRUCTIONS.
MORTGAGE:       TO MORTGAGE ANY OF YOUR PROPERTY.
PROPERTY:       TO FIND OUT WHAT PROPERTY YOU'VE GOT.
QUIT:   TO GIVE THE GAME TO ME.
RENT:   TO COLLECT RENT FROM ME.
        IN THE EVENT OF THROWING A DOUBLE I WILL GIVE YOU
        ABOUT TWO SECONDS TO TYPE 'RENT' IF I LAND ON YOUR PROPERTY.
SELL:   TO SELL HOUSES OR HOTELS (1 HOTEL=5 HOUSES)
STATE:  TO GET A LIST OF THE COMPLETE STATE OF THE BOARD.
THROW:  TO THROW THE DICE.
UNMORTGAGE:TO UNMORTGAGE ANY OF YOUR PROPERTY.
<CR>:   CARRIAGE RETURN WILL ALLOW ME TO HAVE MY GO.

IN ALL THESE INSTRUCTIONS ONLY THE FIRST TWO CHARACTERS WILL
BE RECOGNISED.

I SHALL START THIS GAME.
I'VE GOT $1500
I'VE THROWN 10 AND I AM NOW ON JUST VISITING JAIL

YOUR TURN. ## 

... some while later...

## THROW
YOU'VE THROWN 7 AND YOU ARE NOW ON FLEET STREET
THATS MY PROPERTY
RENT COLLECTED:- $1050

HARD LUCK NIGEL YOU HAVE JUST LOST.
I KNEW ALL THE TIME I COULD BEAT YOU.
I HOPE YOU ENJOYED THE GAME AND WILL PLAY WITH ME AGAIN SOMETIME ...
BE SEEING YOU
BYE BYE NIGEL

EXIT

.
```

## Acknowledgements

  * [PiDP-10 Google Groups](https://groups.google.com/g/pidp-10) for their support in getting the operating system up and running via simh, in particular [Clem Cole](https://groups.io/g/simh/topic/91528716). Note that much of the commentary around getting my source code loaded onto the PDP-10 suggested that mag-tape would be easiest, however I did not find a compatible combination of simulator, disk image or mag-tape format that worked. In the end I went the TTY: path. It is laborious (read slow) when loading changes, but it works.

## Notes

  1. The `.TITLE` was changed to `MONOP - ...` from the original `...` simply to make the `SAVE` command above save `MONOP.EXE` by default, rather than `MONOPO.EXE`.
  2. `<BEL>` characters were removed from outputted text as they were annoying - more so than in 1975!
