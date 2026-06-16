# KiCad Design Blocks

Reusable KiCad 10 design blocks (schematic + PCB layout fragments) for use as a Git submodule.
A design block bundles a schematic fragment with an optional PCB layout fragment so circuits can be reused across projects without copy-pasting.

## Structure

```
blocks.kicad_blocks/
└── <BlockName>.kicad_block/
    ├── <BlockName>.kicad_sch   # Schematic fragment
    ├── <BlockName>.kicad_pcb   # PCB layout fragment (optional)
    └── <BlockName>.json        # Block metadata and status fields
```

## Using as a Git Submodule

### Initial setup

```bash
git submodule add https://github.com/<user>/kicad-design-blocks.git kicad-design-blocks
git commit -m "Add kicad-design-blocks submodule"
```

Then in KiCad: **Preferences → Manage Design Block Libraries** → add:

| Nickname | Path |
|----------|------|
| `blocks` | `${KIPRJMOD}/kicad-design-blocks/blocks.kicad_blocks` |

This creates a `design-block-lib-table` in your project folder — commit it to your project repo.

### Cloning a project that uses this submodule

```bash
git clone --recurse-submodules <project-url>
# or if already cloned:
git submodule update --init
```

### Pulling new blocks into an existing project

```bash
git submodule update --remote kicad-design-blocks
git add kicad-design-blocks
git commit -m "Update kicad-design-blocks"
```

## Adding a New Block

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow and required metadata fields.

## KiCad Documentation

- [Schematic Design Blocks](https://docs.kicad.org/10.0/en/eeschema/eeschema.html#schematic-design-blocks)
- [PCB Design Blocks](https://docs.kicad.org/10.0/en/pcbnew/pcbnew.html#pcb-design-blocks)
