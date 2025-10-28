# 📖 Complete Documentation Index

## 🎯 New User? Start Here!

**[START_HERE.md](START_HERE.md)** - Choose your learning path (5 min)

Then pick based on your style:
- 🏃 **Fast learner?** → [QUICKSTART.md](QUICKSTART.md)
- 🎨 **Visual person?** → [VISUAL_GUIDE.md](VISUAL_GUIDE.md)  
- 🎬 **Want to see it work?** → [LIVE_DEMO.md](LIVE_DEMO.md)
- 📖 **Need everything?** → [README.md](README.md)

---

## 📚 All Documentation Files

### Essential Reading
| File | Purpose | Time | Priority |
|------|---------|------|----------|
| **[START_HERE.md](START_HERE.md)** | Navigation & learning paths | 5 min | ⭐⭐⭐⭐⭐ |
| **[QUICKSTART.md](QUICKSTART.md)** | Get started in 5 minutes | 5 min | ⭐⭐⭐⭐⭐ |
| **[LIVE_DEMO.md](LIVE_DEMO.md)** | See actual generated code | 10 min | ⭐⭐⭐⭐ |

### Deep Dive
| File | Purpose | Time | When to Read |
|------|---------|------|-------------|
| **[VISUAL_GUIDE.md](VISUAL_GUIDE.md)** | Diagrams & workflows | 10 min | Understanding how it works |
| **[README.md](README.md)** | Complete documentation | 30 min | Need full details |
| **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** | High-level overview | 15 min | Want big picture |

### Reference
| File | Purpose | When to Use |
|------|---------|------------|
| **[FILE_LIST.txt](FILE_LIST.txt)** | Complete file inventory | Finding specific files |
| **[INDEX.md](INDEX.md)** | This file! | Navigation |

---

## 💻 Code Files

### Templates (Write Your Code Here!)
- `templates/Kinematics.template` - Example template with placeholders

### Generated Code (Auto-Created - Don't Edit!)
- `generated/Kinematics.cxx` - Baseline variant
- `generated/Kinematics_bJER10v00.cxx` - bJER10v00 variant
- `generated/Kinematics_MuonCorr.cxx` - MuonCorr variant

### Framework Code
- `include/AnalysisConfig.h` - Configuration system
- `include/PlotUtils.h` - Common utilities
- `src/AnalysisConfig.cpp` - Implementation
- `src/PlotUtils.cpp` - Implementation

### Automation
- `scripts/generate_analysis.py` - Code generator (Python)
- `Makefile` - Build automation
- `examples.py` - Runnable examples

---

## 🎓 Learning Paths

### Path 1: "I'm in a hurry!" (10 minutes)
```
START_HERE.md → QUICKSTART.md → Try: make generate-all
```

### Path 2: "Show me proof it works" (20 minutes)
```
START_HERE.md → LIVE_DEMO.md → QUICKSTART.md → Try it yourself
```

### Path 3: "I want to understand everything" (45 minutes)
```
START_HERE.md → VISUAL_GUIDE.md → README.md → examples.py → QUICKSTART.md
```

### Path 4: "I'm migrating existing code" (60 minutes)
```
PROJECT_SUMMARY.md → LIVE_DEMO.md → templates/Kinematics.template 
→ QUICKSTART.md (Migration section) → Try converting your file
```

---

## 🔍 Find What You Need

### I want to...

**...understand the problem this solves**
→ [PROJECT_SUMMARY.md](PROJECT_SUMMARY.md) - Problem & Solution section

**...see it working with real code**
→ [LIVE_DEMO.md](LIVE_DEMO.md) - Side-by-side comparisons

**...get started immediately**
→ [QUICKSTART.md](QUICKSTART.md) - 3 steps to success

**...understand how template variables work**
→ [VISUAL_GUIDE.md](VISUAL_GUIDE.md) - Placeholder reference card

**...migrate my existing files**
→ [QUICKSTART.md](QUICKSTART.md) - Use Case 1 section

**...add a new variant**
→ [README.md](README.md) - Adding New Variant section

**...add a new analysis type**
→ [README.md](README.md) - Adding New Analysis Type section

**...see practical examples**
→ Run: `python3 examples.py`

**...troubleshoot an issue**
→ [README.md](README.md) - Troubleshooting section

**...understand all files**
→ [FILE_LIST.txt](FILE_LIST.txt) - Complete inventory

---

## 🎯 Quick Reference

### Essential Commands
```bash
make all              # Build framework
make generate-all     # Generate all variants
make help             # Show all commands
python3 examples.py   # Run examples
```

### Essential Placeholders
```
{{PATH_INFIX}}        → MJB, MJB_bJER10v00, etc.
{{LJET_PT}}           → ljet_pt, ljet_bJR10v00_pt, etc.
{{FUNCTION_SUFFIX}}   → "", "_bJER10v00", etc.
```

### File Locations
```
templates/     → Your code (with placeholders)
generated/     → Auto-generated variants
include/       → C++ headers
src/           → C++ implementation
scripts/       → Python generator
```

---

## 📊 Documentation Statistics

- **Total docs**: 7 markdown files + 1 text file
- **Total pages**: ~50 pages equivalent
- **Code examples**: 30+ practical examples
- **Diagrams**: 15+ visual explanations
- **Lines of documentation**: 2,500+ lines

---

## 🎬 Recommended First Session (30 minutes)

1. **[START_HERE.md](START_HERE.md)** (5 min) - Understand the framework
2. **[LIVE_DEMO.md](LIVE_DEMO.md)** (10 min) - See real generated code
3. **[QUICKSTART.md](QUICKSTART.md)** (10 min) - Learn the commands
4. **Try it**: `make generate-all` (5 min) - Generate variants yourself

After this, you'll understand:
- What problem the framework solves
- How it works with real code
- How to use it
- That it actually works!

---

## 💡 Tips for Success

1. **Start with documentation** before diving into code
2. **View the generated examples** in `generated/` directory
3. **Try the commands** in a safe test environment first
4. **Read error messages** - they're helpful!
5. **Use diff** to compare template vs generated files

---

## 🆘 Need Help?

Check these in order:
1. **[QUICKSTART.md](QUICKSTART.md)** - Common tasks
2. **[README.md](README.md)** - Detailed troubleshooting
3. **[VISUAL_GUIDE.md](VISUAL_GUIDE.md)** - Visual explanations
4. **[LIVE_DEMO.md](LIVE_DEMO.md)** - See working examples

---

## ✅ Success Checklist

Track your progress:

```
☐ Read START_HERE.md
☐ Chose a learning path
☐ Understood the problem
☐ Saw working examples (LIVE_DEMO.md)
☐ Ran make generate-all successfully
☐ Viewed generated files
☐ Understood placeholders
☐ Ready to convert my code!
```

---

## 🎉 You're Ready!

Pick your starting point above and begin eliminating code duplication!

**Most popular path**: START_HERE.md → LIVE_DEMO.md → QUICKSTART.md → Try it!

🚀 **Happy coding!**
