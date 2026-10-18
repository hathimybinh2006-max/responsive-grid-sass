# [Bài tập] Tái cấu trúc mã CSS cho sẵn (Responsive Grid)

Mã nguồn được tái cấu trúc từ repository gốc: [codegym-vn/responsive-grid](https://github.com/codegym-vn/responsive-grid)

## Mục tiêu tái cấu trúc
- Chuyển đổi toàn bộ CSS trong thẻ `<style>` và các đoạn **inline style** dày đặc trong HTML gốc thành kiến trúc **SASS/SCSS chuẩn hóa 7-1 pattern**.
- Sử dụng **Biến (Variables)** để quản lý bảng màu, chiều cao và số cột.
- Sử dụng **Mixins** để tính toán tự động độ rộng của cột (`@mixin col-width`) và định dạng khối widget (`@mixin block-style`).
- Áp dụng phương pháp đặt tên **BEM** (`.gridwrapper--header`, `.gridcontent--sidebar`, `.widget-item--full`...) giúp HTML sạch sẽ, dễ bảo trì.

---

## Cấu trúc thư mục dự án
```text
responsive-grid-sass/
├── index.html                   ← File HTML mới sạch sẽ, không còn inline styles
├── responsive_grid.htm          ← File HTML gốc ban đầu (để đối chiếu)
├── css/
│   └── style.css                ← File CSS hoàn chỉnh được biên dịch từ SASS
├── scss/
│   ├── main.scss                ← File SCSS gốc tổng hợp các module
│   ├── abstracts/
│   │   ├── _variables.scss      ← Biến màu sắc, kích thước, hệ thống 12 cột
│   │   └── _mixins.scss         ← Mixin tính độ rộng cột và style khối
│   ├── base/
│   │   └── _reset.scss          ← Reset box-sizing, font, body
│   ├── layout/
│   │   └── _grid.scss           ← Hệ thống 12 cột grid, wrappers, columns
│   └── components/
│       └── _widgets.scss        ← Các khối widget bên trong sidebar
└── README.md
```

---

## Bảng so sánh trước và sau khi tái cấu trúc

| Đặc điểm | Mã nguồn gốc | Sau khi tái cấu trúc với SASS |
|---|---|---|
| **Vị trí CSS** | Trộn lẫn trong thẻ `<style>` và viết trực tiếp `style="..."` ở từng thẻ `<div>` | Tách biệt hoàn toàn, tổ chức thành các partial SCSS theo thư mục |
| **Quản lý kích thước cột** | Viết cứng `width: 8.33%`, `width: 25%`, `width: 100%` | Mixin `@include col-width(3)` tự tính toán: `(3 / 12) * 100% = 25%` |
| **Quản lý màu sắc** | Rải rác mã màu `#9933cc`, `#0099cc`, `#33b5e5` | Tập trung tại `_variables.scss` (`$color-header`, `$color-footer`...) |
| **Class name** | Chung chung (`.gridwrapper`, `.gridcontent`), phụ thuộc inline style | Chuẩn BEM rõ nghĩa: `.gridwrapper--main`, `.gridcontent--sidebar` |

---

## Cách biên dịch SASS
Cài đặt sass và biên dịch:
```bash
npm install -g sass
sass scss/main.scss css/style.css
```
Hoặc watch khi phát triển:
```bash
sass --watch scss/main.scss:css/style.css
```
