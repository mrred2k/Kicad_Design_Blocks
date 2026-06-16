# Contributing

## Adding a New Block

1. In KiCad Schematic Editor: select the circuit → right-click → **Save as Design Block**
2. Choose the `blocks` library (points to `blocks.kicad_blocks/`)
3. Fill in Name, Keywords, Description — and the metadata fields below
4. Optionally add the PCB layout fragment in the PCB Editor
5. Open a pull request

## Naming & Description

Block names follow the pattern `Function_KeySpec` — e.g. `Stepdown_24VIn_5VOut`, `LinearReg_3V3`.

- **Description**: function first, then key parameters — e.g. `Buck (step-down) DC/DC converter, Vin max 32V, Vout fixed 5V`
- **Keywords**: space-separated, lowercase except units — e.g. `buck step-down dcdc converter 5V power`

## Required Metadata Fields

Every block must have these fields set in its Design Block Properties (or directly in the `.json` file):

| Field | Allowed Values | Description |
|-------|---------------|-------------|
| `maturity` | `schematic` / `layout` / `produced` | Highest stage reached: schematic only, schematic + PCB layout, or built and confirmed working |
| `lcsc_parts` | `yes` / `no` | Whether LCSC part numbers are assigned to all components |
| `lcsc_basic_optimized` | `yes` / `no` | Whether parts were chosen from LCSC Basic parts where possible (no extended surcharge at JLCPCB) |
| `has_3d` | `yes` / `partial` / `no` | Whether 3D models are assigned to all (`yes`), some (`partial`), or no components (`no`) |
| `reviewed` | `yes` / `no` | Whether someone other than the author has reviewed the block — set by the reviewer when merging |

### Example `.json`

```json
{
  "description": "Short description of what this circuit does",
  "keywords": "keyword1 keyword2",
  "fields": {
    "maturity": "layout",
    "lcsc_parts": "yes",
    "lcsc_basic_optimized": "yes",
    "has_3d": "yes",
    "reviewed": "no"
  }
}
```

## Notes

- THT components that require hand soldering should be mentioned in the Description
- `reviewed: "yes"` means a second person checked it, not the author
