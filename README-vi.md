<div align="center">

# 📄 Modular LaTeX CV

**Hệ thống CV LaTeX có cấu trúc module, hỗ trợ tạo nhiều phiên bản CV cho từng vị trí ứng tuyển.**
Viết một lần, tuỳ chỉnh cho mọi công việc — tất cả trong một repository duy nhất.

[![LaTeX](https://img.shields.io/badge/LaTeX-pdflatex-008080?style=for-the-badge&logo=latex&logoColor=white)](https://www.latex-project.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

[English](README.md)

</div>

---

## Mục Lục

- [Tại Sao Dùng Template Này](#tại-sao-dùng-template-này)
- [Cấu Trúc Thư Mục](#cấu-trúc-thư-mục)
- [Cách Hoạt Động](#cách-hoạt-động)
- [Bắt Đầu](#bắt-đầu)
- [Tạo CV Cho Vị Trí Cụ Thể](#tạo-cv-cho-vị-trí-cụ-thể)
- [Sử Dụng Trên Overleaf](#sử-dụng-trên-overleaf)
- [Tác Giả](#tác-giả)
- [Giấy Phép](#giấy-phép)

---

## Tại Sao Dùng Template Này

| Vấn đề | Giải pháp |
|---|---|
| Copy nguyên file `.tex` cho mỗi lần ứng tuyển | Thư mục `base/` dùng chung — sửa một lần, áp dụng mọi nơi |
| Quên cập nhật nội dung trên nhiều bản CV | Các role import trực tiếp từ `base/`, thay đổi tự động lan truyền |
| Thư mục lộn xộn với nhiều file PDF rời rạc | Mỗi vị trí có thư mục riêng trong `role/`, giữ các phiên bản gọn gàng |

---

## Cấu Trúc Thư Mục

```text
nvminh162-cv-latex/
├── base/                          # Nội dung CV chung (nguồn dữ liệu duy nhất)
│   ├── main.tex                   # File entry point chính
│   ├── preamble.tex               # Packages, page geometry, fonts
│   ├── commands.tex               # Các lệnh & môi trường LaTeX tuỳ chỉnh
│   └── sections/
│       ├── header.tex             # Tên, chức danh, thông tin liên hệ
│       ├── summary.tex            # Tóm tắt chuyên môn
│       ├── education.tex          # Học vấn
│       ├── skills.tex             # Kỹ năng kỹ thuật
│       ├── projects.tex           # Dự án nổi bật
│       ├── experience.tex         # Kinh nghiệm làm việc
│       └── awards.tex             # Giải thưởng & chứng chỉ
│
├── role/                          # Các phiên bản CV theo vị trí
│   └── intern-frontend-developer-aipower/
│       ├── main.tex               # Import từ ../../base/, override cục bộ
│       └── sections/
│           └── header.tex         # Header riêng cho vị trí này
│
├── projects/                      # Mã nguồn dự án đầy đủ (submodule / tham chiếu)
│
├── README.md                      # Tài liệu tiếng Anh
├── README-vi.md                   # Tài liệu tiếng Việt
└── LICENSE
```

### Thư Mục Chính

| Thư mục | Mục đích |
|---|---|
| `base/` | CV gốc — toàn bộ nội dung dùng chung nằm ở đây. Build trực tiếp để có PDF tổng quát. |
| `role/<tên-vị-trí>/` | Bản fork nhẹ, import phần lớn section từ `base/` và chỉ override phần khác biệt (VD: tiêu đề header, summary, danh sách project). |
| `projects/` | Các repository dự án được tham chiếu trong phần Projects của CV. |

---

## Cách Hoạt Động

```text
base/                          role/intern-frontend-developer-aipower/
├── preamble.tex    ◄──────────── \input{../../base/preamble}
├── commands.tex    ◄──────────── \input{../../base/commands}
├── sections/
│   ├── header.tex                 sections/header.tex  ← Override CỤC BỘ
│   ├── summary.tex ◄──────────── \input{../../base/sections/summary}
│   ├── skills.tex  ◄──────────── \input{../../base/sections/skills}
│   ├── projects.tex◄──────────── \input{../../base/sections/projects}
│   └── awards.tex  ◄──────────── \input{../../base/sections/awards}
```

> **Cơ chế override:** Muốn tuỳ chỉnh section nào cho vị trí cụ thể, tạo bản copy cục bộ trong `role/<vị-trí>/sections/` rồi đổi đường dẫn `\input` trong `main.tex` của role đó. Các section còn lại vẫn lấy từ `base/`.

---

## Bắt Đầu

### Yêu Cầu

- **TeX distribution** — [MiKTeX](https://miktex.org) (Windows) hoặc [TeX Live](https://tug.org/texlive/) (đa nền tảng)
- **pdflatex** — đã bao gồm trong cả hai distribution trên

### Build CV Gốc

```powershell
cd base
pdflatex main.tex
```

Kết quả: `base/main.pdf`

### Build CV Cho Vị Trí Cụ Thể

```powershell
cd role/intern-frontend-developer-aipower
pdflatex main.tex
```

Kết quả: `role/intern-frontend-developer-aipower/main.pdf`

---

## Tạo CV Cho Vị Trí Cụ Thể

1. **Tạo thư mục role mới:**

    ```powershell
    mkdir role/backend-engineer-ten-cong-ty/sections
    ```

2. **Tạo `main.tex`** import từ `base/`:

    ```latex
    \input{../../base/preamble}
    \input{../../base/commands}

    \begin{document}

    \input{sections/header}              % ← override cục bộ
    \input{../../base/sections/summary}
    \input{../../base/sections/education}
    \input{../../base/sections/skills}
    \input{../../base/sections/projects}
    \input{../../base/sections/awards}

    \end{document}
    ```

3. **Tạo `sections/header.tex`** với chức danh riêng:

    ```latex
    \begin{center}
        {\fontsize{25}{28}\selectfont\bfseries NGUYEN VAN MINH}\\[4pt]
        {\large\bfseries Backend Engineer}\\[6pt]
        (+84) 353 999 798 \;|\; ...
    \end{center}
    ```

4. **Override thêm section khác** nếu cần — copy file từ `base/sections/`, chỉnh sửa, rồi cập nhật đường dẫn `\input`.

---

## Sử Dụng Trên Overleaf

1. Upload toàn bộ repository dưới dạng file ZIP.
2. Đặt main document là `base/main.tex` (hoặc `role/<vị-trí>/main.tex` tuỳ mục đích).
3. Recompile.

> **Lưu ý:** Không compile trực tiếp các file section riêng lẻ (VD: `sections/projects.tex`) — chúng là các fragment, không phải document độc lập.

---

## Tác Giả

<div align="center">

| Thông tin | Giá trị |
|---|---|
| **Họ tên** | Nguyễn Văn Minh |
| **GitHub** | [@nvminh162](https://github.com/nvminh162) |
| **Website** | [nvminh162.id.vn](https://nvminh162.id.vn) |
| **Email** | [nvminh162@gmail.com](mailto:nvminh162@gmail.com) |

</div>

---

## Giấy Phép

Dự án được cấp phép theo **MIT License** — xem file [LICENSE](LICENSE) để biết chi tiết.

---

<div align="center">

**Được xây dựng với ❤️ và LaTeX**

</div>
