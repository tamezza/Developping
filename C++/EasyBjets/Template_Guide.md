# 📝 Template Guide - Complete Reference

## 🎯 Available Templates

Your framework now includes **5 complete templates** ready to use:

### 1. **Kinematics_FULL.template** (64 KB)
Complete kinematics analysis from your original code
- All histogram types
- Full analysis workflow
- Production-ready

### 2. **Mass_Response.template** (40 KB)
Mass response and direct balance analysis
- Mass distributions
- R_DB calculations
- Scale factor computations

### 3. **Rdb_pT_bins_MCut.template** (88 KB)
R_DB vs pT with mass cuts
- Binned pT analysis
- Mass cut applications
- Comprehensive plots

### 4. **CustomAnalysis.template** (11 KB)
Simple example template for learning
- Clear structure
- Well-commented
- Perfect for understanding placeholders

### 5. **Kinematics.template** (13 KB)
Simplified kinematics template
- Streamlined version
- Good starting point

---

## 🔧 How to Use These Templates

### Quick Start: Generate All Variants

```bash
cd analysis_framework/

# Generate all variants from all templates
python3 scripts/generate_analysis.py --all

# Or use Makefile
make generate-all
```

### Generate Specific Variant

```bash
# Generate bJER10v00 variant of Kinematics
python3 scripts/generate_analysis.py \
    --variant bJER10v00 \
    --analysis Kinematics_FULL

# Generate MuonCorr variant of Mass_Response
python3 scripts/generate_analysis.py \
    --variant MuonCorr \
    --analysis Mass_Response
```

---

## 📖 Understanding Template Placeholders

### File-Level Placeholders

| Placeholder | Purpose | Example (baseline) | Example (bJER10v00) |
|-------------|---------|-------------------|---------------------|
| `{{ANALYSIS_TYPE}}` | Analysis name | `Kinematics` | `Kinematics` |
| `{{VAR_SUFFIX}}` | Variant suffix | `` (empty) | `_bJER10v00` |
| `{{FUNCTION_SUFFIX}}` | Function suffix | `` (empty) | `_bJER10v00` |

### Path Placeholders

| Placeholder | Purpose | Example (baseline) | Example (bJER10v00) |
|-------------|---------|-------------------|---------------------|
| `{{PATH_INFIX}}` | Directory path | `MJB` | `MJB_bJER10v00` |
| `{{FILE_INFIX}}` | File name infix | `` (empty) | `bJER10v00_` |

### Variable Name Placeholders

| Placeholder | Purpose | Example (baseline) | Example (bJER10v00) |
|-------------|---------|-------------------|---------------------|
| `{{LJET_PT}}` | Large jet pT variable | `ljet_pt` | `ljet_bJR10v00_pt` |
| `{{LJET_MASS}}` | Large jet mass variable | `ljet_m` | `ljet_bJR10v00_mass` |

### Branch Name Placeholders

| Placeholder | Purpose | Example (baseline) | Example (bJER10v00) |
|-------------|---------|-------------------|---------------------|
| `{{BRANCH_LJET_PT}}` | Branch name for pT | `ljet_pt` | `ljet_bJR10v00_pt` |
| `{{BRANCH_LJET_MASS}}` | Branch name for mass | `ljet_m` | `ljet_bJR10v00_mass` |

---

## 🎬 Example: What Gets Generated

### Template Code (Kinematics_FULL.template):

```cpp
void {{ANALYSIS_TYPE}}{{FUNCTION_SUFFIX}}() {
    std::vector<float>* {{LJET_PT}} = nullptr;
    tree->SetBranchAddress("{{BRANCH_LJET_PT}}", &{{LJET_PT}});
    
    std::string inputPath = "../../NtupleSlim/{{PATH_INFIX}}_0p46wp_slim/";
    std::string outputPath = "../Plots/{{PATH_INFIX}}/Kinematics/";
}
```

### Generated for Baseline:

```cpp
void Kinematics() {
    std::vector<float>* ljet_pt = nullptr;
    tree->SetBranchAddress("ljet_pt", &ljet_pt);
    
    std::string inputPath = "../../NtupleSlim/MJB_0p46wp_slim/";
    std::string outputPath = "../Plots/MJB/Kinematics/";
}
```

### Generated for bJER10v00:

```cpp
void Kinematics_bJER10v00() {
    std::vector<float>* ljet_bJR10v00_pt = nullptr;
    tree->SetBranchAddress("ljet_bJR10v00_pt", &ljet_bJR10v00_pt);
    
    std::string inputPath = "../../NtupleSlim/MJB_bJER10v00_0p46wp_slim/";
    std::string outputPath = "../Plots/MJB_bJER10v00/Kinematics/";
}
```

---

## 🔍 Template Comparison

### Which Template Should I Use?

| Template | Use When | Pros | Cons |
|----------|----------|------|------|
| **Kinematics_FULL** | Production analysis | Complete, tested | Large file |
| **Mass_Response** | Mass/R_DB analysis | Focused, complete | Specific use |
| **Rdb_pT_bins_MCut** | Binned pT analysis | Comprehensive | Very large |
| **CustomAnalysis** | Learning/starting | Simple, clear | Basic features |
| **Kinematics** | Quick start | Compact | Less complete |

**Recommendation**: Start with **CustomAnalysis** to understand, then use **Kinematics_FULL** for production.

---

## 🎓 Tutorial: Using CustomAnalysis Template

### Step 1: View the Template

```bash
cd analysis_framework/templates/
less CustomAnalysis.template
```

### Step 2: Generate a Variant

```bash
python3 scripts/generate_analysis.py \
    --variant bJER10v00 \
    --analysis CustomAnalysis \
    --template-dir templates \
    --output-dir generated
```

### Step 3: Check the Generated File

```bash
less generated/CustomAnalysis_bJER10v00.cxx
```

### Step 4: Compare with Baseline

```bash
# Generate baseline
python3 scripts/generate_analysis.py \
    --variant baseline \
    --analysis CustomAnalysis

# Compare
diff generated/CustomAnalysis.cxx generated/CustomAnalysis_bJER10v00.cxx
```

### Step 5: Compile and Run (if ROOT is available)

```bash
root -l -b -q generated/CustomAnalysis_bJER10v00.cxx+
```

---

## 🛠️ Customizing Templates

### Add Your Own Variables

1. Edit template file
2. Add placeholder where variable name changes:

```cpp
// If variable name is variant-specific, use placeholder:
std::vector<float>* {{MY_NEW_VAR}} = nullptr;

// If variable name is the same for all variants, use directly:
std::vector<float>* my_constant_var = nullptr;
```

### Add New Placeholders

1. Edit `scripts/generate_analysis.py`
2. Add to `get_replacements()` method:

```python
def get_replacements(self, variant: str) -> Dict[str, str]:
    config = self.VARIANTS[variant]
    
    return {
        # ... existing placeholders ...
        
        # Your new placeholder
        '{{MY_NEW_PLACEHOLDER}}': f"custom_{config['var_prefix']}name"
    }
```

### Create New Template

1. Copy existing template:
```bash
cp templates/CustomAnalysis.template templates/MyAnalysis.template
```

2. Edit and add placeholders

3. Add to generator:
```python
ANALYSIS_TYPES = ['Kinematics', 'Mass_Response', 'MyAnalysis']
```

4. Generate:
```bash
make generate ANALYSIS=MyAnalysis VARIANT=bJER10v00
```

---

## 📊 Template Statistics

### File Sizes
- **Kinematics_FULL**: 64 KB (1,463 lines)
- **Mass_Response**: 40 KB (973 lines)
- **Rdb_pT_bins_MCut**: 88 KB (2,156 lines)
- **CustomAnalysis**: 11 KB (314 lines)
- **Kinematics**: 13 KB (319 lines)

### Placeholder Counts
Each template uses approximately:
- **15-20** path/file placeholders
- **10-15** variable name placeholders
- **2-3** function name placeholders

### Generated Files (per template)
- 1 template → 4 variants (baseline, bJER10v00, bJER10v01, MuonCorr)
- Total generated: **5 templates × 4 variants = 20 files**

---

## ⚠️ Common Issues and Solutions

### Issue 1: Variable Name Not Replaced

**Problem**: Generated file has `{{LJET_PT}}` instead of `ljet_pt`

**Solution**: 
- Check placeholder is exactly `{{LJET_PT}}` (double braces, all caps)
- Regenerate: `make generate-all`

### Issue 2: Compilation Error After Generation

**Problem**: Generated .cxx file won't compile

**Solution**:
- Check template is valid C++ before placeholders
- Verify all braces are balanced
- Look for syntax errors in template

### Issue 3: Wrong Branch Names

**Problem**: `ljet_pt` used but should be `ljet_bJR10v00_pt`

**Solution**:
- Use `{{BRANCH_LJET_PT}}` for branch names in `SetBranchAddress()`
- Use `{{LJET_PT}}` for variable declarations
- They're different!

### Issue 4: Path Not Found

**Problem**: Generated code can't find input files

**Solution**:
- Check `{{PATH_INFIX}}` is used correctly in paths
- Verify actual data files exist at expected locations
- Update template paths if your structure is different

---

## 🎯 Best Practices

### DO:
✅ Use placeholders for variant-specific parts  
✅ Test template with baseline variant first  
✅ Comment your custom placeholders  
✅ Keep templates in version control  
✅ Use descriptive placeholder names  

### DON'T:
❌ Edit generated files (edit template instead)  
❌ Mix placeholder types ({{LJET_PT}} vs ljet_pt)  
❌ Forget to regenerate after template changes  
❌ Commit generated files to version control  
❌ Use placeholders for non-variant parts  

---

## 📚 Quick Reference Card

```
┌─────────────────────────────────────────────────────────┐
│                 TEMPLATE PLACEHOLDER CHEAT SHEET         │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Function Names:                                         │
│    void {{ANALYSIS_TYPE}}{{FUNCTION_SUFFIX}}()          │
│    → Kinematics() or Kinematics_bJER10v00()            │
│                                                          │
│  Variable Declarations:                                  │
│    std::vector<float>* {{LJET_PT}} = nullptr;          │
│    → ljet_pt or ljet_bJR10v00_pt                       │
│                                                          │
│  Branch Names:                                           │
│    tree->SetBranchAddress("{{BRANCH_LJET_PT}}", ...)   │
│    → "ljet_pt" or "ljet_bJR10v00_pt"                   │
│                                                          │
│  Paths:                                                  │
│    "../../NtupleSlim/{{PATH_INFIX}}_0p46wp_slim/"      │
│    → "../../NtupleSlim/MJB_0p46wp_slim/"               │
│    → "../../NtupleSlim/MJB_bJER10v00_0p46wp_slim/"     │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 Next Steps

1. **Try CustomAnalysis**: Start with the simple template
2. **Generate variants**: Run `make generate-all`
3. **Compare outputs**: Use `diff` to see differences
4. **Test compile**: Try compiling generated files
5. **Use production templates**: Switch to Kinematics_FULL or Mass_Response
6. **Create your own**: Copy CustomAnalysis and customize

---

## 📞 Getting Help

If you're stuck:

1. Check the [QUICKSTART.md](../QUICKSTART.md) for common commands
2. Review [LIVE_DEMO.md](../LIVE_DEMO.md) for examples
3. Read [README.md](../README.md) for detailed docs
4. Look at CustomAnalysis.template for reference

---

## ✅ Success Checklist

```
☐ Viewed at least one template
☐ Understood placeholder system
☐ Generated baseline variant
☐ Generated bJER10v00 variant
☐ Compared generated files
☐ Identified the differences
☐ Ready to use in production!
```

---

**You now have complete, production-ready templates! 🎉**

All templates are based on your actual code and ready to generate all variants automatically.
