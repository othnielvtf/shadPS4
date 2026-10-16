<!--
SPDX-FileCopyrightText: 2026 shadPS4 Emulator Project
SPDX-License-Identifier: GPL-2.0-or-later
-->

# shadPS4 — Development Fork

> [!IMPORTANT]
> **For development, debugging, and experimental testing only.**
> This is a personal, unofficial fork of [shadPS4](https://github.com/shadps4-emu/shadPS4),
> maintained to investigate macOS compatibility issues and prepare potential upstream contributions.
> It is not an official shadPS4 release or a stable end-user distribution.

**Full credit for the original project goes to the shadPS4 team and its contributors.**
All rights to the original code, project name, logos, games, and third-party assets remain
with their respective copyright and trademark owners. This fork does not claim ownership
of the upstream project or imply endorsement by its maintainers.

[Original project](https://github.com/shadps4-emu/shadPS4) ·
[Official website](https://shadps4.net/) ·
[Upstream contributors](https://github.com/shadps4-emu/shadPS4/graphs/contributors) ·
[License](LICENSE)

## Purpose

This repository is a workspace for investigating crashes, testing changes, and preparing
small, reviewable fixes for shadPS4. Current work focuses on Apple Silicon Macs running
the x86_64 emulator through Rosetta:

- Emit standard NOP sequences when relocating guest code.
- Work around affected 256-bit AVX stores under Rosetta.
- Retain existing macOS memory reservations during optimized linking.

Cuphead is a reproduction and testing case for these emulator changes. This is not a
Cuphead source-code project, and the fixes do not special-case the game.

## Branches

| Branch | Contents |
| --- | --- |
| [`main`](https://github.com/othnielvtf/shadPS4/tree/main) | Latest checked upstream baseline plus all three experimental macOS fixes and this fork's development README. |
| [`fix/canonical-relocated-nops`](https://github.com/othnielvtf/shadPS4/tree/fix/canonical-relocated-nops) | Independent NOP relocation fix. |
| [`fix/macos-reserved-sections`](https://github.com/othnielvtf/shadPS4/tree/fix/macos-reserved-sections) | Independent macOS reservation retention fix. |
| [`fix/rosetta-avx-stores`](https://github.com/othnielvtf/shadPS4/tree/fix/rosetta-avx-stores) | AVX store workaround, based on the NOP fix. |
| [`macos-cuphead-tested`](https://github.com/othnielvtf/shadPS4/tree/macos-cuphead-tested) | All three fixes combined; source used for local gameplay validation. |

The focused fix branches are kept separate from this fork-specific README for upstream review.

## Validation and limitations

The combined changes were built locally for macOS x86_64 in Release mode with ThinLTO.
Testing used an Apple M5 Pro running macOS 26.6.2 and Cuphead CUSA20499, base version 1.00.

Opening gameplay checks covered the title screen, save loading, map movement, Forest Follies,
shooting, jumping, damage, death, retry, the game's pause menu, and returning to the map.

- The whole game, updates, and DLC have not been tested.
- The separate fix branches have not each been validated as standalone full game builds.
- Observed FPS samples around 40–60 are not a controlled benchmark or a claimed speed increase.
- One diagnostic run stalled after repeated emulator F9 pause/resume. A fresh run using the
  game's normal pause menu returned to the map successfully; the earlier stall's cause is unproven.
- Instruction probes were run on macOS. The prepared OpenOrbis test sources have not been
  built or run on PS4 hardware.

These results describe this experimental fork and do not establish official upstream compatibility.

## Development resources

Start with the original project's documentation:

- [macOS build instructions](https://github.com/shadps4-emu/shadPS4/blob/main/documents/building-macos.md)
- [Debugging and reporting issues](https://github.com/shadps4-emu/shadPS4/blob/main/documents/Debugging/Debugging.md)
- [Contribution guidelines](https://github.com/shadps4-emu/shadPS4/blob/main/CONTRIBUTING.md)
- [Official game compatibility tracker](https://github.com/shadps4-compatibility/shadps4-game-compatibility)

For normal emulator use, refer to the [official QtLauncher releases](https://github.com/shadps4-emu/shadps4-qtlauncher/releases)
and [upstream quick start](https://github.com/shadps4-emu/shadPS4/wiki/I.-Quick-start-%5BUsers%5D).

AI assistance was used for implementation, analysis, and local testing of the experimental
changes. Any upstream submission must follow the project's requirements for disclosure,
human review, understanding of the code, and human-written PR descriptions.

## Credits and ownership

shadPS4 is the work of the [upstream shadPS4 team](https://github.com/shadps4-emu/shadPS4#main-team)
and [all project contributors](https://github.com/shadps4-emu/shadPS4/graphs/contributors).
The original shadPS4 logo is credited upstream to [Xphalnos](https://github.com/Xphalnos).

The upstream project also acknowledges Panda3DS, fpPS4, yuzu, felix86, and emudev.org.
See the [original acknowledgements](https://github.com/shadps4-emu/shadPS4#special-thanks),
[third-party license files](LICENSES), and notices accompanying dependencies in [`externals`](externals).

Games, firmware, names, trademarks, and third-party assets belong to their respective owners.
No ownership of those materials is claimed by this fork.

## License

The existing shadPS4 copyright notices and **GPL-2.0-or-later** licensing remain in place.
See [LICENSE](LICENSE), the source-file headers, and individual dependency notices for the
applicable terms. All rights remain with the respective rights holders, subject to those licenses.

The development-only notice describes this fork's intended purpose; it does not change
the rights granted by the existing licenses.
