# Modular LaTeX CV Template

A modular LaTeX CV template with shared core content and easy profile-specific customization.

## Overview

- Keep reusable CV content in one place.
- Create multiple tailored CV versions without duplication.
- Update once and reuse across profiles.

## Structure

- `base/` for shared content and layout.
- `companies/` for profile-specific entry files and overrides.
- `output/` for generated PDF files.

## Local Build

Compile from the profile directory you want to build:

```powershell
cd base

pdflatex main.tex
```

```powershell
cd companies/<target-profile>

pdflatex main.tex
```

## Overleaf

1. Upload the full repository.
2. Set the main document to either `base/main.tex` or `companies/<target-profile>/main.tex`.
3. Recompile.

Do not compile included partial files directly (such as files in `sections/`).

## Create a New Profile

1. Create `companies/<new-profile>/`.
2. Add `companies/<new-profile>/main.tex`.
3. Reuse shared sections from `base/sections/`.
4. Add profile-specific overrides only when needed.

## Notes

This repository may contain sample CV content. Replace all personal and project details before using it for real applications.

## License

MIT License. See `LICENSE` for details.

## Author

- GitHub: `@nvminh162`
