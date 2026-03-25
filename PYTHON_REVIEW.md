# Python Scripts Security & Best Practices Review

**Review Date:** January 31, 2026  
**Scripts Reviewed:** 7 maintenance utility scripts in `skills/ideaverse-maintenance/scripts/`

---

## Executive Summary

The scripts are generally well-written with good defensive programming practices. **No critical security vulnerabilities were found.** However, there are several best practices improvements and refactoring opportunities that would improve code quality, maintainability, and consistency.

---

## Critical Issues
**None identified.** All scripts properly validate file paths and handle errors gracefully.

---

## High Priority Issues

### 1. **Manual Argument Parsing (All Scripts Except vault_utils.py)**

**Impact:** Maintainability, consistency, proper error handling  
**Severity:** High

**Files Affected:**
- `check_frontmatter.py`
- `detect_moc_bloat.py`
- `find_broken_links.py`
- `find_orphans.py`
- `suggest_archival.py`
- `validate_squeeze_points.py`

**Current Implementation:**
```python
def get_args():
    args = {
        'vault_path': Path.cwd(),
        'strict': False,
        'json_output': False
    }
    
    positional = []
    i = 1
    while i < len(sys.argv):
        arg = sys.argv[i]
        if arg == '--strict':
            args['strict'] = True
            i += 1
        # ... more manual parsing
    return args
```

**Problems:**
- Manual parsing is error-prone and doesn't provide `--help` automatically
- Inconsistent argument handling across scripts
- No validation that arguments are valid
- Difficult to maintain when adding new arguments

**Recommendation:**
Replace with `argparse` from Python standard library:
```python
import argparse

def get_args():
    parser = argparse.ArgumentParser(
        description='Check for missing frontmatter properties in notes.'
    )
    parser.add_argument(
        'vault_path',
        nargs='?',
        type=Path,
        default=Path.cwd(),
        help='Path to vault (default: current directory)'
    )
    parser.add_argument(
        '--strict',
        action='store_true',
        help='Check MOCs for required "in" property'
    )
    parser.add_argument(
        '--json',
        action='store_true',
        dest='json_output',
        help='Output results as JSON'
    )
    return parser.parse_args()
```

**Benefits:**
- Automatic `--help` flag
- Better error messages for invalid arguments
- More Pythonic and maintainable
- Consistent across all scripts

---

## Medium Priority Issues

### 2. **Regex Pattern Duplication**

**Impact:** Maintainability, consistency  
**Severity:** Medium

**Files Affected:**
- `check_frontmatter.py` (line: custom YAML parsing)
- `detect_moc_bloat.py` (wikilink pattern)
- `find_broken_links.py` (wikilink pattern)
- `find_orphans.py` (wikilink pattern)
- `suggest_archival.py` (wikilink pattern)
- `validate_squeeze_points.py` (wikilink pattern)

**Current Implementation:**
```python
# In multiple files
pattern = r'\[\[([^\]|]+)(?:\|[^\]]+)?\]\]'
```

**Recommendation:**
Define wikilink constant in `vault_utils.py`:
```python
# In vault_utils.py
WIKILINK_PATTERN = r'\[\[([^\]|]+)(?:\|[^\]]+)?\]\]'

def extract_wikilinks(content: str) -> List[str]:
    """Extract all wikilinks from content."""
    links = []
    for match in re.finditer(WIKILINK_PATTERN, content):
        links.append(match.group(1).strip())
    return links
```

Then import and use across all scripts:
```python
from vault_utils import extract_wikilinks
```

**Benefits:**
- Single source of truth
- Easier to update regex if needed
- Consistent behavior across scripts
- Reduces code duplication

---

### 3. **Hardcoded Root Notes List**

**Impact:** Maintainability  
**Severity:** Medium

**Files Affected:**
- `check_frontmatter.py` (line 97)
- `find_orphans.py` (line 61)

**Current Implementation:**
```python
root_notes = {'Home', 'Home Basic', 'Ideaverse Map'}
```

**Recommendation:**
Move to `vault_utils.py` as a constant:
```python
# In vault_utils.py
ROOT_NOTES = {'Home', 'Home Basic', 'Ideaverse Map'}
```

This allows centralized updates when new root notes are added.

---

### 4. **Exception Handling Too Broad**

**Impact:** Debugging, error visibility  
**Severity:** Medium

**Files Affected:**
- `check_frontmatter.py` (line 154)
- `suggest_archival.py` (line 140)
- `validate_squeeze_points.py` (line 186)

**Current Implementation:**
```python
except Exception as e:
    issues.append({
        'path': str(md_file.relative_to(vault_path)),
        'issue': f'read error: {e}',
        'severity': 'error'
    })
```

**Problems:**
- Catches too many exception types, including programming errors
- Makes debugging harder
- Could mask unexpected errors

**Recommendation:**
Catch specific exceptions:
```python
except (IOError, OSError, UnicodeDecodeError) as e:
    issues.append({
        'path': str(md_file.relative_to(vault_path)),
        'issue': f'read error: {e}',
        'severity': 'error'
    })
```

---

### 5. **Missing Type Hints**

**Impact:** Code clarity, IDE support, maintainability  
**Severity:** Medium

**Files Affected:** All scripts except `vault_utils.py`

**Current:**
```python
def parse_frontmatter(content):
    """Extract YAML frontmatter as dict."""
```

**Recommendation:**
```python
from typing import Dict, List, Optional

def parse_frontmatter(content: str) -> Optional[Dict[str, any]]:
    """Extract YAML frontmatter as dict."""
```

Benefits:
- Better IDE autocompletion
- Clearer function contracts
- Easier to catch type errors
- Self-documenting code

---

## Low Priority Issues

### 6. **Naive YAML Parsing in check_frontmatter.py**

**Impact:** Robustness  
**Severity:** Low

**Issue:**
The custom YAML parser (lines 42-77) is simplified and may not handle all YAML edge cases correctly (quoted strings, nested structures, special characters).

**Current Approach:**
```python
def parse_frontmatter(content):
    # Custom regex-based YAML parsing
    match = re.match(r'^(\w+):\s*(.*)', line)
```

**Recommendation:**
While using the full `pyyaml` library would add a dependency, the current implementation is acceptable since:
1. The vault's YAML is simple and well-formed
2. The script degrades gracefully with try-except
3. It avoids external dependencies per the design goal

**Alternative:** If robustness becomes an issue, consider `PyYAML` library with security parsing:
```python
import yaml
props = yaml.safe_load(frontmatter)  # Much safer than unsafe_load
```

---

### 7. **Exit Code Logic in detect_moc_bloat.py**

**Impact:** Script behavior  
**Severity:** Low

**Issue (Line 100):**
```python
sys.exit(1 if any(r['status'] == 'bloated' for r in results) else 0)
```

This exits with code 1 only if bloated MOCs are found, not for warnings. This is correct for CI/CD but could be documented.

**Recommendation:**
Add comment explaining exit code behavior:
```python
# Exit with 1 if bloat found (for CI/CD integration), 0 for warning only
sys.exit(1 if any(r['status'] == 'bloated' for r in results) else 0)
```

---

### 8. **Inconsistent Output Formatting**

**Impact:** User experience  
**Severity:** Low

**Issue:**
Different scripts use different emoji/formatting for severity levels:

- `detect_moc_bloat.py`: 🔴, 🟡 (circles)
- `suggest_archival.py`: 🔴, 🟡, 🟢 (circles)
- `validate_squeeze_points.py`: 📍 (pin)

**Recommendation:**
Create a constants file or utility for consistent output formatting:
```python
# In vault_utils.py
class OutputFormat:
    HIGH = "🔴 High"
    MEDIUM = "🟡 Medium"  
    LOW = "🟢 Low"
    INFO = "ℹ️ Info"
```

---

### 9. **Unused Import in suggest_archival.py**

**Impact:** Code cleanliness  
**Severity:** Low

**Issue (Line 10):**
```python
import os  # Imported but never used
```

**Recommendation:**
Remove unused imports.

---

### 10. **String Interpolation Consistency**

**Impact:** Code style  
**Severity:** Low

**Issue:**
Mix of f-strings and `.format()` across scripts. Python best practice is f-strings.

**Current Example (vault_utils.py line 24):**
```python
submodule_patterns.append(f'{submodule_path}/**')  # f-string (good)
```

Some scripts consistently use f-strings (good), but it's worth auditing all for consistency.

---

## Security Analysis

### ✅ No Critical Vulnerabilities Found

**Positive Security Practices:**

1. **Proper Path Validation**
   - `file_path.relative_to(vault_root)` prevents directory traversal
   - Graceful handling of files outside vault
   ```python
   try:
       rel_path = str(file_path.relative_to(vault_root))
   except ValueError:
       return False  # File outside vault
   ```

2. **Safe File Operations**
   - All file reads use context managers
   - `encoding='utf-8'` specified (prevents encoding issues)
   - Exception handling around file operations

3. **Input Validation**
   - Vault path existence checked before processing
   - File paths normalized before pattern matching
   - Regex patterns use standard library `fnmatch` (safe)

4. **No Command Injection Risks**
   - No `subprocess`, `os.system()`, or shell execution
   - All operations use Path objects and standard library

5. **No Data Exposure**
   - Error messages don't leak sensitive paths
   - JSON output handles special characters safely

---

## Recommendations Summary

| Priority | Issue | Fix Time | Impact |
|----------|-------|----------|--------|
| High | Use `argparse` for CLI args | 30-45 min | Maintainability, consistency |
| Medium | Extract wikilink regex pattern | 15 min | DRY principle, maintainability |
| Medium | Move hardcoded constants to vault_utils | 10 min | Maintainability |
| Medium | Specify exception types | 15 min | Debugging, clarity |
| Medium | Add type hints to all scripts | 30-45 min | Code clarity, IDE support |
| Low | Remove unused imports | 5 min | Code cleanliness |
| Low | Consistent output formatting | 20 min | User experience |
| Low | Document exit code behavior | 5 min | Clarity |

---

## Testing Recommendations

### Unit Tests to Add

1. **Path filtering logic** (vault_utils.py)
   ```python
   def test_is_vault_content_filters_node_modules()
   def test_is_vault_content_filters_git_submodules()
   def test_gitignore_patterns_loading()
   ```

2. **Regex patterns**
   ```python
   def test_wikilink_extraction_valid_links()
   def test_wikilink_extraction_with_aliases()
   def test_wikilink_extraction_ignores_broken_syntax()
   ```

3. **Frontmatter parsing**
   ```python
   def test_parse_frontmatter_valid_yaml()
   def test_parse_frontmatter_missing_frontmatter()
   def test_parse_frontmatter_with_lists()
   ```

### Script Testing

Run each script on test vault:
```bash
cd skills/ideaverse-maintenance/scripts
./check_frontmatter.py ../../..
./detect_moc_bloat.py ../../..
./find_broken_links.py ../../..
./find_orphans.py ../../..
./suggest_archival.py ../../..
./validate_squeeze_points.py ../../..
```

Verify:
- No errors on valid vault
- Proper output format
- JSON output valid
- Return codes correct

---

## Implementation Status

### ✅ Completed

**High Priority:**
- [x] Replaced manual argument parsing with `argparse` in all 6 scripts
- [x] Extracted `extract_wikilinks()` and `extract_wikilinks_set()` to `vault_utils.py`
- [x] Moved `ROOT_NOTES` constant to `vault_utils.py`
- [x] Added `WIKILINK_PATTERN` constant to `vault_utils.py`

**Medium Priority:**
- [x] Specified exception types (`IOError`, `OSError`, `UnicodeDecodeError`) instead of broad `Exception` catches
- [x] Removed unused `import os` from `suggest_archival.py`

All scripts now:
- Use `argparse` with automatic `--help` support
- Share common utilities via `vault_utils.py`
- Have consistent error handling
- Are more maintainable and easier to extend

---

## Conclusion

The scripts demonstrate good defensive programming with:
- ✅ Proper error handling
- ✅ Path validation and security
- ✅ No external dependency bloat
- ✅ Clear, documented logic
- ✅ DRY principle applied (shared utilities)
- ✅ Consistent argument parsing via argparse

**Status:** All practical, non-overengineering improvements have been implemented.

