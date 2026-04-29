# codex-pkmn Demo Edits

This demo turns classic games into AI interaction surfaces while they still run on their original engines.

In Ocarina of Time, Navi becomes an in-game prompt interface for GPT-5.5. In Pokemon Emerald, a custom NPC in Professor Birch's lab lets the player talk to GPT-5.5, then uses game-side tools to grant Pokemon or warp directly to the end of the game.

The point is not just that an old game can call a model. It is that decompiled games can become living, moddable frontends for modern AI: familiar worlds, original engine constraints, and new programmable behavior layered into the game itself.

## What Changed

This project modifies two community decompilation projects for a hackathon demo:

- **Ocarina of Time**: adds a Navi/Codex prompt flow that lets the player submit in-game text and receive an AI response back through the game UI.
- **Pokemon Emerald**: adds a custom Codex NPC, prompt-entry flow, starter Pokemon changes, and tool-backed interactions for granting Pokemon and warping game state.

## Why Decompilation Projects Work Well Here

Video game decompilation projects reconstruct classic games as buildable C/source-code projects. They do not replace the need for original game data. Instead, they let developers rebuild and modify a game when paired with legally obtained assets or ROMs and the upstream build tooling.

That makes them useful hackathon targets: the games still behave like the originals, but specific systems can be changed, extended, and rebuilt. For this demo, the game engines become small AI-native runtimes without turning the games into ports or remakes.

## Repository Note

This repository contains only our hackathon changes, not the full upstream game decompilation repositories. The underlying games and assets remain owned by their respective rights holders. Any build or run flow depends on legally obtained original game data and the requirements of the relevant upstream projects.

## Base Projects

- Ocarina of Time decompilation: [zeldaret/oot](https://github.com/zeldaret/oot)
- Pokemon Emerald decompilation: [pret/pokeemerald](https://github.com/pret/pokeemerald)

## What Is Included

- `patches/oot/*.patch`: three local OOT commits for the Navi/Codex UI and IS64 prompt flow.
- `patches/pokeemerald.patch`: binary-capable patch for the Pokemon Emerald Codex NPC, prompt flow, starter changes, and game-state tools.
- `pokeemerald/graphics/pokemon/custom_starters/`: original custom starter preview/source assets used by the patch.

## Apply the OOT Patch

```sh
git clone https://github.com/zeldaret/oot.git
cd oot
git am --3way /path/to/codex-pkmn-demo-edits/patches/oot/*.patch
```

Then follow the upstream `zeldaret/oot` build instructions for your platform. After the normal setup/build, run the produced ROM in an emulator or on your normal OOT development target.

## Apply the Pokemon Emerald Patch

```sh
git clone https://github.com/pret/pokeemerald.git
cd pokeemerald
git apply --binary /path/to/codex-pkmn-demo-edits/patches/pokeemerald.patch
cp -R /path/to/codex-pkmn-demo-edits/pokeemerald/graphics/pokemon/custom_starters graphics/pokemon/
make -j
```

The build outputs a GBA ROM from the upstream project. Run it with a GBA emulator after applying the patch and building.

## Notes for Judges

The patch-only format is deliberate: it demonstrates the work while avoiding redistribution of the full upstream repositories. To review the implementation, apply the patches to clean checkouts of the linked base projects.
