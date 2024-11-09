# PowerShell File Annotations

A simple PowerShell script that allows you to add and view annotations/notes for files in your directories.

## Features

- Add annotations to any file in your system
- View files with their annotations in directory listings
- Annotations are stored persistently in user's home directory
- Simple and intuitive commands

## Installation

1. Download `file-annotations.ps1`
2. Add the following line to your PowerShell profile (usually at `$PROFILE`):
```powershell
. path\to\file-annotations.ps1
```

## Usage

### Add annotation to a file
```powershell
tip "filename.txt" "This is an important document"
```

### List files with annotations
```powershell
lst
```
This will show all files in the current directory with their annotations (if any).

## Storage

Annotations are stored in `~/.file-annotations/` directory as JSON files. Each annotation is stored in a separate file named with a base64-encoded hash of the full file path.

## Requirements

- PowerShell 5.1 or later
- Windows, macOS, or Linux with PowerShell installed
