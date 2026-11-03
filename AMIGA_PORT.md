# Amiga port intake: Omnispeak

- Port Atlas: [g-omnispeak](https://www.amicradle.com/ports/#g-omnispeak)
- Priority: `P1`
- Atlas decision: `port`
- Upstream source: `https://github.com/sulix/omnispeak`
- Atlas source pin: `144f21e9891cd3df194df44bb0f2531c5dbc6bcb`
- Imported commit: `144f21e9891cd3df194df44bb0f2531c5dbc6bcb`
- Rights state: `review`

## Target contract

Primary target: AmigaOS 3.x / AmiCradle AC090 / Motorola 68040 + FPU.

Use the OPEN platform libraries where applicable: OpenGPU, OpenAudio/OpenAHI, OpenInput, OpenSocket and measured OpenMulticore work. Preserve a correct 68040 fallback and do not assume Roadshow.

No build, runtime, playability or release claim is made by this source-intake commit. Upstream submodules are not initialised. Original commercial game data remains external.

## Rights and data boundary

review; Confirm source/data licences before release.

## Build (AmigaOS 3.x, 68040 + FPU, on acsdl12)

    make -f amiga/Makefile.amigaos \
        STOVE=/path/to/openamigagcc-16.2.0-open4-x86_64-linux \
        NDK=/path/to/gfopensdk/OpenNDK/Include_H \
        ACSDL=/path/to/amicradle-guest/gameports/acsdl12

acsdl12 (amicradle-guest `gameports/acsdl12`) is SDL 1.2 on ACGame and AHI; it
needs its SDL_OpenAudio and threads. This gives `build/amigaos/Omnispeak/` with
the program and Omnispeak's episode files (`keen4/`, `keen5/`, `keen6e1*/`).
Put the program, one episode's Omnispeak files and that episode's own data
(`GAMEMAPS`, `AUDIO`, `EGAGRAPH`) in one drawer and run it there; it finds the
episode by itself. The game data is not in this repository.

Changes for the Amiga, all under `__amigaos__`: the program's drawer
(`PROGDIR:`) for the game and user files, with paths joined for a device name
and a writable test that tries a file; the sound process keeps the game's time
(`sd_sdl_audioSync`), at 22050 Hz; no overscan border, so the screen is 320x200.
And one fix for any big-endian machine: a font's header is read as id_ca.c
left it (in the machine's byte order), not as little-endian bytes again.

State (3 November 2026): in an AmiCradle lab instance (OpenKick ROM, 68040 +
FPU) with the Keen 4 shareware data, on AGA and RTG: the intro, title, menus,
a new game, the world map with music. Not yet: a level, saving, a real 68040.

