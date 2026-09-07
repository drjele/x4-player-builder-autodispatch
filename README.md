# Player Builder Autodispatch for X4: Foundations

<p align="center">
  <img src="extension/preview.jpg" alt="Player Builder Autodispatch" width="512">
</p>

Player-owned builders running **Find Build Tasks** do not automatically respond when one of your stations need a construction vessel. This is not a range or pilot-skill problem: vanilla
`build.buildstorage` explicitly broadcasts automatic requests only for non-player build modules.

This mod enables those requests for player-owned stations and makes them private to your own builders. When a station build or reconstruction reaches the point where it has the required resources and is waiting for a construction vessel, an available player-owned builder running **Find Build Tasks** can accept it automatically.

Before accepting, the builder must also have a valid gate route to the station under its current sector-travel blacklist. A builder trapped in an unreachable area, or cut off by its blacklist, will ignore the signal so another eligible builder can answer it.

**Requires X4: Foundations 9.00.** No DLC or other mod is required. It works on an existing savegame and stores no state of its own.

## Install

```bash
./install.sh
```

The helper copies `extension/` into the game's `extensions/<extension-id>`
directory, using the id in `extension/content.xml`. It searches the usual Steam layouts and additional library folders. To choose an installation:

```bash
X4_PATH="/path/to/X4 Foundations" ./install.sh
```

Restart X4 after installing or updating. To remove the manual installation:

```bash
./install.sh --uninstall
```

## Behaviour

The complete ownership rule is:

| Requesting station | Builder that may accept automatically     |
|--------------------|-------------------------------------------|
| Player             | Player only, with a valid permitted route |
| NPC                | Vanilla rules, unchanged                  |

The mod does not assign an arbitrary idle builder. The ship must already have **Find Build Tasks**
as its running default behaviour and must pass all vanilla checks: it must be unassigned, able to dock by relation, within the station's five-jump request search, and the station must lie inside the builder behaviour's configured search range. The additional route check uses the builder's sector travel blacklist before it reserves the task; sector activity rules continue to apply during its movement as in vanilla.

The station also needs its ordinary vanilla construction prerequisites. Destroyed modules are automatically returned to its construction plan by the station engineer, but reconstruction cannot start until the build storage has the required wares. Damaged modules that were not destroyed use the station repair system instead and do not need a builder.

## What it changes

Two small XPath patches are applied to the 9.00 vanilla AI scripts:

| Patch                                 | Change                                                                                                                               |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `aiscripts/build.buildstorage.xml`    | Lets player build modules broadcast the same request as NPC build modules and use the same short recheck while waiting for resources |
| `aiscripts/order.build.find.task.xml` | Rejects a player station's request on every non-player builder and on player builders without a blacklist-compliant gate route       |

The second patch is essential. Simply deleting vanilla's player exclusion would allow a nearby NPC builder to accept the broadcast without going through the normal manual hire and payment flow.

## Status

Both selectors and their single-match cardinality are verified against the installed X4 9.00 game files. The merged XML is structurally validated, and automatic player-builder assignment has been verified in game on an existing save.

## Publishing to the Steam Workshop

Install **X Tools** (Steam app 282160) and keep Steam running and logged in with an account that owns X4. On Linux, install Proton as well; on Windows, run the helper from Git Bash, MSYS or Cygwin.

```bash
./publish.sh publish
./publish.sh update "what changed"
```

Use `publish` once, then `update` with a change note. `X4_PATH`,
`X_TOOLS_PATH` and `PROTON_PATH` override automatic discovery. The staging location must contain an `extensions` directory.

The first upload records the numeric id in `steam/workshop-id`; retain that file for future updates. The readable id in the repository's `content.xml`
stays unchanged. After publishing, open the printed Workshop URL, complete any required Steam agreement and choose the item's visibility. Avoid keeping both the manual installation and a subscription to the same mod enabled.

Update the manifest version and release date together with `CHANGELOG.md`
when releasing. See [Development](DEVELOPMENT.md) for staging, platform and release conventions.

## Development

See [DEVELOPMENT.md](DEVELOPMENT.md) for setup, code style, validation and release conventions.

## Legal

MIT, see [`LICENSE`](LICENSE). Non-commercial fan project; X4: Foundations belongs to Egosoft GmbH and this project is not affiliated with or endorsed by Egosoft.
