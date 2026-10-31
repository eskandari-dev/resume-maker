---
name: track-application
description: Move a submitted application from Ready To Apply/<company-name>/<position> into Applied. Use when the user says they applied or submitted, or asks to track, archive, or move an application into Applied.
---

# Track a submitted application

Move one submitted application from `Ready To Apply` into `Applied`. Keep the company folder, position folder, and files inside it.

## Resolve the source

Use the path the user gives. It must be a position folder:

```
Ready To Apply/<company-name>/<position>
```

If they name the company and position instead of a path, build that path. Slug each name: replace `&` with `and`; turn slashes, backslashes, `|`, `:`, and whitespace into a single hyphen; remove `* ? " < >`; collapse repeated hyphens and trim hyphens from the ends. If several folders match, list them and ask which one to move.

## Move

Run this from the repository root. Quote paths, because `Ready To Apply` contains a space.

```powershell
$source = "Ready To Apply/<company-name>/<position>"
$destParent = "Applied/<company-name>"
$dest = Join-Path $destParent "<position>"
if (-not (Test-Path -LiteralPath $source -PathType Container)) { throw "Source folder not found: $source" }
if (Test-Path -LiteralPath $dest) { throw "Already tracked: $dest" }
New-Item -ItemType Directory -Force -Path $destParent | Out-Null
Move-Item -LiteralPath $source -Destination $destParent
$companyDir = Split-Path $source -Parent
if ((Get-ChildItem -LiteralPath $companyDir -Force | Measure-Object).Count -eq 0) {
  Remove-Item -LiteralPath $companyDir
}
```

Do not copy, delete files inside the position folder, or change the resume or cover letter.

If the source is missing or the destination already exists, stop and report the path. Do not merge folders.

## Done

Confirm the new path:

```
Applied/<company-name>/<position>
```
