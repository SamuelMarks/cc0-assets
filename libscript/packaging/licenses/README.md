# Canonical SPDX License Registry

Standardized, authoritative legal text (`.txt`) and Rich Text Format (`.rtf`) files
for open-source, source-available, and proprietary licenses commonly bundled into LibScript native
installers (WiX `.msi`, Inno Setup `.exe`, NSIS `.exe`) are maintained in the companion
`../cc0-assets/libscript/packaging/licenses/` repository to keep this core framework codebase
focused exclusively on executable scripts and declarative configurations.

## Storage Location

`../cc0-assets/libscript/packaging/licenses/`

## File Manifest

| SPDX Identifier | Description | Text File | RTF File |
| :--- | :--- | :--- | :--- |
| `AGPL-3.0-only` | GNU Affero General Public License v3.0 | `AGPL-3.0-only.txt` | `AGPL-3.0-only.rtf` |
| `Apache-2.0` | Apache License 2.0 | `Apache-2.0.txt` | `Apache-2.0.rtf` |
| `BSD-2-Clause` | BSD 2-Clause "Simplified" License | `BSD-2-Clause.txt` | `BSD-2-Clause.rtf` |
| `BSD-3-Clause` | BSD 3-Clause "New" or "Revised" License | `BSD-3-Clause.txt` | `BSD-3-Clause.rtf` |
| `CC0-1.0` | Creative Commons Zero v1.0 Universal | `CC0-1.0.txt` | `CC0-1.0.rtf` |
| `GPL-2.0-only` | GNU General Public License v2.0 only | `GPL-2.0-only.txt` | `GPL-2.0-only.rtf` |
| `GPL-2.0-or-later` | GNU General Public License v2.0 or later | `GPL-2.0-or-later.txt` | `GPL-2.0-or-later.rtf` |
| `LGPL-2.1-only` | GNU Lesser General Public License v2.1 | `LGPL-2.1-only.txt` | `LGPL-2.1-only.rtf` |
| `LGPL-3.0-only` | GNU Lesser General Public License v3.0 | `LGPL-3.0-only.txt` | `LGPL-3.0-only.rtf` |
| `MIT` | MIT License | `MIT.txt` | `MIT.rtf` |
| `Python-2.0` | Python Software Foundation License 2.0 | `Python-2.0.txt` | `Python-2.0.rtf` |
| `RSALv2` | Redis Source Available License v2 | `RSALv2.txt` | `RSALv2.rtf` |
| `SSPL-1.0` | Server Side Public License v1 | `SSPL-1.0.txt` | `SSPL-1.0.rtf` |

## Maintenance & Generation Procedure

The `.txt` documents represent canonical license wording. The companion `.rtf` documents are generated
using strict POSIX shell line-by-line escaping for compatibility with native Windows Installer (WiX)
`ScrollableText` controls and RichEdit 2.0+ dialog viewports:

```sh
for txt in packaging/licenses/*.txt; do
  rtf="${txt%.txt}.rtf"
  printf '{tf1\ansi\deff0 {\fonttbl {\f0 Courier;}}\fs20
' > "$rtf"
  sed 's/\/\/g; s/{/\{/g; s/}/\}/g; s/$/\par/' "$txt" >> "$rtf"
  printf '}
' >> "$rtf"
done
```
