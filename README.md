# Modular LaTeX CV - NGUYEN VAN MINH

A modular LaTeX CV template with shared CV content and layout.

## Overview

- Keep CV content in one place.
- Update shared content from the `base/` directory.
- Generate the final PDF from the base document.

## Structure

- `base/` for CV content and layout.
- `output/` for generated PDF files.

## Local Build

Compile from the base directory:

```powershell
cd base

pdflatex main.tex
```

## Overleaf

1. Upload the full repository.
2. Set the main document to `base/main.tex`.
3. Recompile.

Do not compile included partial files directly (such as files in `sections/`).

## Notes

This repository may contain sample CV content. Replace all personal and project details before using it for real applications.

## License

MIT License. See `LICENSE` for details.

## Author

- GitHub: `@nvminh162`
