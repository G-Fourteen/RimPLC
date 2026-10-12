# RimPLC

A standalone ladder-logic advisor for RimWorld. Sensors read the colony, tags set
thresholds, marks hold recorded values, and rungs describe **if this, then this**.
The main tab shows each rung's live contacts and lets you edit, enable, import and
export a ladder. Advice is the default; this version's automatic coils are limited
to messages, marks and tags. It does not build, spawn or destroy world objects.

**Version 0.1.0.** Package ID `Operator.RimPLC`; author `Operator`.
RimWorld **1.6 and 1.7** are declared targets and share the existing `1.6/` content
folder. A declaration is not a compatibility result: a running 1.7 session has
not yet been verified. The core requires no other mod, Harmony or expansion.
Rimrooms-specific preset rungs remain inactive without Rimrooms.

Read the [user guide](docs/USER_GUIDE.md). JSON formats for rules, tags, sensors,
marks, ladders and commands are included under [docs/schema](docs/schema/).

## Install

Copy this repository's mod files to a local Mods folder as `RimPLC`, keeping
`About/` and `LoadFolders.xml` directly inside it. The loadable files are
`About/`, `LoadFolders.xml`, `1.6/`, `Languages/` and `Presets/`; `Source/` is for
developers and `BridgeTools/` is the separate optional companion below.
Enable RimPLC through your mod manager. Back up a save before changing its mod
list; removal from an existing save has not been checked.

## Build the core

Install a .NET SDK and use your own local RimWorld installation:

```powershell
dotnet build Source/RimPLC/RimPLC.csproj -c Release -p:RimWorldPath="C:/path/to/RimWorld"
```

`RIMWORLD_PATH` is also accepted. The project targets .NET Framework 4.7.2 and
C# 7.3, treats warnings as errors, and writes `1.6/Assemblies/RimPLC.dll`.
Game assemblies are read from `RimWorldWin64_Data/Managed` with `Private=false`
and are never copied into the output. Build commands do not stage or launch the
game. The shipped `Presets/LadderV2.json` is self-contained; no parent repository,
Python generator or training dataset is needed to build or run this mod.

## Optional RimBridgeServer tools

The core mod does not require RimBridgeServer. Its file API works at
`<RimWorld config folder>/RimPLC/inbox.jsonl`, returning results in `outbox.jsonl`.

To build the optional companion after building the core:

```powershell
dotnet build Source/RimPLC.BridgeTools/RimPLC.BridgeTools.csproj -c Release -p:RimWorldPath="C:/path/to/RimWorld" -p:RimBridgeSdkPath="C:/path/to/RimBridgeServer.Sdk.dll"
```

With RimBridgeServer installed, copy **only** `BridgeTools/RimPLC.BridgeTools.dll`
to `<RimWorld>/BridgeTools/RimPLC/`. The SDK and bridge are supplied by their own
project; neither is bundled here. The companion exposes `rimplc/read_ladder`,
`read_state`, `set_tag`, `set_mark`, `upsert_rung`, `remove_rung`, `enable_rung`,
`letters_seen`, `export` and `import`.

## License and repositories

Original RimPLC source is MIT licensed; see [LICENSE](LICENSE). RimWorld and its
assemblies belong to Ludeon Studios and are not included.

- [Forgejo](https://git.unityailab.com/GFourteen/RimPLC)
- [GitHub](https://github.com/G-Fourteen/RimPLC)


These are the owner's publication destinations. A local export does not confirm
that either remote has been created or updated.
