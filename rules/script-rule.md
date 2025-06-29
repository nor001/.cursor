# Script & Automation Development Rules

## 🎯 MANDATORY ACTIVATION MARKER

**ACTIVATION MARKER**: [script]

## ⚡ ULTRA-DIRECT PROTOCOL

**For scripts, batch files, shell, AutoHotkey, or standard automations:**

### Core Principles
- ✅ **Create and save the final file directly** on the first call
- ✅ **Do not perform intermediate validations** unless destructive or critical
- ✅ **Do not iterate on syntax** unless explicitly requested
- ✅ **Choose the simplest and most universal** approach
- ❌ **Do not ask about format, name, or location** unless ambiguous

### When to Execute Directly (90% of cases)
- ✅ **File operations** - create, copy, move, delete
- ✅ **Text processing** - search, replace, format
- ✅ **System automation** - scheduled tasks, monitoring
- ✅ **Data conversion** - CSV to JSON, format changes
- ✅ **Utility scripts** - backup, cleanup, organization
- ✅ **Simple calculations** - math operations, reports

### When to Ask (10% of cases)
- ❌ **System-critical operations** - registry changes, service modifications
- ❌ **Data destruction** - permanent deletion, overwriting important files
- ❌ **Security-sensitive** - password handling, encryption operations
- ❌ **Network operations** - external API calls, data transmission

---

## 📋 SCRIPT TYPE PATTERNS

### Batch Files (Windows)
```batch
@echo off
REM Simple, direct, no error checking unless critical
REM Use built-in commands, avoid external dependencies

setlocal EnableDelayedExpansion

REM Direct action pattern
if exist "%~1" (
    echo Processing: %~1
    REM Process directly
) else (
    echo File not found: %~1
    exit /b 1
)

endlocal
```

### PowerShell Scripts
```powershell
# Direct execution pattern
# Use built-in cmdlets, avoid complex error handling unless critical

param(
    [string]$InputFile,
    [string]$OutputFile
)

# Direct processing
if (Test-Path $InputFile) {
    Get-Content $InputFile | ForEach-Object {
        # Process each line directly
        $_ | Out-File -Append $OutputFile
    }
} else {
    Write-Error "File not found: $InputFile"
    exit 1
}
```

### Shell Scripts (Linux/macOS)
```bash
#!/bin/bash
# Simple, direct, POSIX-compatible where possible
# Use built-in commands, minimal error checking

INPUT_FILE="$1"
OUTPUT_FILE="$2"

# Direct processing
if [ -f "$INPUT_FILE" ]; then
    while IFS= read -r line; do
        echo "$line" >> "$OUTPUT_FILE"
    done < "$INPUT_FILE"
else
    echo "File not found: $INPUT_FILE" >&2
    exit 1
fi
```

### AutoHotkey Scripts
```autohotkey
; Direct automation pattern
; Simple key mappings and window automation
; Avoid complex logic unless specifically requested

#NoEnv
#SingleInstance Force

; Direct hotkey mappings
F1::
    Send, Hello World{Enter}
return

; Window automation - direct and simple
^j::
    WinActivate, Notepad
    Send, ^a
    Send, This is automated text
return
```

### Python Scripts (Simple Automation)
```python
#!/usr/bin/env python3
# Simple, direct, minimal dependencies
# Use standard library, avoid complex patterns

import sys
import os
from pathlib import Path

def main():
    if len(sys.argv) < 2:
        print("Usage: script.py <input_file>")
        sys.exit(1)
    
    input_file = Path(sys.argv[1])
    
    # Direct processing
    if input_file.exists():
        with open(input_file, 'r') as f:
            for line in f:
                print(line.strip())
    else:
        print(f"File not found: {input_file}")
        sys.exit(1)

if __name__ == "__main__":
    main()
```

---

## 🔧 UTILITY AUTOMATION PATTERNS

### File Processing Template
```bash
#!/bin/bash
# Universal file processing template
# Works for most file operations

process_files() {
    local input_dir="$1"
    local output_dir="$2"
    
    # Create output directory if needed
    mkdir -p "$output_dir"
    
    # Process each file directly
    for file in "$input_dir"/*; do
        if [ -f "$file" ]; then
            basename_file=$(basename "$file")
            # Direct processing
            cp "$file" "$output_dir/$basename_file"
        fi
    done
}
```

### Cross-Platform Script Template
```bash
#!/bin/bash
# Cross-platform compatibility
# Detect OS and adjust accordingly

detect_os() {
    case "$(uname -s)" in
        Linux*)     echo "linux" ;;
        Darwin*)    echo "mac" ;;
        CYGWIN*|MINGW*) echo "windows" ;;
        *)          echo "unknown" ;;
    esac
}

OS=$(detect_os)

case "$OS" in
    "linux"|"mac")
        # Unix-like operations
        ls -la
        ;;
    "windows")
        # Windows operations
        dir
        ;;
esac
```

### Scheduled Task Template
```bash
#!/bin/bash
# Simple scheduled task template
# No complex logging unless requested

LOG_FILE="/tmp/script.log"

# Direct execution with minimal logging
{
    echo "$(date): Starting task"
    
    # Main task - direct execution
    perform_main_task
    
    echo "$(date): Task completed"
} >> "$LOG_FILE"
```

---

## 📊 PERFORMANCE & EFFICIENCY

### Script Optimization Principles
- **Direct execution** - avoid unnecessary loops or checks
- **Minimal I/O** - reduce file operations where possible
- **Built-in functions** - use shell/language built-ins over external tools
- **Early exit** - fail fast on errors
- **Simple logic** - avoid complex conditionals

### Efficient Patterns
```bash
# ✅ GOOD: Direct and efficient
while IFS= read -r line; do
    echo "$line"
done < "$file"

# ❌ AVOID: Complex and slow
for line in $(cat "$file"); do
    echo "$line"
done
```

### Memory Efficiency
```python
# ✅ GOOD: Process line by line
def process_large_file(filename):
    with open(filename, 'r') as f:
        for line in f:
            yield line.strip()

# ❌ AVOID: Load entire file into memory
def process_large_file_bad(filename):
    with open(filename, 'r') as f:
        lines = f.readlines()
    return [line.strip() for line in lines]
```

---

## 🛡️ ERROR HANDLING (MINIMAL)

### Basic Error Handling
```bash
# Simple error handling - only for critical failures
command_that_might_fail() {
    if ! some_command; then
        echo "Error: Command failed" >&2
        exit 1
    fi
}

# Most scripts: let errors propagate naturally
set -e  # Exit on any error
```

### Error Handling Levels
1. **None** (default) - Let script fail naturally
2. **Basic** - Exit codes and simple messages
3. **Enhanced** - Only for critical/requested scripts

---

## 🎯 SCRIPT ACTIVATION

### Automatic Script Context Detection
```bash
# Detect script type from file extension or shebang
detect_script_context() {
    local file="$1"
    
    case "$file" in
        *.bat|*.cmd)    echo "batch" ;;
        *.ps1)          echo "powershell" ;;
        *.sh)           echo "shell" ;;
        *.ahk)          echo "autohotkey" ;;
        *.py)           echo "python" ;;
        *)              echo "generic" ;;
    esac
}
```

### Script Rule Activation Triggers
```bash
# Automatic triggers based on script context detection
@script-detected        # Activates script-rule.md
@batch-detected         # Activates batch-specific patterns
@shell-detected         # Activates shell-specific patterns
@automation-detected    # Activates automation patterns

# Manual triggers for specific script domains
@script-rules          # Force script rules activation
@automation-rules      # Force automation rules activation
@utility-rules         # Force utility rules activation
```

---

## 📝 DOCUMENTATION (MINIMAL)

### Script Documentation Rules
- **NO documentation** for simple, self-explanatory scripts
- **Inline comments** only for complex logic
- **Usage examples** only if the script has multiple parameters
- **Header comments** only for complex or shared scripts

### Minimal Documentation Template
```bash
#!/bin/bash
# Purpose: Brief one-line description
# Usage: script.sh input_file output_file
# Author: [Optional, only for shared scripts]

# [Rest of script - no additional comments unless complex]
```

---

## 🚀 FAST-TRACK EXECUTION RULES

### Validation Strategy
```bash
# ONLY validate for critical operations
function validate_critical_operation() {
    case "$1" in
        "delete_system_files"|"modify_registry"|"change_permissions")
            echo "CRITICAL: This operation requires confirmation"
            return 1
            ;;
        *)
            # Direct execution for standard operations
            return 0
            ;;
    esac
}
```

### Action Priority
1. **Single, direct action** - no questions, no validations
2. **Cross-platform compatibility** where possible
3. **Simple, maintainable code** - avoid complex patterns
4. **Minimal dependencies** - use built-in functions

---

> This rule contains all specific script and automation rules. It activates automatically when script context is detected or manually with the corresponding triggers.
