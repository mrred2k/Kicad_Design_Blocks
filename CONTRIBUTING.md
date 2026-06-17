# Contributing

## Adding a New Block

1. In KiCad Schematic Editor: select the circuit → right-click → **Save as Design Block**
2. Choose the `blocks` library, fill in Name, Keywords, Description and the metadata fields below
3. Optionally add the PCB layout fragment in the PCB Editor
4. Open a pull request

## Naming & Description

Block names follow `Function_KeySpec` — e.g. `Stepdown_24VIn_5VOut`, `LinearReg_3V3`.

- **Description**: function first, then key parameters — e.g. `Buck DC/DC converter, Vin max 32V, Vout fixed 5V`
- **Keywords**: space-separated, lowercase except units — e.g. `buck step-down dcdc converter 5V power`

## Metadata Fields

| Field | Allowed Values | Description |
|-------|---------------|-------------|
| `maturity` | `schematic` / `layout` / `produced` | Highest stage reached |
| `lcsc_parts` | `yes` / `no` | LCSC part numbers assigned to all components |
| `jlcpcb_basic` | `yes` / `no` | Parts chosen from JLCPCB Basic Parts list where possible (no per-part surcharge) |
| `has_3d` | `yes` / `partial` / `no` | 3D models assigned to all, some, or no components |
| `reviewed` | `yes` / `no` | Reviewed by someone other than the author — set by the reviewer when merging |

THT components that require hand soldering should be mentioned in the Description.

### Example `.json`

```json
{
  "description": "Short description of what this circuit does",
  "keywords": "keyword1 keyword2",
  "fields": {
    "maturity": "layout",
    "lcsc_parts": "yes",
    "jlcpcb_basic": "yes",
    "has_3d": "yes",
    "reviewed": "no"
  }
}
```

Do not add a `README.md` inside a block folder — it is auto-generated on merge and will be overwritten. Extra context belongs in the `description` field of the block's `.json` file.

## CI / Automation

Three workflows run automatically:

| Workflow | Trigger | What it does |
|----------|---------|--------------|
| **Validate blocks** | Every PR touching `blocks.kicad_blocks/` | Checks all metadata fields are present and valid, fails hard if not |
| **PR preview** | Every PR touching `blocks.kicad_blocks/` | Generates schematic/PCB SVG previews and posts them as a PR comment |
| **Generate previews** | Push to `main` | Regenerates all SVG previews and commits them to the repo |
