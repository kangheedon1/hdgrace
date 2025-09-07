# HDGRACE BrowserAutomationStudio XML Generator

ALWAYS follow these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Prerequisites and Setup
- Run on Linux with Python 3.12+ installed
- No external dependencies required - uses only Python standard library
- Repository contains Korean documentation files and BAS XML templates

### Core Build and Execution
- **MAIN COMMAND**: `python3 HDGRACE_2025-09-07.py`
- **EXECUTION TIME**: ~7 seconds consistently. NEVER CANCEL - Set timeout to 30+ seconds minimum.
- **OUTPUT**: Generates 25MB+ XML file with 3,065 functions and 300,000+ actions
- **SUCCESS INDICATOR**: Exit code 0 and "Script finished successfully" message

### Build Workflow
1. Execute: `python3 HDGRACE_2025-09-07.py`
2. **TIMING**: Build completes in 6.8±0.1 seconds. NEVER CANCEL builds that appear to hang - wait minimum 30 seconds.
3. Check for success: Look for "Script finished successfully" in output
4. Verify outputs: Check for generated files (see Output Files section)

### Validation and Testing
- **XML VALIDATION**: Run `python3 -c "import xml.etree.ElementTree as ET; tree = ET.parse('C:\\\\Users\\\\office2\\\\Pictures\\\\Desktop\\\\3065\\\\valid/HDGRACE-최종본.XML'); print('XML Valid')"`
- **CONSISTENCY TEST**: Script produces identical timing (6.75-6.80s) across multiple runs
- **STRUCTURE VERIFICATION**: Generated XML contains exactly 3,065 functions and 312,630 actions
- Always verify XML structure after making changes to the generator

### Output Files
Generated files are placed in Windows-style paths (even on Linux):
- `C:\Users\office2\Pictures\Desktop\3065\valid/HDGRACE-최종본.XML` - Main 25MB BAS XML file
- `C:\Users\office2\Pictures\Desktop\3065\valid/_VALIDATION.txt` - Validation report
- `C:\Users\office2\Pictures\Desktop\3065\valid/_STATISTICS.json` - Generation statistics
- `C:\Users\office2\Pictures\Desktop\3065\valid/bas2910_generation.log` - Build log

### Error Scenarios and Troubleshooting
- **EXPECTED WARNINGS**: "Input file not found" for `C:\Users\office2\Pictures\Desktop\원본txt.파일` - this is normal
- **EXPECTED WARNINGS**: "GitHub cloning is a placeholder" - this is normal simulation mode
- **DATETIME WARNING**: `datetime.utcnow()` deprecation warning is expected and does not affect functionality
- If build fails, check Python version (requires 3.12+) and ensure no file permission issues

## Common Workflows

### Making Changes to Generator
1. Edit `HDGRACE_2025-09-07.py` 
2. Test with: `python3 -m py_compile HDGRACE_2025-09-07.py` (should complete silently)
3. Run full build: `python3 HDGRACE_2025-09-07.py`
4. Validate XML output as described above
5. **CRITICAL**: Always verify function and action counts remain above minimums (3,065 functions, 300,000 actions)

### Working with Korean Documentation
- `읽고 -꼭 100% 반영.txt` - Core requirements and refactoring principles
- `124개기능.txt` - 124 feature specifications in BAS XML format
- `기존+추가UI버튼_이모지를_큰_카테고리_별로_.txt` - UI button and emoji specifications
- `누락-기능/` - Directory with 58 missing feature files (numbered .txt files)
- These files contain Korean text describing browser automation features

### Module and Archive Files
- `modules.zip` - Multi-part archive containing BAS modules (warnings about multi-part are normal)
- `SiteVisitor.xml` - Example BAS project file (validates successfully)
- `translate.js` - JavaScript translation utilities

## Repository Structure Reference

### Root Directory Contents
```
.
├── HDGRACE_2025-09-07.py          # Main generator script
├── 읽고 -꼭 100% 반영.txt           # Core requirements (Korean)
├── 124개기능.txt                   # 124 feature specifications
├── 기존+추가UI버튼_이모지를_큰_카테고리_별로_.txt  # UI specifications
├── 누락-기능/                      # 58 missing feature files
├── SiteVisitor.xml                 # Example BAS project
├── modules.zip                     # BAS modules archive
├── translate.js                    # Translation utilities
└── [많은 한국어 텍스트 파일들]         # Various Korean documentation
```

### File Sizes for Reference
- `HDGRACE_2025-09-07.py`: 13KB Python script
- Generated XML: ~25-27MB output file
- `modules.zip`: 12MB multi-part archive
- Korean text files: Range from 20KB to 30MB

### Key Directories Created During Build
- `C:\Users\office2\Pictures\Desktop\3065\valid/` - Output directory (Windows path on Linux)
- `temp_repos/` - GitHub repository cloning directory (placeholder)

## CRITICAL Timing and Timeout Information

### Build Times (NEVER CANCEL)
- **Normal execution**: 6.8 seconds ±0.1 seconds
- **Set timeout to**: Minimum 30 seconds, recommended 60 seconds
- **XML prettifying phase**: Takes 5+ seconds of the total time
- **If build appears stuck**: Wait minimum 30 seconds before investigating

### Performance Characteristics
- Generates 312,630 actions in ~0.4 seconds
- Generates 3,065 UI elements in ~0.004 seconds  
- XML prettifying and file writing: ~5.5 seconds
- Memory usage: Peaks during XML generation phase

## Module Import and Testing

### Import as Module
```python
import importlib.util
spec = importlib.util.spec_from_file_location('hdgrace', 'HDGRACE_2025-09-07.py')
module = importlib.util.module_from_spec(spec)
spec.loader.exec_module(module)
# Access Config class: module.Config
```

### Configuration Access
- BAS Versions: `["29.1.0", "29.2.0"]`
- Minimum functions: `3065`
- Minimum actions: `300000`
- Target precision: `0.00000000001`

## Quality Assurance Checklist

Before committing changes:
1. Run `python3 -m py_compile HDGRACE_2025-09-07.py` - Must complete without errors
2. Execute full build: `python3 HDGRACE_2025-09-07.py` - Must complete in ~7 seconds
3. Validate XML structure with Python XML parser
4. Verify function count ≥ 3,065 and action count ≥ 300,000
5. Check that all output files are generated
6. Review logs for any new error messages beyond expected warnings

## Clean-Up and Git Hygiene
- Generated files are in `.gitignore` and should not be committed
- Remove `__pycache__/` and generated output directories before commits
- Windows-style paths in filenames are expected behavior, not errors