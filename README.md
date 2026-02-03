# Pet Shop Website

Website pet shop interaktif dengan animasi scroll yang halus menggunakan Vue.js 2, GSAP, dan Lenis Smooth Scroll.

## 📁 Struktur Project

```
pet-shop/
├── public/                 # Static files
├── src/
│   ├── assets/
│   │   ├── images/        # Gambar-gambar (clinic.jpeg, food.jpeg, grooming.jpeg, logo.png)
│   │   └── styles/        # Global styles
│   │       ├── main.scss  # Main stylesheet entry point
│   │       ├── _variables.scss  # SCSS variables (colors, etc)
│   │       └── _mixins.scss     # SCSS mixins (responsive breakpoints)
│   ├── components/        # Vue components
│   │   ├── Header.vue           # Navigasi header dengan scroll smooth
│   │   ├── SectionOne.vue       # Sticky image stack animation
│   │   ├── SectionTwo.vue       # Parallax step animation
│   │   └── SectionThree.vue     # Thank you section
│   ├── pages/
│   │   └── Index.vue      # Main page yang menggabungkan semua section
│   ├── App.vue            # Root component (inisialisasi Lenis)
│   └── main.js            # Entry point aplikasi
├── package.json           # Dependencies dan scripts
├── vue.config.js          # Vue CLI configuration (publicPath)
└── README.md              # Dokumentasi project
```

## 🚀 Teknologi yang Digunakan

| Teknologi | Versi | Deskripsi |
|-----------|-------|-----------|
| **Vue.js** | 2.6.14 | Framework JavaScript progresif untuk building user interface |
| **GSAP** | 3.14.2 | GreenSock Animation Platform untuk animasi yang powerful |
| **Lenis** | 1.3.17 | Library smooth scroll untuk pengalaman scrolling yang lebih halus |
| **Sass/SCSS** | 1.32.7 | Preprocessor CSS untuk styling yang modular dan maintainable |
| **Vue CLI** | 5.0.0 | Standard tooling untuk Vue.js development |

### GSAP Plugins yang Digunakan:
- **ScrollTrigger**: Memicu animasi berdasarkan posisi scroll
- **ScrollToPlugin**: Navigasi scroll yang mulus ke elemen tertentu

## ✨ Fitur

### 1. Smooth Scrolling
- Integrasi **Lenis** untuk smooth scroll yang performa tinggi
- Sinkronisasi dengan GSAP ScrollTrigger melalui `ticker.add()`
- Custom easing function untuk scroll experience yang natural

### 2. Navigasi Interaktif (Header)
- **Sticky header** yang berubah style saat scroll (background blur, shadow)
- **Navigasi klik** untuk berpindah antar section:
  - Grooming → `#grooming`
  - Food → `#food`
  - Clinic → `#clinic`
- Auto-highlight kata yang aktif berdasarkan posisi scroll
- Responsive untuk Desktop, Tablet, dan Mobile

### 3. Sticky Image Stack (Section One)
- **Desktop**: Gambar sticky di sebelah kanan yang berganti saat scroll
- **Mobile/Tablet**: Gambar inline di bawah setiap content block
- Animasi fade dan scale transition antar gambar
- 3 Content blocks dengan icon animasi (emoji floating)
- ScrollTrigger untuk mengaktifkan gambar berdasarkan posisi content

### 4. Parallax Step Animation (Section Two)
- **Pinned section** dengan virtual scroll (250% height)
- Animasi **zoom-out** effect pada background image
- Text overlay yang fade in/out dengan scale effect
- 3 Steps: Pet Grooming → Healthy Food → Veterinary Clinic
- Scrub animation yang sinkron dengan scroll position

### 5. Responsive Design
Breakpoints yang digunakan:
- **Desktop**: > 1200px
- **Tablet Landscape**: 1025px - 1200px
- **Tablet Portrait**: 769px - 1024px
- **Mobile**: 480px - 768px
- **Mobile Small**: < 480px

## 🛠️ Instalasi

### Prerequisites
- **Node.js** v18.18.0 atau higher
- **npm** 10.2.3 atau higher

### Langkah-langkah Instalasi

1. **Clone repository** (jika dari git):
   ```bash
   git clone <repository-url>
   cd pet-shop
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Install additional packages** (jika belum ada di package.json):
   ```bash
   npm install lenis gsap
   ```

## 🎯 Cara Menjalankan

### Development Mode
Menjalankan development server dengan hot-reload:
```bash
npm run serve
```
Aplikasi akan berjalan di `http://localhost:8080`

## 🎨 Komponen

### [App.vue](src/App.vue)
- Root component yang menginisialisasi **Lenis smooth scroll**
- Mengintegrasikan Lenis dengan GSAP ScrollTrigger
- Global styles untuk reset CSS dan base font

### [Header.vue](src/components/Header.vue)
- Fixed header dengan 3 navigasi items
- Menggunakan GSAP ScrollTrigger untuk deteksi scroll position
- Menggunakan Lenis.scrollTo() untuk smooth navigation
- State: `isMerged`, `activeWord`

### [SectionOne.vue](src/components/SectionOne.vue)
- Sticky image stack dengan 3 content blocks
- Desktop: Layout 2 kolom (text kiri, sticky image kanan)
- Mobile: Single column dengan inline images
- ScrollTrigger untuk change image based on content visibility

### [SectionTwo.vue](src/components/SectionTwo.vue)
- Pinned parallax section dengan step-by-step animation
- Zoom-out effect dari scale 1.3 → 1.0
- Text overlay dengan fade in/out dan scale effect
- Virtual scroll 250% untuk 3 steps

### [SectionThree.vue](src/components/SectionThree.vue)
- Simple thank you section dengan fadeInUp animation
- Background biru solid (#1e88e5)


**Referensi**:
- [Vue.js Documentation](https://vuejs.org/)
- [GSAP Documentation](https://greensock.com/docs/)
- [Lenis Documentation](https://github.com/studio-freight/lenis)
- [Vue CLI Configuration Reference](https://cli.vuejs.org/config/)
