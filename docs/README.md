# 🌿 EcoTrack — Agent Brief & Project Scaffold

> Platform Digital Pengelolaan & Edukasi Sampah  
> Stack: Next.js 14 (App Router) · Tailwind CSS · TypeScript

---

## 🎯 User Scenario — Alur Lengkap

### Pertama Kali Masuk Aplikasi (New User)

```
1. LANDING PAGE  (/)
   └── User membuka browser → melihat halaman utama EcoTrack
       Hero section: headline, subtitle, CTA [Mulai Sekarang] & [Pelajari Lebih]
       Section: Cara Kerja (3 langkah: Lapor → Validasi → Dapat Poin)
       Section: Statistik platform (total user, sampah terkumpul, reward dibagikan)
       Section: Preview fitur unggulan (Gamifikasi, Peta, Edukasi)
       Footer: navigasi, sosial media, kontak

2. REGISTER PAGE  (/auth/register)
   └── User klik [Mulai Sekarang] → form registrasi
       Input: Nama lengkap, Email, Password, Konfirmasi Password
       Checkbox: setuju syarat & ketentuan
       [Daftar] button → sistem kirim email verifikasi
       Link: "Sudah punya akun? Login"

3. EMAIL VERIFICATION
   └── User buka email → klik link verifikasi → redirect ke halaman sukses
       "Akun berhasil diverifikasi! Silakan login."

4. LOGIN PAGE  (/auth/login)
   └── Input: Email, Password
       [Masuk] button → redirect ke Dashboard
       Link: "Lupa password?" → Reset Password flow
       Link: "Belum punya akun? Daftar"

5. DASHBOARD / HOME  (/dashboard)
   └── Greeting: "Selamat datang, [Nama]! 👋"
       Kartu Ringkasan: Total Poin, Laporan Disetujui, Reward Ditukar
       Aktivitas Terbaru: list 3 laporan terakhir + statusnya
       Shortcut CTA: [+ Laporkan Sampah] [Tukar Poin] [Lihat Edukasi]
       Notifikasi banner jika ada laporan baru divalidasi

6. LAPORKAN SAMPAH  (/reports/create)
   └── User klik [+ Laporkan Sampah]
       Form:
         - Upload Foto (drag & drop / klik, max 5MB, JPG/PNG)
         - Jenis Sampah: dropdown (Organik / Anorganik / B3 / Daur Ulang)
         - Estimasi Berat/Jumlah: input angka + satuan
         - Lokasi: input alamat manual atau [Gunakan Lokasi Saya] (GPS)
         - Catatan Tambahan: textarea opsional
       Preview foto sebelum submit
       [Kirim Laporan] → status: "Menunggu Review"

7. RIWAYAT LAPORAN  (/reports)
   └── List semua laporan yang pernah disubmit user
       Setiap card: foto thumbnail, jenis sampah, tanggal, status badge
       Status badge: Menunggu Review (kuning) / Divalidasi (hijau) / Ditolak (merah)
       Klik card → detail laporan + catatan reviewer

8. LAPORAN DIVALIDASI (notifikasi)
   └── User terima notifikasi in-app: "Laporan #123 disetujui! +50 poin"
       Poin otomatis bertambah di saldo
       User klik notifikasi → lihat detail laporan

9. DASHBOARD POIN  (/points)
   └── Total Poin Aktif (besar, prominent)
       Riwayat Transaksi Poin:
         - +50 poin: "Laporan sampah organik disetujui" (tgl)
         - -200 poin: "Penukaran Voucher Belanja Rp 20.000" (tgl)
       Progress bar menuju reward berikutnya

10. KATALOG REWARD  (/rewards)
    └── Grid kartu reward: gambar, nama, poin yang dibutuhkan, stok
        Filter: Semua / Voucher / Merchandise / Donasi
        Badge "Bisa Ditukar" (hijau) jika poin mencukupi
        Badge "Poin Kurang" (abu) jika belum cukup
        Klik reward → modal detail

11. REDEEM REWARD  (/rewards/redeem/:id)
    └── Detail reward: gambar besar, deskripsi, syarat
        Saldo poin saat ini vs poin dibutuhkan
        Form: alamat pengiriman (jika fisik)
        [Konfirmasi Penukaran] → konfirmasi modal
        Sukses → notifikasi "Penukaran berhasil! Cek status di Riwayat Redeem"

12. RIWAYAT REDEEM  (/rewards/history)
    └── List penukaran reward: nama reward, tanggal, status
        Status: Diproses / Dikirim / Selesai
        Detail tracking note dari Admin

13. LAPORKAN TITIK SAMPAH  (/trash-spots/create)
    └── Peta interaktif (Leaflet.js) → user klik/pin lokasi
        Form:
          - Foto kondisi (upload)
          - Deskripsi kondisi
          - Tingkat Keparahan: Ringan / Sedang / Berat
          - Lokasi otomatis dari pin peta
        [Kirim Laporan] → status: "Dilaporkan"

14. PETA TITIK SAMPAH  (/trash-spots)
    └── Peta interaktif dengan marker lokasi penumpukan
        Filter: status (Semua / Dilaporkan / Dalam Penanganan / Selesai)
        Klik marker → popup: foto, deskripsi, status, tanggal laporan

15. EDUKASI  (/education)
    └── Header: "Pusat Edukasi Pengelolaan Sampah"
        Search bar + filter kategori (Organik / Anorganik / B3 / Daur Ulang)
        Grid artikel: thumbnail, judul, kategori badge, estimasi baca
        Klik artikel → halaman detail

16. DETAIL ARTIKEL  (/education/:slug)
    └── Thumbnail artikel, judul, tanggal publikasi, estimasi baca
        Konten artikel lengkap (rich text)
        Navigasi: "Artikel Sebelumnya" / "Artikel Berikutnya"
        Related articles di sidebar/bawah

17. LOKASI PEMBUANGAN  (/disposal-locations)
    └── Peta dengan marker TPS & Bank Sampah terdekat
        Sidebar list lokasi dengan jarak dari user
        Filter: TPS / Bank Sampah / Semua
        Klik marker/card → detail: alamat, jam operasional,
          jenis sampah diterima, nomor kontak

18. PROFIL  (/profile)
    └── Foto profil, nama, email
        Edit profil: nama, foto
        Ganti password
        Statistik personal: total laporan, total poin diperoleh
        Tombol [Keluar]

19. NOTIFIKASI  (/notifications)
    └── List semua notifikasi (read/unread)
        Tipe: laporan divalidasi, poin diterima, status redeem berubah
        Klik → navigate ke halaman terkait
        [Tandai Semua Sudah Dibaca]
```

### Alur Admin (Setelah Login sebagai Admin)

```
A1. ADMIN DASHBOARD  (/admin)
    └── Statistik: Total User, Laporan Masuk Hari Ini,
        Poin Didistribusikan, Reward Ditukar
        Grafik aktivitas mingguan
        Tabel laporan terbaru yang menunggu validasi

A2. VALIDASI LAPORAN  (/admin/reports)
    └── Tabel: nama user, foto (thumbnail), jenis sampah,
        tanggal, lokasi, status
        Filter: Semua / Menunggu / Disetujui / Ditolak
        Klik baris → modal detail: foto besar, semua metadata
        Tombol [Setujui] → input poin → konfirmasi
        Tombol [Tolak] → input alasan penolakan

A3. MANAJEMEN REWARD  (/admin/rewards)
    └── Tabel katalog reward + tombol [+ Tambah Reward]
        Form: nama, deskripsi, gambar, poin dibutuhkan, stok
        Toggle aktif/nonaktif reward
        Tabel penukaran masuk + update status pengiriman

A4. MANAJEMEN KONTEN EDUKASI  (/admin/education)
    └── Tabel artikel: judul, kategori, status (Draft/Published), tanggal
        [+ Tulis Artikel] → editor WYSIWYG (TipTap / Quill)
        Publish / Unpublish / Delete artikel

A5. MANAJEMEN TITIK SAMPAH  (/admin/trash-spots)
    └── Tabel laporan titik sampah + status
        Assign ke petugas lapangan
        Update status penanganan + catatan

A6. MANAJEMEN LOKASI PEMBUANGAN  (/admin/disposal-locations)
    └── Tabel TPS & Bank Sampah
        [+ Tambah Lokasi] → form: nama, tipe, alamat, koordinat,
          jam operasional, jenis sampah diterima, kontak
        Edit / Nonaktifkan lokasi

A7. MANAJEMEN PENGGUNA  (/admin/users)
    └── Tabel semua user: nama, email, role, total poin, tanggal daftar
        Ubah role, reset poin, suspend akun
```

---

## 📁 Struktur Folder & Pembagian Tugas

```
ecotrack/
├── app/                                    # Next.js 14 App Router
│   │
│   ├── (public)/                           # [HAMID] Route grup publik
│   │   ├── page.tsx                        # Landing Page
│   │   ├── layout.tsx
│   │   ├── auth/
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   └── register/
│   │   │       └── page.tsx
│   │   └── education/
│   │       ├── page.tsx                    # List artikel
│   │       └── [slug]/
│   │           └── page.tsx               # Detail artikel
│   │
│   ├── (user)/                             # [ALFIN] Route grup user terautentikasi
│   │   ├── layout.tsx                      # Layout dengan sidebar/navbar user
│   │   ├── dashboard/
│   │   │   └── page.tsx
│   │   ├── reports/
│   │   │   ├── page.tsx                    # Riwayat laporan
│   │   │   └── create/
│   │   │       └── page.tsx               # Form buat laporan
│   │   ├── points/
│   │   │   └── page.tsx                   # Dashboard poin
│   │   ├── rewards/
│   │   │   ├── page.tsx                   # Katalog reward
│   │   │   ├── history/
│   │   │   │   └── page.tsx              # Riwayat redeem
│   │   │   └── redeem/
│   │   │       └── [id]/
│   │   │           └── page.tsx          # Konfirmasi redeem
│   │   ├── profile/
│   │   │   └── page.tsx
│   │   └── notifications/
│   │       └── page.tsx
│   │
│   ├── (map)/                              # [RAJA] Route fitur peta
│   │   ├── layout.tsx
│   │   ├── trash-spots/
│   │   │   ├── page.tsx                   # Peta titik sampah
│   │   │   └── create/
│   │   │       └── page.tsx              # Form lapor titik sampah
│   │   └── disposal-locations/
│   │       └── page.tsx                  # Peta lokasi pembuangan
│   │
│   └── (admin)/                            # [RIFQI] Route admin panel
│       ├── layout.tsx                      # Layout admin sidebar
│       ├── admin/
│       │   ├── page.tsx                   # Admin dashboard
│       │   ├── reports/
│       │   │   └── page.tsx              # Validasi laporan
│       │   ├── rewards/
│       │   │   └── page.tsx              # Manajemen reward
│       │   ├── education/
│       │   │   └── page.tsx              # Manajemen artikel
│       │   ├── trash-spots/
│       │   │   └── page.tsx              # Manajemen titik sampah
│       │   ├── disposal-locations/
│       │   │   └── page.tsx              # Manajemen lokasi
│       │   └── users/
│       │       └── page.tsx              # Manajemen pengguna
│
├── components/
│   │
│   ├── ui/                                 # [HAMID] Design system primitives
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Textarea.tsx
│   │   ├── Badge.tsx
│   │   ├── Card.tsx
│   │   ├── Modal.tsx
│   │   ├── Dropdown.tsx
│   │   ├── Avatar.tsx
│   │   ├── ProgressBar.tsx
│   │   ├── Spinner.tsx
│   │   ├── Toast.tsx
│   │   └── Tabs.tsx
│   │
│   ├── layout/                             # [HAMID] Layout components
│   │   ├── Navbar.tsx
│   │   ├── Footer.tsx
│   │   ├── Sidebar.tsx
│   │   ├── UserLayout.tsx
│   │   └── AdminLayout.tsx
│   │
│   ├── landing/                            # [HAMID] Landing page sections
│   │   ├── HeroSection.tsx
│   │   ├── HowItWorksSection.tsx
│   │   ├── StatsSection.tsx
│   │   ├── FeaturesSection.tsx
│   │   └── CtaSection.tsx
│   │
│   ├── auth/                               # [HAMID] Auth components
│   │   ├── LoginForm.tsx
│   │   ├── RegisterForm.tsx
│   │   └── ResetPasswordForm.tsx
│   │
│   ├── dashboard/                          # [ALFIN] Dashboard components
│   │   ├── SummaryCard.tsx
│   │   ├── RecentActivityList.tsx
│   │   ├── QuickActionButtons.tsx
│   │   └── NotificationBanner.tsx
│   │
│   ├── reports/                            # [ALFIN] Report components
│   │   ├── ReportForm.tsx
│   │   ├── PhotoUploader.tsx
│   │   ├── WasteTypeSelector.tsx
│   │   ├── LocationPicker.tsx
│   │   ├── ReportCard.tsx
│   │   ├── ReportStatusBadge.tsx
│   │   └── ReportDetailModal.tsx
│   │
│   ├── points/                             # [ALFIN] Points & rewards components
│   │   ├── PointsBalanceCard.tsx
│   │   ├── PointsTransactionList.tsx
│   │   ├── PointsProgressBar.tsx
│   │   ├── RewardCard.tsx
│   │   ├── RewardCatalogGrid.tsx
│   │   ├── RedeemConfirmModal.tsx
│   │   └── RedemptionHistoryList.tsx
│   │
│   ├── map/                                # [RAJA] Map components
│   │   ├── InteractiveMap.tsx
│   │   ├── MapMarker.tsx
│   │   ├── TrashSpotPopup.tsx
│   │   ├── DisposalLocationPopup.tsx
│   │   ├── TrashSpotForm.tsx
│   │   ├── TrashSpotCard.tsx
│   │   ├── LocationSidebar.tsx
│   │   └── MapFilterBar.tsx
│   │
│   ├── education/                          # [RAJA] Education components
│   │   ├── ArticleCard.tsx
│   │   ├── ArticleGrid.tsx
│   │   ├── ArticleSearchBar.tsx
│   │   ├── CategoryFilterTabs.tsx
│   │   ├── ArticleDetail.tsx
│   │   └── RelatedArticles.tsx
│   │
│   ├── notifications/                      # [ALFIN] Notification components
│   │   ├── NotificationItem.tsx
│   │   ├── NotificationList.tsx
│   │   └── NotificationBell.tsx
│   │
│   └── admin/                              # [RIFQI] Admin panel components
│       ├── AdminStatsCard.tsx
│       ├── AdminActivityChart.tsx
│       ├── ReportValidationTable.tsx
│       ├── ReportDetailPanel.tsx
│       ├── ValidationActionButtons.tsx
│       ├── RewardManagementTable.tsx
│       ├── RewardFormModal.tsx
│       ├── RedemptionManagementTable.tsx
│       ├── ArticleManagementTable.tsx
│       ├── ArticleEditor.tsx
│       ├── TrashSpotManagementTable.tsx
│       ├── DisposalLocationTable.tsx
│       ├── DisposalLocationFormModal.tsx
│       └── UserManagementTable.tsx
│
├── lib/                                    # [HAMID] Utilities & config
│   ├── api.ts                             # Axios / fetch wrapper
│   ├── auth.ts                            # Auth helpers (JWT decode, etc.)
│   ├── validators.ts                      # Zod schemas
│   └── utils.ts                           # Helper functions
│
├── hooks/                                  # [HAMID] Custom React hooks
│   ├── useAuth.ts
│   ├── useGeolocation.ts
│   └── useNotifications.ts
│
├── types/                                  # [HAMID] TypeScript interfaces
│   └── index.ts
│
├── styles/
│   └── globals.css                        # [HAMID] Global CSS + Tailwind directives
│
├── public/
│   └── assets/
│
├── tailwind.config.ts                      # [HAMID] Design system tokens
└── next.config.ts
```

### 👥 Ringkasan Pembagian Tugas

| Member | Scope |
|--------|-------|
| **Hamid** | `app/(public)/` · `components/ui/` · `components/layout/` · `components/landing/` · `components/auth/` · `lib/` · `hooks/` · `types/` · `styles/globals.css` · `tailwind.config.ts` |
| **Alfin** | `app/(user)/` · `components/dashboard/` · `components/reports/` · `components/points/` · `components/notifications/` |
| **Raja** | `app/(map)/` · `components/map/` · `components/education/` |
| **Rifqi** | `app/(admin)/` · `components/admin/` seluruhnya |

---

## 🤖 Prompt untuk AI Agent (Next.js Scaffold Generator)

```
You are an expert Next.js 14 developer using the App Router and TypeScript.
Your task is to scaffold all component and page stub files for a web platform
called **EcoTrack** — a waste management and education platform with gamification.

## Design System

Implement the following design tokens in tailwind.config.ts AND globals.css:

### Colors
- Primary:   #1B2A5E  (dark navy)
- Secondary: #D32F2F  (red)
- Tertiary:  #2E7D32  (green)
- Neutral:   #475569
- Background: #EEF0F8 (light blue-grey)
- Surface:   #FFFFFF
- Border:    #E2E8F0

### Typography
Font families (declare in globals.css @import and tailwind config):
- UI / Body:  Inter, 'Noto Sans', system-ui, -apple-system, sans-serif
- Article:    'Merriweather', 'Georgia', serif
- Mono:       'JetBrains Mono', 'Fira Code', 'Courier New', monospace

### Spacing & Radius
- Card border-radius: 12px  (rounded-xl)
- Input border-radius: 8px  (rounded-lg)
- Button border-radius: 24px (rounded-full)
- Card shadow: 0 2px 8px rgba(27,42,94,0.08)

### Tailwind Config Extension
Extend the default Tailwind theme with:
  colors: { primary, secondary, tertiary, neutral, background }
  fontFamily: { sans, serif, mono }
  borderRadius: { card: '12px', input: '8px', btn: '24px' }
  boxShadow: { card: '0 2px 8px rgba(27,42,94,0.08)' }

---

## Your Task

Create **stub files** for every component and page listed below. Each stub must:
1. Have the correct named export matching the filename (PascalCase)
2. Use TypeScript with properly typed props interface
3. Return a placeholder `<div>` with:
   - `data-component` attribute set to the component name
   - A visible `<p>` or `<span>` showing the component name (for dev identification)
   - Tailwind classes for basic layout (bg-white, p-4, rounded-xl where appropriate)
4. Include a JSDoc comment block describing what the component renders
5. Include `// ASSIGNED TO: [Name]` at the top of each file
6. Include a `// TODO: Implement UI` comment in the return statement
7. For pages, wrap in a `<main>` tag and show the route as a comment

Do NOT implement real logic, real API calls, or real UI yet.
Only declare the prop interfaces — don't implement them.

---

## Files to Generate

---

### tailwind.config.ts
Extend theme with all design tokens above.
Add Inter and Merriweather to fontFamily.

### styles/globals.css
Import Inter and Merriweather from Google Fonts.
Configure Tailwind @tailwind directives.
Add CSS custom properties for design tokens:
  --color-primary, --color-secondary, --color-tertiary,
  --color-neutral, --color-background

---

### types/index.ts
// ASSIGNED TO: Hamid
Export these TypeScript interfaces:
  User { id, name, email, role, photoUrl, totalPoints, createdAt }
  WasteReport { id, userId, wasteType, estimatedWeight, photoUrl,
    locationAddress, latitude, longitude, status, pointsAwarded,
    reviewNote, createdAt }
  PointTransaction { id, userId, reportId, transactionType, points,
    description, createdAt }
  Reward { id, name, description, imageUrl, pointsRequired, stock, isActive }
  RewardRedemption { id, userId, rewardId, pointsSpent, status,
    deliveryAddress, trackingNote, createdAt }
  TrashSpotReport { id, userId, photoUrl, description, severityLevel,
    latitude, longitude, locationAddress, status, handlerNote, createdAt }
  EducationArticle { id, authorId, title, slug, content, category,
    thumbnailUrl, isPublished, publishedAt, createdAt }
  DisposalLocation { id, name, type, address, latitude, longitude,
    operationalHours, acceptedWasteTypes, contact, isActive }
  Notification { id, userId, type, message, isRead, createdAt }

---

### components/ui/Button.tsx
// ASSIGNED TO: Hamid
Props: label(string), onClick(()=>void), variant('primary'|'secondary'|
  'outlined'|'ghost'), size('sm'|'md'|'lg'), disabled(boolean?),
  loading(boolean?), fullWidth(boolean?)
Variants map to Tailwind classes using design tokens.

### components/ui/Input.tsx
// ASSIGNED TO: Hamid
Props: name, label(string?), placeholder, type, value, onChange,
  error(string?), disabled(boolean?)

### components/ui/Textarea.tsx
// ASSIGNED TO: Hamid
Props: name, label(string?), placeholder, value, onChange,
  rows(number?), error(string?)

### components/ui/Badge.tsx
// ASSIGNED TO: Hamid
Props: label(string), variant('success'|'warning'|'danger'|'info'|'neutral')
Map to green/yellow/red/blue/grey background respectively.

### components/ui/Card.tsx
// ASSIGNED TO: Hamid
Props: children(ReactNode), className(string?), onClick(()=>void?)
Shadow: shadow-card, radius: rounded-card

### components/ui/Modal.tsx
// ASSIGNED TO: Hamid
Props: isOpen(boolean), onClose(()=>void), title(string?), children(ReactNode)

### components/ui/Dropdown.tsx
// ASSIGNED TO: Hamid
Props: options(Array<{label,value}>), value(string), onChange, placeholder

### components/ui/Avatar.tsx
// ASSIGNED TO: Hamid
Props: src(string?), name(string), size('sm'|'md'|'lg')
Show initials if no src.

### components/ui/ProgressBar.tsx
// ASSIGNED TO: Hamid
Props: value(number 0-100), color('primary'|'secondary'|'tertiary'), label(string?)

### components/ui/Spinner.tsx
// ASSIGNED TO: Hamid
Props: size('sm'|'md'|'lg'), color(string?)

### components/ui/Toast.tsx
// ASSIGNED TO: Hamid
Props: message(string), type('success'|'error'|'info'), onClose(()=>void)

### components/ui/Tabs.tsx
// ASSIGNED TO: Hamid
Props: tabs(Array<{label, value}>), activeTab(string), onChange

---

### components/layout/Navbar.tsx
// ASSIGNED TO: Hamid
Props: isAuthenticated(boolean), user(User?)
Show: logo, nav links, notification bell (if auth), avatar menu (if auth),
  login/register buttons (if not auth)

### components/layout/Footer.tsx
// ASSIGNED TO: Hamid
No props. Static links: About, Kontak, Kebijakan Privasi + social icons

### components/layout/Sidebar.tsx
// ASSIGNED TO: Hamid
Props: role('user'|'admin'), currentPath(string)
User nav: Dashboard, Laporan, Poin & Reward, Titik Sampah, Edukasi,
  Lokasi Pembuangan, Profil
Admin nav: Dashboard, Validasi Laporan, Reward, Edukasi, Titik Sampah,
  Lokasi, Pengguna

### components/layout/UserLayout.tsx
// ASSIGNED TO: Hamid
Props: children(ReactNode)
Wraps with Navbar + Sidebar (user variant) + content area

### components/layout/AdminLayout.tsx
// ASSIGNED TO: Hamid
Props: children(ReactNode)
Wraps with AdminSidebar + content area with admin branding

---

### components/landing/HeroSection.tsx
// ASSIGNED TO: Hamid
No props. Big headline, subtitle, two CTA buttons: [Mulai Sekarang] [Pelajari Lebih]
Background: gradient primary to background color

### components/landing/HowItWorksSection.tsx
// ASSIGNED TO: Hamid
No props. 3-step cards: Lapor → Validasi → Dapat Poin
Each card: icon, step number, title, description

### components/landing/StatsSection.tsx
// ASSIGNED TO: Hamid
No props. 4 stat counters: Total Pengguna, Sampah Terkumpul (kg),
  Poin Dibagikan, Reward Ditukar

### components/landing/FeaturesSection.tsx
// ASSIGNED TO: Hamid
No props. Feature highlight cards: Gamifikasi, Peta Interaktif,
  Konten Edukasi, Pelaporan Mudah

### components/landing/CtaSection.tsx
// ASSIGNED TO: Hamid
No props. Bottom CTA: headline + [Bergabung Sekarang] button + background accent

---

### components/auth/LoginForm.tsx
// ASSIGNED TO: Hamid
Props: onSubmit(({email,password})=>void), isLoading(boolean)
Fields: Email, Password (show/hide toggle), Remember Me checkbox
Link: Lupa Password, Belum punya akun?

### components/auth/RegisterForm.tsx
// ASSIGNED TO: Hamid
Props: onSubmit(({name,email,password,confirmPassword})=>void), isLoading(boolean)
Fields: Nama Lengkap, Email, Password, Konfirmasi Password, ToS checkbox

### components/auth/ResetPasswordForm.tsx
// ASSIGNED TO: Hamid
Props: onSubmit(({email})=>void), isLoading(boolean)
Field: Email only

---

### components/dashboard/SummaryCard.tsx
// ASSIGNED TO: Alfin
Props: title(string), value(string|number), icon(ReactNode),
  color('primary'|'secondary'|'tertiary'), trend(string?)

### components/dashboard/RecentActivityList.tsx
// ASSIGNED TO: Alfin
Props: activities(Array<WasteReport>)
Each item: foto thumbnail, jenis sampah, tanggal, status badge

### components/dashboard/QuickActionButtons.tsx
// ASSIGNED TO: Alfin
No props. 3 shortcut buttons: + Laporkan Sampah, Tukar Poin, Lihat Edukasi

### components/dashboard/NotificationBanner.tsx
// ASSIGNED TO: Alfin
Props: message(string), type('success'|'info'), onDismiss(()=>void)

---

### components/reports/ReportForm.tsx
// ASSIGNED TO: Alfin
Props: onSubmit(FormData=>void), isLoading(boolean)
Sections: PhotoUploader, WasteTypeSelector, weight input,
  LocationPicker, notes textarea, submit button

### components/reports/PhotoUploader.tsx
// ASSIGNED TO: Alfin
Props: onUpload((file:File)=>void), preview(string?), maxSizeMB(number)
Drag & drop zone + click to upload. Shows preview after upload.
Validates: JPG/PNG only, max 5MB

### components/reports/WasteTypeSelector.tsx
// ASSIGNED TO: Alfin
Props: value(string), onChange((val:string)=>void)
Options: Organik, Anorganik, B3, Daur Ulang (as styled radio cards)

### components/reports/LocationPicker.tsx
// ASSIGNED TO: Alfin
Props: value(string), onChange((val:string)=>void),
  onGetGPS(()=>void), isGPSLoading(boolean)
Text input for address + [Gunakan Lokasi Saya] button

### components/reports/ReportCard.tsx
// ASSIGNED TO: Alfin
Props: report(WasteReport), onClick(()=>void)
Shows: thumbnail, waste type, date, status badge

### components/reports/ReportStatusBadge.tsx
// ASSIGNED TO: Alfin
Props: status('PENDING'|'APPROVED'|'REJECTED')
Maps to Badge component with appropriate variant and Indonesian label

### components/reports/ReportDetailModal.tsx
// ASSIGNED TO: Alfin
Props: report(WasteReport?), isOpen(boolean), onClose(()=>void)
Full photo, all metadata, review note if rejected

---

### components/points/PointsBalanceCard.tsx
// ASSIGNED TO: Alfin
Props: totalPoints(number)
Large prominent display of current points balance

### components/points/PointsTransactionList.tsx
// ASSIGNED TO: Alfin
Props: transactions(Array<PointTransaction>)
Each row: icon (+/-), description, points (colored), date

### components/points/PointsProgressBar.tsx
// ASSIGNED TO: Alfin
Props: currentPoints(number), nextRewardPoints(number), nextRewardName(string)
Progress bar showing distance to next redeemable reward

### components/points/RewardCard.tsx
// ASSIGNED TO: Alfin
Props: reward(Reward), userPoints(number), onClick(()=>void)
Card with image, name, points required, stock badge
"Bisa Ditukar" (green) if userPoints >= pointsRequired

### components/points/RewardCatalogGrid.tsx
// ASSIGNED TO: Alfin
Props: rewards(Array<Reward>), userPoints(number),
  activeFilter(string), onFilterChange((f:string)=>void)
Grid of RewardCard + filter tabs: Semua / Voucher / Merchandise / Donasi

### components/points/RedeemConfirmModal.tsx
// ASSIGNED TO: Alfin
Props: reward(Reward?), isOpen(boolean), onClose(()=>void),
  onConfirm((deliveryAddress:string)=>void), isLoading(boolean)
Shows reward summary, points to be deducted, delivery address input

### components/points/RedemptionHistoryList.tsx
// ASSIGNED TO: Alfin
Props: redemptions(Array<RewardRedemption>)
Each row: reward name, date, points spent, status badge, tracking note

---

### components/notifications/NotificationItem.tsx
// ASSIGNED TO: Alfin
Props: notification(Notification), onClick(()=>void)
Shows: icon (based on type), message, time ago, unread dot indicator

### components/notifications/NotificationList.tsx
// ASSIGNED TO: Alfin
Props: notifications(Array<Notification>), onMarkAllRead(()=>void)
List of NotificationItem + "Tandai Semua Dibaca" button

### components/notifications/NotificationBell.tsx
// ASSIGNED TO: Alfin
Props: count(number), onClick(()=>void)
Bell icon with badge count overlay (for navbar)

---

### components/map/InteractiveMap.tsx
// ASSIGNED TO: Raja
Props: center([lat,lng]), zoom(number), markers(Array<MapMarker>),
  onMapClick(([lat,lng])=>void?)
Leaflet.js map wrapper. Dynamic import (no SSR).

### components/map/MapMarker.tsx
// ASSIGNED TO: Raja
Props: position([lat,lng]), type('trash-spot'|'disposal'|'selected'),
  popupContent(ReactNode)
Custom icon based on type.

### components/map/TrashSpotPopup.tsx
// ASSIGNED TO: Raja
Props: spot(TrashSpotReport)
Popup: thumbnail foto, deskripsi, severity badge, status badge, tanggal

### components/map/DisposalLocationPopup.tsx
// ASSIGNED TO: Raja
Props: location(DisposalLocation)
Popup: nama, tipe badge, alamat, jam operasional, jenis sampah, kontak

### components/map/TrashSpotForm.tsx
// ASSIGNED TO: Raja
Props: selectedCoords([lat,lng]?), onSubmit((data)=>void), isLoading(boolean)
Fields: PhotoUploader, deskripsi textarea, severity selector,
  koordinat (dari klik peta), submit button

### components/map/TrashSpotCard.tsx
// ASSIGNED TO: Raja
Props: spot(TrashSpotReport), onClick(()=>void)
List card for sidebar: lokasi, severity badge, status, tanggal

### components/map/LocationSidebar.tsx
// ASSIGNED TO: Raja
Props: locations(Array<DisposalLocation>), onSelect((loc)=>void)
Scrollable list of disposal locations sorted by distance
Each item: nama, tipe, jarak, jam buka

### components/map/MapFilterBar.tsx
// ASSIGNED TO: Raja
Props: options(Array<{label,value}>), active(string), onChange

---

### components/education/ArticleCard.tsx
// ASSIGNED TO: Raja
Props: article(EducationArticle), onClick(()=>void)
Card: thumbnail, category badge, judul, estimasi baca (reading time)

### components/education/ArticleGrid.tsx
// ASSIGNED TO: Raja
Props: articles(Array<EducationArticle>)
Responsive grid of ArticleCard components

### components/education/ArticleSearchBar.tsx
// ASSIGNED TO: Raja
Props: value(string), onChange((v:string)=>void), placeholder(string?)

### components/education/CategoryFilterTabs.tsx
// ASSIGNED TO: Raja
Props: categories(Array<string>), active(string), onChange
Tabs: Semua / Organik / Anorganik / B3 / Daur Ulang

### components/education/ArticleDetail.tsx
// ASSIGNED TO: Raja
Props: article(EducationArticle)
Full content renderer: thumbnail hero, title, meta (date, read time),
  rich text content (dangerouslySetInnerHTML or MDX),
  prev/next navigation links

### components/education/RelatedArticles.tsx
// ASSIGNED TO: Raja
Props: articles(Array<EducationArticle>), currentSlug(string)
Horizontal scroll or grid of 3 related ArticleCard

---

### components/admin/AdminStatsCard.tsx
// ASSIGNED TO: Rifqi
Props: title(string), value(number|string), icon(ReactNode),
  color('primary'|'secondary'|'tertiary'), change(string?)

### components/admin/AdminActivityChart.tsx
// ASSIGNED TO: Rifqi
Props: data(Array<{date:string, reports:number, points:number}>)
Line or bar chart placeholder (use recharts or chart.js stub)

### components/admin/ReportValidationTable.tsx
// ASSIGNED TO: Rifqi
Props: reports(Array<WasteReport>), onApprove((id,points)=>void),
  onReject((id,reason)=>void), activeFilter(string), onFilterChange
Columns: User, Foto, Jenis, Lokasi, Tanggal, Status, Aksi

### components/admin/ReportDetailPanel.tsx
// ASSIGNED TO: Rifqi
Props: report(WasteReport?), isOpen(boolean), onClose(()=>void)
Slide-in or modal: foto besar, semua metadata, approve/reject actions

### components/admin/ValidationActionButtons.tsx
// ASSIGNED TO: Rifqi
Props: reportId(string), onApprove(()=>void), onReject(()=>void)
[Setujui] primary button + [Tolak] danger button

### components/admin/RewardManagementTable.tsx
// ASSIGNED TO: Rifqi
Props: rewards(Array<Reward>), onEdit((r)=>void), onToggle((id)=>void)
Columns: Nama, Poin, Stok, Status toggle, Aksi

### components/admin/RewardFormModal.tsx
// ASSIGNED TO: Rifqi
Props: reward(Reward?), isOpen(boolean), onClose, onSave
Fields: nama, deskripsi, gambar (upload), poin dibutuhkan, stok, aktif toggle

### components/admin/RedemptionManagementTable.tsx
// ASSIGNED TO: Rifqi
Props: redemptions(Array<RewardRedemption>), onUpdateStatus
Columns: User, Reward, Poin Digunakan, Status, Aksi update status

### components/admin/ArticleManagementTable.tsx
// ASSIGNED TO: Rifqi
Props: articles(Array<EducationArticle>), onEdit, onDelete, onTogglePublish
Columns: Judul, Kategori, Status, Tanggal, Aksi

### components/admin/ArticleEditor.tsx
// ASSIGNED TO: Rifqi
Props: article(EducationArticle?), onSave((data)=>void), isLoading(boolean)
WYSIWYG editor placeholder (TipTap or Quill stub)
Fields: judul, slug (auto-generate), kategori, thumbnail upload, konten editor

### components/admin/TrashSpotManagementTable.tsx
// ASSIGNED TO: Rifqi
Props: spots(Array<TrashSpotReport>), onUpdateStatus, onAssign
Columns: Lokasi, Severity, Status, Pelapor, Tanggal, Aksi

### components/admin/DisposalLocationTable.tsx
// ASSIGNED TO: Rifqi
Props: locations(Array<DisposalLocation>), onEdit, onToggle

### components/admin/DisposalLocationFormModal.tsx
// ASSIGNED TO: Rifqi
Props: location(DisposalLocation?), isOpen, onClose, onSave
Fields: nama, tipe (TPS/Bank Sampah), alamat, koordinat (lat/lng),
  jam operasional, jenis sampah diterima, kontak, aktif toggle

### components/admin/UserManagementTable.tsx
// ASSIGNED TO: Rifqi
Props: users(Array<User>), onChangeRole, onSuspend
Columns: Avatar+Nama, Email, Role badge, Total Poin, Tanggal Daftar, Aksi

---

## Page Stubs

Generate page stubs for ALL routes below.
Each page stub must:
- Import the relevant component(s) from components/
- Return a <main> with the component(s) laid out
- Include a comment: // Route: /path/to/page

### app/(public)/page.tsx
// ASSIGNED TO: Hamid
Compose: HeroSection, HowItWorksSection, StatsSection, FeaturesSection, CtaSection

### app/(public)/auth/login/page.tsx
// ASSIGNED TO: Hamid
Compose: LoginForm centered in a two-column layout (form left, illustration right)

### app/(public)/auth/register/page.tsx
// ASSIGNED TO: Hamid
Compose: RegisterForm centered layout

### app/(public)/education/page.tsx
// ASSIGNED TO: Raja
Compose: ArticleSearchBar, CategoryFilterTabs, ArticleGrid

### app/(public)/education/[slug]/page.tsx
// ASSIGNED TO: Raja
Compose: ArticleDetail, RelatedArticles

### app/(user)/dashboard/page.tsx
// ASSIGNED TO: Alfin
Compose: NotificationBanner?, SummaryCard x3, QuickActionButtons, RecentActivityList

### app/(user)/reports/page.tsx
// ASSIGNED TO: Alfin
Compose: page header + list of ReportCard components

### app/(user)/reports/create/page.tsx
// ASSIGNED TO: Alfin
Compose: ReportForm full page

### app/(user)/points/page.tsx
// ASSIGNED TO: Alfin
Compose: PointsBalanceCard, PointsProgressBar, PointsTransactionList

### app/(user)/rewards/page.tsx
// ASSIGNED TO: Alfin
Compose: RewardCatalogGrid

### app/(user)/rewards/history/page.tsx
// ASSIGNED TO: Alfin
Compose: RedemptionHistoryList

### app/(user)/rewards/redeem/[id]/page.tsx
// ASSIGNED TO: Alfin
Compose: RedeemConfirmModal (open by default)

### app/(user)/profile/page.tsx
// ASSIGNED TO: Alfin
Compose: Avatar, profile form fields, stats summary

### app/(user)/notifications/page.tsx
// ASSIGNED TO: Alfin
Compose: NotificationList

### app/(map)/trash-spots/page.tsx
// ASSIGNED TO: Raja
Compose: InteractiveMap (full height), MapFilterBar

### app/(map)/trash-spots/create/page.tsx
// ASSIGNED TO: Raja
Compose: InteractiveMap (half height) + TrashSpotForm

### app/(map)/disposal-locations/page.tsx
// ASSIGNED TO: Raja
Compose: InteractiveMap + LocationSidebar

### app/(admin)/admin/page.tsx
// ASSIGNED TO: Rifqi
Compose: AdminStatsCard x4, AdminActivityChart, ReportValidationTable (preview 5 rows)

### app/(admin)/admin/reports/page.tsx
// ASSIGNED TO: Rifqi
Compose: ReportValidationTable full + ReportDetailPanel

### app/(admin)/admin/rewards/page.tsx
// ASSIGNED TO: Rifqi
Compose: RewardManagementTable + RedemptionManagementTable + RewardFormModal

### app/(admin)/admin/education/page.tsx
// ASSIGNED TO: Rifqi
Compose: ArticleManagementTable + ArticleEditor

### app/(admin)/admin/trash-spots/page.tsx
// ASSIGNED TO: Rifqi
Compose: TrashSpotManagementTable

### app/(admin)/admin/disposal-locations/page.tsx
// ASSIGNED TO: Rifqi
Compose: DisposalLocationTable + DisposalLocationFormModal

### app/(admin)/admin/users/page.tsx
// ASSIGNED TO: Rifqi
Compose: UserManagementTable

---

## package.json dependencies to include:
- next: 14
- react, react-dom
- typescript
- tailwindcss, postcss, autoprefixer
- leaflet, react-leaflet (map — dynamic import only, no SSR)
- @types/leaflet
- recharts (charts for admin)
- react-hook-form (form handling)
- zod (validation)
- axios (HTTP client)
- @tiptap/react, @tiptap/starter-kit (WYSIWYG editor stub)
- lucide-react (icons)
- clsx, tailwind-merge (class utilities)
- date-fns (date formatting)

## Critical Rules:
- Use App Router (NOT pages/ directory)
- Mark all Leaflet map components with "use client" AND dynamic import with ssr:false
- Mark all interactive client components with "use client"
- Server components stay as default (no directive)
- All colors MUST use Tailwind config tokens, NOT hardcoded hex
- All components must be importable as named exports
- Props interfaces must be in the same file as the component (not a separate types file)
- Use cn() utility (clsx + tailwind-merge) for conditional class merging
- Every file must have: // ASSIGNED TO: [Name] and // TODO: Implement UI

Output each file as a separate code block with its full relative path as the title.
Generate ALL files — do not skip any.
```

---

## 📄 Catatan Tambahan untuk Tim

### Git Branch Convention
```
feature/<nama>/<deskripsi>

Contoh:
  feature/hamid/core-ui-components
  feature/hamid/landing-page
  feature/alfin/dashboard-reports
  feature/alfin/points-rewards
  feature/raja/map-feature
  feature/raja/education-pages
  feature/rifqi/admin-panel
```

### Commit Convention
```
feat(scope): deskripsi
fix(scope): deskripsi
style(scope): deskripsi
chore(scope): deskripsi
```

### Hal yang Perlu Didiskusikan Tim
- API base URL & environment variables (.env.local)
- Auth state management: Context API vs Zustand vs NextAuth.js
- Map provider: Leaflet.js (free) atau Google Maps API (butuh API key)
- WYSIWYG editor: TipTap (recommended) atau Quill
- Image upload strategy: langsung ke Cloudinary atau melalui backend API
