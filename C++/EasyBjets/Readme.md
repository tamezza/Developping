# Automated Analysis Framework

## Overview

This framework eliminates code duplication across different analysis variants by providing:
- **Centralized configuration** for different analysis variants
- **Template-based code generation** for creating variant-specific files
- **Common utilities** shared across all analysis types
- **Automated build system** using Make

## Problem Solved

Previously, you had multiple nearly-identical files like:
- `Kinematics.cxx`, `Kinematics_bJER10v00.cxx`, `Kinematics_bJER10v01.cxx`, `Kinematics_MuonCorr.cxx`
- `Mass_Response.cxx`, `Mass_Response_bJER10v00.cxx`, etc.

The only differences were:
1. Input/output file paths (with variant prefixes)
2. Variable names (with variant-specific naming)
3. Function names (with variant suffixes)

This framework generates these variants automatically from templates.

## Directory Structure

```
analysis_framework/
│
├── include/                    # Header files
│   ├── AnalysisConfig.h       # Variant configuration
│   └── PlotUtils.h            # Common plotting utilities
│
├── src/                        # Source files
│   ├── AnalysisConfig.cpp     # Configuration implementation
│   └── PlotUtils.cpp          # Plotting utilities implementation
│
├── templates/                  # Template files
│   ├── Kinematics.template
│   ├── Mass_Response.template
│   └── Rdb_pT_bins_MCut.template
│
├── generated/                  # Generated variant files
│   ├── Kinematics_bJER10v00.cxx
│   ├── Kinematics_bJER10v01.cxx
│   └── ... (auto-generated)
│
├── config/                     # Configuration files
│   └── analysis_config.ini    # Runtime configuration
│
├── scripts/                    # Utility scripts
│   └── generate_analysis.py   # Code generator
│
└── build/                      # Build artifacts
    └── libAnalysisFramework.a # Static library
```

## Quick Start

### 1. Setup

```bash
# Build the framework
make all

# Create example template
make create-template
```

### 2. Generate Analysis Variants

```bash
# Generate all variants for all analysis types
make generate-all

# Generate specific variant
make generate VARIANT=bJER10v00 ANALYSIS=Kinematics

# Or use the Python script directly
python3 scripts/generate_analysis.py --variant bJER10v00 --analysis Kinematics
```

### 3. Compile Generated Files

```bash
# Compile all generated ROOT macros
make compile-generated

# Or compile manually
root -l -b -q generated/Kinematics_bJER10v00.cxx+
```

## Supported Variants

1. **baseline** - Standard analysis (no suffix)
2. **bJER10v00** - bJER version 10v00
3. **bJER10v01** - bJER version 10v01
4. **MuonCorr** - Muon correction variant

## Supported Analysis Types

1. **Kinematics** - Jet kinematics analysis
2. **Mass_Response** - Mass response analysis
3. **Rdb_pT_bins_MCut** - R_DB vs pT with mass cut
4. **RdbNoMcut** - R_DB without mass cut

## Template System

### Template Variables

Templates use placeholder variables that are automatically replaced:

| Placeholder | Description | Example (bJER10v00) |
|-------------|-------------|---------------------|
| `{{PATH_INFIX}}` | Directory path component | `MJB_bJER10v00` |
| `{{FILE_INFIX}}` | File name component | `bJER10v00_` |
| `{{VAR_PREFIX}}` | Variable name prefix | `bJR10v00_` |
| `{{VAR_SUFFIX}}` | Suffix for function names | `_bJER10v00` |
| `{{LJET_PT}}` | Large jet pT variable | `ljet_bJR10v00_pt` |
| `{{LJET_MASS}}` | Large jet mass variable | `ljet_bJR10v00_mass` |
| `{{BRANCH_LJET_PT}}` | Branch name for pT | `ljet_bJR10v00_pt` |
| `{{ANALYSIS_TYPE}}` | Analysis name | `Kinematics` |

### Creating a Template

1. Take your base analysis code
2. Replace variant-specific parts with placeholders
3. Save as `.template` file in `templates/` directory

Example:
```cpp
// Original code
tree->SetBranchAddress("ljet_bJR10v00_pt", &ljet_bJR10v00_pt);

// Template version
tree->SetBranchAddress("{{BRANCH_LJET_PT}}", &{{LJET_PT}});
```

## Using the Framework in Your Code

### Option 1: Use Configuration Classes (C++)

```cpp
#include "include/AnalysisConfig.h"
#include "include/PlotUtils.h"

// Create configuration for specific variant
AnalysisConfig config(AnalysisConfig::Variant::BJER10V00);

// Get paths
std::string inputPath = config.getInputPath("data", "0p46");
std::string outputPath = config.getOutputPath("Kinematics", "0p46");

// Get variable names
std::string ptVar = config.getVarName("ljet_pt");      // -> "ljet_bJR10v00_pt"
std::string branchName = config.getBranchName("ljet_pt"); // -> "ljet_bJR10v00_pt"

// Get function name
std::string funcName = config.getFunctionName("Kinematics"); // -> "Kinematics_bJER10v00"

// Use common utilities
PlotUtils::DrawAtlasLabel();
PlotUtils::CreateDirectoryIfNotExists(outputPath);
```

### Option 2: Use Generated Files

Simply use the generated variant-specific files directly:
```bash
root -l generated/Kinematics_bJER10v00.cxx
```

## Configuration File

Create `config/analysis_config.ini` for runtime settings:

```ini
[Analysis]
type = Kinematics

[WorkingPoints]
points = 46, 60, 77, 85, 125, 155

[Variants]
baseline = true
bJER10v00 = true
bJER10v01 = true
MuonCorr = true

[Paths]
eos_path = ../../
output_base = ../Plots/
```

## Advanced Usage

### Batch Processing All Variants

```python
from scripts.generate_analysis import AnalysisGenerator

generator = AnalysisGenerator()

# Generate all variants for specific analysis
for variant in ['baseline', 'bJER10v00', 'bJER10v01', 'MuonCorr']:
    generator.generate_file('Kinematics', variant, 'Kinematics')
```

### Adding a New Variant

1. Update `scripts/generate_analysis.py`:
```python
VARIANTS = {
    # ... existing variants ...
    'new_variant': {
        'name': 'NewVariant',
        'suffix': '_NewVariant',
        'file_infix': 'NewVariant_',
        'var_prefix': 'new_',
        'path_infix': 'MJB_NewVariant'
    }
}
```

2. Update `include/AnalysisConfig.h`:
```cpp
enum class Variant {
    BASELINE,
    BJER10V00,
    BJER10V01,
    MUON_CORR,
    NEW_VARIANT  // Add new variant
};
```

3. Regenerate files:
```bash
make generate-all
```

### Adding a New Analysis Type

1. Create template: `templates/MyNewAnalysis.template`
2. Add to generator:
```python
ANALYSIS_TYPES = [..., 'MyNewAnalysis']
```
3. Generate:
```bash
make generate ANALYSIS=MyNewAnalysis VARIANT=bJER10v00
```

## Benefits

✅ **No Code Duplication** - Write analysis logic once, generate all variants

✅ **Easy Maintenance** - Update template, regenerate all variants

✅ **Consistent** - All variants follow same structure and style

✅ **Flexible** - Add new variants or analysis types easily

✅ **Type Safe** - Configuration classes prevent naming errors

✅ **Automated** - Scripts handle tedious file generation

## Makefile Commands

```bash
make help              # Show all available commands
make all               # Build framework library
make library           # Build static library
make generate-all      # Generate all variants
make generate          # Generate specific variant
make clean             # Clean build artifacts
make clean-generated   # Remove generated files
make distclean         # Full clean
make create-template   # Create example template
make compile-generated # Compile ROOT macros
```

## Example Workflow

```bash
# 1. Setup
make all

# 2. Create your template
# Edit templates/Kinematics.template

# 3. Generate all variants
make generate-all

# 4. Compile and run
root -l generated/Kinematics_bJER10v00.cxx
```

## Troubleshooting

**Problem**: Template variable not being replaced

**Solution**: Check that placeholder is exactly `{{VARIABLE}}` with double braces

---

**Problem**: Generated file has compilation errors

**Solution**: Verify template syntax is valid C++ before placeholders are replaced

---

**Problem**: Wrong variable names in generated code

**Solution**: Check variant configuration in `generate_analysis.py` matches your naming convention

## Migration Guide

To migrate existing code to this framework:

1. **Identify common code** - Find code that's identical across variants
2. **Create base template** - Use baseline version as template
3. **Add placeholders** - Replace variant-specific parts
4. **Test generation** - Generate one variant and verify
5. **Generate all** - Create all variants
6. **Verify** - Compare generated files with originals

## Contributing

To extend this framework:
1. Add new variants in configuration
2. Create templates for new analysis types
3. Update documentation
4. Test generation for all combinations

## License

This framework is designed for ATLAS analysis code.
