# Omniflow Marketing Kit — LaTeX Style Guide

## Overview

Semua marketing kit mengikuti struktur **4 halaman** (kecuali `master.tex`).  
Setiap modul punya file `.tex` sendiri di folder-nya masing-masing.

---

## 1. Preamble (Wajib, Jangan Diubah)

```latex
\documentclass[a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{xcolor}
\usepackage{tikz}
\usetikzlibrary{calc,positioning,shapes.geometric}
\usepackage{lmodern}
\usepackage{helvet}
\usepackage{hyperref}
\usepackage{microtype}
\usepackage{parskip}
\usepackage{eso-pic}
\usepackage{calc}
\usepackage{fancyhdr}

\geometry{a4paper,left=0mm,right=0mm,top=0mm,bottom=0mm,noheadfoot}
\setlength{\parindent}{0pt}
\setlength{\fboxsep}{6pt}           % ← PENTING: padding seragam semua kotak

\renewcommand{\familydefault}{\sfdefault}
\hypersetup{colorlinks=true,urlcolor=BluePrimary,hidelinks}
```

---

## 2. Brand Colors

| Nama | Hex | Penggunaan |
|---|---|---|
| `BluePrimary` | `#2563EB` | Aksen utama, judul fitur 1, CTA band, trust bar |
| `BlueDark` | `#1E3A8A` | Section title, stat label, judul 3-step card |
| `BlueLight` | `#60A5FA` | Teks footer sekunder |
| `BlueBg` | `#EFF6FF` | Latar kotak testimoni, stat card, 3-step card, pricing |
| `BlueMid` | `#DBEAFE` | Teks CTA band body, trust bar label |
| `TextDark` | `#1E293B` | Body text |
| `TextLight` | `#64748B` | Subtitle, label stat card, caption |
| `White` | `#FFFFFF` | Teks di atas latar gelap |
| `RedLight` | `#FEE2E2` | Latar pain-point header |
| `RedText` | `#B91C1C` | Teks pain-point header |

**Warna fitur grid (6 kolom, 3 baris):**

| Posisi | Warna |
|---|---|
| Fitur 1 | `BluePrimary` |
| Fitur 2 | `EmeraldPrimary` |
| Fitur 3 | `PurplePrimary` |
| Fitur 4 | `BlueDark` |
| Fitur 5 | `OrangePrimary` |
| Fitur 6 | `EmeraldDark` |

**Tag module di cover:** bebas, sesuaikan identitas modul. Contoh: `EmeraldPrimary` (HRIS, EMR, Habitat), `PurplePrimary` (Profilex, Vecta, AI), `TealPrimary` (Booking Engine), `OrangePrimary` (Event Ticketing).

---

## 3. Helper Macros

```latex
% Footer biru di bawah tiap halaman konten (page 2-4)
\newcommand{\compactfooter}{%
    \begin{tikzpicture}[remember picture,overlay]
        \fill[BluePrimary](current page.south west) rectangle ([yshift=1.8cm] current page.south east);
        \node[anchor=south,yshift=1.0cm,text width=19cm,align=center] at (current page.south) {%
            {\fontsize{8.5}{11}\selectfont\bfseries\color{White}
            omniflow.id \enspace\textcolor{BlueLight}{|}\enspace contact@omniflow.id \enspace\textcolor{BlueLight}{|}\enspace +62 821 2560 9413}%
        };
        \node[anchor=south,yshift=0.22cm,text width=19cm,align=center] at (current page.south) {%
            {\fontsize{7}{9}\selectfont\color{BlueMid}
            Jl.\ Letjen S.\ Parman No.\ 28, Grogol Petamburan, Jakarta Barat 11470
            \enspace\textcolor{BlueLight}{·}\enspace Senin--Jumat, 08.00--18.00 WIB}%
        };
    \end{tikzpicture}%
}

% Judul section dengan garis bawah biru
\newcommand{\sectiontitle}[1]{%
    \vspace{10pt}%
    {\fontsize{13}{16}\selectfont\bfseries\color{BlueDark} #1}\par\vspace{3pt}%
    {\color{BluePrimary}\hrule height 0.6pt}\par\vspace{8pt}%
}

% Header tiap halaman konten (page 2-4) — NAMA MODUL DIGANTI
\newcommand{\kitheader}{%
    \thispagestyle{fancy}
    \fancyhf{}
    \fancyhead[L]{\fontsize{7.5}{9}\selectfont\bfseries OMNIFLOW <NAMA> --- MARKETING KIT}
    \fancyhead[R]{\fontsize{7.5}{9}\selectfont omniflow.id}
}
```

> **⚠️ Ganti `<NAMA>`** di `\kitheader` dengan nama modul (contoh: `HRIS`, `CUSTOMERS`, `BOOKING ENGINE`).

---

## 4. Struktur Halaman

### Halaman 1 — Cover

```
┌─────────────────────────────────────┐
│  Latar gradien biru muda            │
│                                     │
│         [Logo Omniflow]             │
│      ┌──────────────────┐           │
│      │ MODULE: NAMA     │  (tag)    │
│      └──────────────────┘           │
│                                     │
│   Judul Utama Modul (20/24 bold)    │
│   Subtitle (11/15 TextLight)        │
│                                     │
│  ┌─────────┬─────────┬─────────┐    │
│  │ Stat 1  │ Stat 2  │ Stat 3  │    │
│  └─────────┴─────────┴─────────┘    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Cover box (deskripsi singkat) │  │
│  └───────────────────────────────┘  │
├─────────────────────────────────────┤
│  Footer biru (alamat, kontak)       │
└─────────────────────────────────────┘
```

**3 stat cards** di cover: angka besar (`\fontsize{22}{26}`) + label kecil.  
Contoh: `Foto+GPS` / `Absensi Wajah`.

**Cover box**: latar `BlueBg`, border `BluePrimary`, teks bold highlight diawal.

### Halaman 2 — Pain Points + Testimoni

```
\newpage
\newgeometry{left=14mm,right=14mm,top=10mm,bottom=12mm}
\kitheader
\compactfooter
\setlength{\parskip}{2pt}

\sectiontitle{KENAPA ... BUTUH ... ?}
(paragraf intro TextLight 9.5/13)

┌──────────────────┬──────────────────┐
│ KOLOM MERAH      │ KOLOM BIRU       │
│ (TANTANGAN...)   │ (... MENJAWAB)   │
│                  │                  │
│ • bold — desk    │ • bold — desk    │
│ • bold — desk    │ • bold — desk    │
│ ... (6 bullets)  │ ... (6 bullets)  │
└──────────────────┴──────────────────┘

┌──────────────────────────────────────┐
│ BAND BIRU (highlight statement)      │
└──────────────────────────────────────┘

\sectiontitle{APA KATA MEREKA?}
┌──────────────────┬──────────────────┐
│ Testimoni 1      │ Testimoni 2      │
│ (quote + nama)   │ (quote + nama)   │
└──────────────────┴──────────────────┘

\restoregeometry
```

**Pain points column**: header `RedLight` + `RedText`, bullets bold — deskripsi.  
**Solution column**: header `BluePrimary` + `White`, bullets bold — deskripsi.  
Masing-masing **6 bullets**, dipisah `\par\vspace{4pt}`.

**Highlight band**: `BluePrimary` colorbox penuh lebar, teks bold putih 1-2 kalimat.

**Testimoni**: 2 kolom `BlueBg` colorbox, quote italic `9.5/13`, nama bold `8.5/11`, role `8/10 TextLight`.

### Halaman 3 — Fitur Utama

```
\newpage
\newgeometry{left=14mm,right=14mm,top=10mm,bottom=12mm}
\kitheader
\compactfooter
\setlength{\parskip}{2pt}

\sectiontitle{FITUR UTAMA OMNIFLOW <NAMA>}
(paragraf intro TextLight 9.5/13)

┌──────────────────┬──────────────────┐
│ Fitur 1          │ Fitur 2          │  ← 3 baris × 2 kolom
│ (judul+4 bullet) │ (judul+4 bullet) │
├──────────────────┼──────────────────┤
│ Fitur 3          │ Fitur 4          │
├──────────────────┼──────────────────┤
│ Fitur 5          │ Fitur 6          │
└──────────────────┴──────────────────┘

┌──────────────────────────────────────┐
│ SEGERA HADIR: ... (band BlueBg)     │
└──────────────────────────────────────┘

\restoregeometry
```

**Setiap fitur** terdiri dari:
- **Title bar**: colorbox warna fitur, teks `\fontsize{10}{13}\bfseries\color{White}`, TANPA `\vspace` dalam.
- **Lead**: `\fontsize{9}{12}\color{TextDark}` — 1 kalimat pembuka.
- **4 bullets**: `\textbullet\ ...\par\vspace{2pt}` — deskripsi fitur.
- Setelah title bar: `\par\vspace{4pt}` (WAJIB `\par` sebelum `\vspace`!).

**Fitur layout per kolom:**
```latex
\noindent
\begin{minipage}[t]{0.485\textwidth}
    \colorbox{<WARNA>}{%
        \begin{minipage}{\dimexpr\textwidth-2\fboxsep\relax}
            {\fontsize{10}{13}\selectfont\bfseries\color{White} <NOMOR>. <JUDUL>}
        \end{minipage}}\par
    \vspace{4pt}
    {\fontsize{9}{12}\selectfont\color{TextDark}%
    <LEAD>.\par\vspace{3pt}
    \textbullet\ <bullet 1>\par\vspace{2pt}%
    \textbullet\ <bullet 2>\par\vspace{2pt}%
    \textbullet\ <bullet 3>\par\vspace{2pt}%
    \textbullet\ <bullet 4>}%%
\end{minipage}%
\hfill
\begin{minipage}[t]{0.485\textwidth}
    ... fitur berikutnya ...
\end{minipage}
```

Antar baris fitur: `\vspace{8pt}` + `\noindent` lagi.

**Coming soon**: `BlueBg` colorbox, bold judul "Segera Hadir:", daftar pisah `\textbullet`.

### Halaman 4 — Dampak + Trust + Testimoni + CTA

```
\newpage
\newgeometry{left=14mm,right=14mm,top=10mm,bottom=12mm}
\kitheader
\compactfooter
\setlength{\parskip}{2pt}

\sectiontitle{DAMPAK NYATA UNTUK ...}

┌──────────────┬──────────────┐
│ Stat Card 1  │ Stat Card 2  │  ← 2×2 grid
├──────────────┼──────────────┤
│ Stat Card 3  │ Stat Card 4  │
└──────────────┴──────────────┘

┌──────────────────────────────────────┐
│ TRUST BAR: AES-256 | 99.9% | ISO... │
└──────────────────────────────────────┘

\sectiontitle{APA KATA MEREKA?}
┌──────────────┬──────────────┐
│ Testimoni 3  │ Stat Besar   │
└──────────────┴──────────────┘

\sectiontitle{SIAP MULAI?}
┌──────────┬──────────┬──────────┐
│ 1. Pilih │ 2. WA+QR │ 3. Tim   │  ← fixed 4.7cm [c]
│ Modul    │          │ Setup    │
└──────────┴──────────┴──────────┘

┌──────────────────────────────────────┐
│ CTA BAND: Uji coba gratis...         │  ← BluePrimary
└──────────────────────────────────────┘

┌──────────────────────────────────────┐
│ PRICING BAND: Mulai Rp 20jt/tahun.. │  ← BlueBg
└──────────────────────────────────────┘

\pagestyle{empty}
\restoregeometry
\end{document}
```

**Impact stat cards (2×2 grid):**
```latex
\noindent
\begin{minipage}[t]{0.485\textwidth}
    \noindent\colorbox{BlueBg}{%
        \begin{minipage}[t][2.7cm][c]{\dimexpr\linewidth-2\fboxsep\relax}
            \centering
            {\fontsize{20}{24}\selectfont\bfseries\color{BluePrimary} <ANGKA>}\par\vspace{2pt}
            {\fontsize{9.5}{12}\selectfont\bfseries\color{BlueDark} <JUDUL>}\par\vspace{2pt}
            {\fontsize{8.5}{11}\selectfont\color{TextDark}<DESKRIPSI>}
        \end{minipage}}%
    \vspace{6pt}
    \noindent\colorbox{BlueBg}{%
        ... card 2 ...
    }%
\end{minipage}%
\hfill
\begin{minipage}[t]{0.485\textwidth}
    ... card 3 & 4 ...
\end{minipage}
```

> **Card height: `2.7cm [c]`** — semua 4 card tinggi seragam & konten center-vertikal.

**Trust bar:** `BluePrimary` colorbox, 4 kolom (`0.24\linewidth`), fixed height `1.25cm [c]`, `\centering`:
```
AES-256        |  99.9%        |  ISO 27001     |  24/7
Enkripsi Data  |  Selalu Online|  Keamanan...   |  Dukungan Ahli
```

**3-step CTA cards:** 3 kolom (`0.318\textwidth`), fixed height `4.7cm [c]`, `BlueBg` colorbox:
1. **Pilih Modul** — subtext deskriptif
2. **Kontak via WhatsApp** — QR code `1.7cm` + "Scan untuk chat cepat" + nomor
3. **Tim Kami Bantu Setup** — "Onboarding dipandu langsung tim Omniflow --- **gratis**, 2--4 minggu."

**CTA band (BluePrimary):**
```latex
{\setlength{\fboxsep}{10pt}\setlength{\fboxrule}{0pt}%
\noindent\colorbox{BluePrimary}{%
    \begin{minipage}{\dimexpr\textwidth-2\fboxsep\relax}
        \centering
        {\fontsize{13}{16}\selectfont\bfseries\color{White}
        <CTA HEADLINE>}\par\vspace{3pt}
        {\fontsize{9.5}{12}\selectfont\color{BlueMid}
        Uji coba gratis 30 hari \enspace\textbullet\enspace \textbf{Tim kami bantu setup \& migrasi} \enspace\textbullet\enspace Dukungan 24/7}\par\vspace{2pt}
        {\fontsize{9.5}{12}\selectfont\color{BlueLight}
        omniflow.id \enspace\textbullet\enspace contact@omniflow.id \enspace\textbullet\enspace +62 821 2560 9413}
    \end{minipage}}}
```

**Pricing band (BlueBg) — WAJIB SETELAH CTA BAND:**
```latex
\vspace{6pt}

{\setlength{\fboxsep}{8pt}\setlength{\fboxrule}{0pt}%
\noindent\colorbox{BlueBg}{%
    \begin{minipage}{\dimexpr\textwidth-2\fboxsep\relax}
        \centering
        {\fontsize{9}{12}\selectfont\bfseries\color{BluePrimary}
        Mulai Rp 20jt/tahun \enspace\textbullet\enspace Hanya 50\% di tahun ke-2 \enspace\textbullet\enspace Unlimited Users}\par\vspace{1pt}
        {\fontsize{8.5}{11}\selectfont\color{BlueDark}
        Semakin banyak modul, semakin hemat}\par\vspace{1pt}
        {\fontsize{8}{10}\selectfont\color{TextLight}
        Negotiable untuk kebutuhan khusus \enspace\textbullet\enspace Whitelabel \& Reseller tersedia}
    \end{minipage}}}
```

> **Urutan WAJIB**: CTA band → pricing band → `\restoregeometry` → `\end{document}`.  
> **HANYA SATU `\end{document}`** di akhir file.

---

## 5. Aturan Spacing (CRITICAL)

| Aturan | Kenapa |
|---|---|
| `\setlength{\fboxsep}{6pt}` global | Semua kotak padding seragam |
| **TIDAK BOLEH** `\vspace` di dalam colorbox/minipage | Dobel padding — `\fboxsep` udah cukup |
| **WAJIB** `\par` setelah `\end{minipage}}` sebelum `\vspace` | Tanpa `\par`, `\vspace` ditunda LaTeX & muncul di tempat salah |
| Title bar fitur: **TANPA** `\vspace` dalam | Hanya teks judul, `\fboxsep` kasih padding |
| Setelah title bar: `\par\vspace{4pt}` | Jarak konsisten title → lead |
| Lead → bullet pertama: `\par\vspace{3pt}` | Jarak konsisten (parskip 2pt + vspace 3pt = 5pt) |
| Antar bullet: `\par\vspace{2pt}` | 2pt spacing per bullet |
| Pain column gap: `\par\vspace{4pt}` | 6 bullets dalam kolom |
| Testimoni & stat card: **TANPA** inner `\vspace` | `\fboxsep` & fixed height `[c]` sudah cukup |
| Kolom sejajar: gunakan `[t][<H>][c]` dengan H seragam | Cegah kolom pendek "naik" sendiri |

---

## 6. Font Sizes

| Elemen | Size |
|---|---|
| Section title | `\fontsize{13}{16}\bfseries\color{BlueDark}` |
| Cover headline | `\fontsize{20}{24}\bfseries\color{BlueDark}` |
| Cover subtitle | `\fontsize{11}{15}\color{TextLight}` |
| Cover stat value | `\fontsize{22}{26}\bfseries\color{BluePrimary}` |
| Cover stat label | `\fontsize{8}{10}\color{TextLight}` |
| Feature title | `\fontsize{10}{13}\bfseries\color{White}` |
| Feature lead | `\fontsize{9}{12}\color{TextDark}` |
| Pain/solution header | `\fontsize{10}{13}\bfseries` |
| Pain/solution bullet | `\fontsize{9.5}{13}\color{TextDark}` |
| Testimoni quote | `\fontsize{9.5}{13}\itshape\color{TextDark}` |
| Testimoni nama | `\fontsize{8.5}{11}\bfseries\color{BluePrimary}` |
| Testimoni role | `\fontsize{8}{10}\color{TextLight}` |
| Impact stat value | `\fontsize{20}{24}\bfseries\color{BluePrimary}` |
| Impact stat title | `\fontsize{9.5}{12}\bfseries\color{BlueDark}` |
| Impact stat desc | `\fontsize{8.5}{11}\color{TextDark}` |
| Trust bar value | `\fontsize{18}{22}\bfseries\color{White}` |
| Trust bar label | `\fontsize{8}{10}\color{BlueMid}` |
| Step card number | `\fontsize{22}{26}\bfseries\color{BluePrimary}` |
| Step card title | `\fontsize{10}{13}\bfseries\color{BlueDark}` |
| Step card desc | `\fontsize{9}{12}\color{TextDark}` |
| CTA band headline | `\fontsize{13}{16}\bfseries\color{White}` |
| CTA band body | `\fontsize{9.5}{12}\color{BlueMid}` |
| CTA band footer | `\fontsize{9.5}{12}\color{BlueLight}` |
| Pricing line 1 | `\fontsize{9}{12}\bfseries\color{BluePrimary}` |
| Pricing line 2 | `\fontsize{8.5}{11}\color{BlueDark}` |
| Pricing line 3 | `\fontsize{8}{10}\color{TextLight}` |

---

## 7. Checklist Sebelum Commit

- [ ] **Satu** `\end{document}` di akhir file
- [ ] `\fboxsep}{6pt}` di preamble
- [ ] Nama modul di `\kitheader` sudah diganti
- [ ] Nama modul di tag cover (`MODULE: ...`)
- [ ] Tidak ada `\vspace` di dalam minipage/colorbox (kecuali antar elemen konten)
- [ ] `\par` ada setelah setiap `\end{minipage}}` yg diikuti `\vspace`
- [ ] Semua kolom sejajar pakai fixed height `[c]`
- [ ] Trust bar: 4 kolom `1.25cm`, stat card: `2.7cm`, step card: `4.7cm`
- [ ] CTA band diikuti pricing band, baru `\restoregeometry`
- [ ] QR code `../qr_wa.jpeg` ada di step card 2
- [ ] Logo `../logo.png` direferensi di cover
- [ ] Fitur grid 6 item (3 baris × 2 kolom)
- [ ] Testimoni: 2 di halaman 2, 1 + big stat di halaman 4
- [ ] Coming soon section di akhir halaman 3
- [ ] `\restoregeometry` di akhir setiap halaman konten (sebelum `\newpage`)
- [ ] Kompil: `TEXMFHOME=/nonexistent pdflatex -interaction=nonstopmode -halt-on-error`
- [ ] Hasil: 4 halaman, 0 overfull vbox

---

## 8. Contoh Minimal

Lihat file yang sudah jadi sebagai referensi utama:
- **Template standar**: `hris/hris.tex`, `emr/emr.tex`, `customers/customers.tex`
- **Master overview**: `master/master.tex` (struktur beda — 4 hal, ada INVESTASI + integrasi)

Generator: `/tmp/genkits.py` — Python script untuk generate kit baru dari data dictionary.
