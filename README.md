<div align="center">

# 📄 Modular LaTeX CV

**A scalable, role-based CV system built with LaTeX.**
Write once, tailor for every job — all from a single repository.

[![LaTeX](https://img.shields.io/badge/LaTeX-pdflatex-008080?style=for-the-badge&logo=latex&logoColor=white)](https://www.latex-project.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

[Tiếng Việt](README-vi.md)

</div>

---

## Table of Contents

- [Why This Template](#why-this-template)
- [Repository Structure](#repository-structure)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Creating a Role-Specific CV](#creating-a-role-specific-cv)
- [Using with Overleaf](#using-with-overleaf)
- [Author](#author)
- [License](#license)

---

## Why This Template

| Problem | Solution |
|---|---|
| Duplicating entire `.tex` files for each job application | A shared `base/` with reusable sections — edit once, apply everywhere |
| Forgetting to update a bullet point across multiple CVs | Role variants import directly from `base/`, so changes propagate automatically |
| Messy folder of unrelated PDF exports | Each role has its own directory under `role/`, keeping variants organized |

---

## Repository Structure

```text
nvminh162-cv-latex/
├── base/                          # Shared CV content & layout (single source of truth)
│   ├── main.tex                   # Base document entry point
│   ├── preamble.tex               # Packages, page geometry, fonts
│   ├── commands.tex               # Custom LaTeX commands & environments
│   └── sections/
│       ├── header.tex             # Name, title, contact info
│       ├── summary.tex            # Professional summary
│       ├── education.tex          # Education background
│       ├── skills.tex             # Technical skills
│       ├── projects.tex           # Project highlights
│       ├── experience.tex         # Work experience
│       └── awards.tex             # Awards & certifications
│
├── role/                          # Role-specific CV variants
│   └── intern-frontend-developer-aipower/
│       ├── main.tex               # Imports from ../../base/, overrides locally
│       └── sections/
│           └── header.tex         # Custom header for this role
│
├── projects/                      # Full project source repos (submodules / references)
│
├── README.md                      # English documentation
├── README-vi.md                   # Vietnamese documentation
└── LICENSE
```

### Key Directories

| Directory | Purpose |
|---|---|
| `base/` | The canonical CV — all shared content lives here. Build directly for a general-purpose PDF. |
| `role/<job-name>/` | A lightweight fork that imports most sections from `base/` and overrides only what differs (e.g., header title, summary, selected projects). |
| `projects/` | Supporting project repositories referenced in the CV's project section. |

---

## How It Works

```text
base/                          role/intern-frontend-developer-aipower/
├── preamble.tex    ◄──────────── \input{../../base/preamble}
├── commands.tex    ◄──────────── \input{../../base/commands}
├── sections/
│   ├── header.tex                 sections/header.tex  ← LOCAL override
│   ├── summary.tex ◄──────────── \input{../../base/sections/summary}
│   ├── skills.tex  ◄──────────── \input{../../base/sections/skills}
│   ├── projects.tex◄──────────── \input{../../base/sections/projects}
│   └── awards.tex  ◄──────────── \input{../../base/sections/awards}
```

> **Override pattern:** To customize any section for a specific role, create a local copy in `role/<job>/sections/` and change the `\input` path in that role's `main.tex`. All other sections continue to pull from `base/`.

---

## Getting Started

### Prerequisites

- **TeX distribution** — [MiKTeX](https://miktex.org) (Windows) or [TeX Live](https://tug.org/texlive/) (cross-platform)
- **pdflatex** — included with both distributions above

### Build the Base CV

```powershell
cd base
pdflatex main.tex
```

Output: `base/main.pdf`

### Build a Role-Specific CV

```powershell
cd role/intern-frontend-developer-aipower
pdflatex main.tex
```

Output: `role/intern-frontend-developer-aipower/main.pdf`

---

## Creating a Role-Specific CV

1. **Create a new role directory:**

    ```powershell
    mkdir role/backend-engineer-company-name/sections
    ```

2. **Create `main.tex`** that imports from `base/`:

    ```latex
    \input{../../base/preamble}
    \input{../../base/commands}

    \begin{document}

    \input{sections/header}              % ← local override
    \input{../../base/sections/summary}
    \input{../../base/sections/education}
    \input{../../base/sections/skills}
    \input{../../base/sections/projects}
    \input{../../base/sections/awards}

    \end{document}
    ```

3. **Create `sections/header.tex`** with the role-specific title:

    ```latex
    \begin{center}
        {\fontsize{25}{28}\selectfont\bfseries NGUYEN VAN MINH}\\[4pt]
        {\large\bfseries Backend Engineer}\\[6pt]
        (+84) 353 999 798 \;|\; ...
    \end{center}
    ```

4. **Override more sections** as needed — just copy the file from `base/sections/`, modify it, and update the `\input` path.

---

## Using with Overleaf

1. Upload the entire repository as a ZIP file.
2. Set the main document to `base/main.tex` (or the desired `role/<job>/main.tex`).
3. Recompile.

> **Note:** Do not compile individual section files (e.g., `sections/projects.tex`) directly — they are fragments, not standalone documents.

---

## Author

<div align="center">

| Field | Value |
|---|---|
| **Name** | Nguyen Van Minh |
| **GitHub** | [@nvminh162](https://github.com/nvminh162) |
| **Website** | [nvminh162.id.vn](https://nvminh162.id.vn) |
| **Email** | [nvminh162@gmail.com](mailto:nvminh162@gmail.com) |

</div>

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ and LaTeX**

</div>
