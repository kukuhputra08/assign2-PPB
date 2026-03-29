# Assignment 2 - My First App
Aplikasi Flutter sederhana yang menampilkan penggunaan **Row**, **Column**, **StatelessWidget**, **StatefulWidget**, serta berbagai widget dasar lainnya.

## Screenshot Struktur Aplikasi
Aplikasi terdiri dari 4 bagian utama yang tersusun secara vertikal dalam sebuah `Column`:

```
┌──────────────────────────────────┐
│           AppBar                 │  ← "My First App" (orange)
├──────────────────────────────────┤
│                                  │
│     ┌──────────────────┐         │
│     │                  │         │
│     │   Image.asseet   │         │  ← Gambar random (lightBlue)
│     │  (picsum.photos) │         │
│     │                  │         │
│     └──────────────────┘         │
│                                  │
│  ┌─────────────────────────┐     │
│  │ What image is that      │     │  ← Teks pertanyaan (pink)
│  └─────────────────────────┘     │
│                                  │
│  ┌─────────────────────────┐     │
│  │  Food  Scenery  People  │     │  ← Kategori icon (yellow)
│  └─────────────────────────┘     │
│                                  │
│  ┌─────────────────────────┐     │
│  │ Counter here: 0     [+] │     │  ← Counter interaktif (cyan)
│  └─────────────────────────┘     │
│                                  │
└──────────────────────────────────┘
```

<img width="676" height="1376" alt="image" src="https://github.com/user-attachments/assets/15485489-1e76-44c0-8da5-8edca84c8118" />

## Widget Tree

Berikut adalah struktur widget tree dari aplikasi:

```
Column
├── Container
│   └── Image
├── Container
│   └── Text
├── Container
│   └── Row
│       ├── Column
│       │   ├── Icon
│       │   └── Text
│       ├── Column
│       │   ├── Icon
│       │   └── Text
│       └── Column
│           ├── Icon
│           └── Text
└── Container
    └── Row
        ├── Text
        └── Container
            └── Icon
```

**Penjelasan Struktur:**
- **Column** (root): Menyusun 3 `Container` + 1 `CounterCard` secara vertikal
- **Container** pertama: Menampilkan gambar dari internet (`Image.network`)
- **Container** kedua: Menampilkan teks pertanyaan
- **Container** ketiga: Berisi `Row` dengan 3 `Column` (masing-masing `Icon` + `Text` untuk kategori Food, Scenery, People)
- **CounterCard**: Pada widget tree terlihat sebagai `Container -> Row -> Text + Container -> Icon`, karena root dari `CounterCard` adalah `Container`

## Penjelasan Widget

### 1. MyApp (StatelessWidget)
Widget root aplikasi. Membungkus seluruh aplikasi dalam `MaterialApp` dengan konfigurasi:
- **Theme**: Material 3 dengan seed color `deepPurple`
- **Home**: Mengarah ke `const RowColumnPage()`
- **Title**: Menggunakan nilai `'Flutter Demo'`

### 2. RowColumnPage (StatelessWidget)
Halaman utama aplikasi yang menggunakan `Scaffold` sebagai struktur dasar. Terdiri dari:

Di dalam method `build`, widget ini juga membuat variabel:
- `mediaQueryData` dari `MediaQuery.of(context)`
- `screenWidth` dari `mediaQueryData.size.width`
- `screenHeight` dari `mediaQueryData.size.height`

Catatan: `screenWidth` dan `screenHeight` saat ini belum dipakai langsung pada layout.

#### a. AppBar
- Judul **"My First App"** dengan teks berwarna hitam
- Background warna `orange[200]`
- Judul diposisikan di tengah (`centerTitle: true`)

#### b. Body - Column (Konten Utama)
Seluruh konten body disusun secara vertikal menggunakan `Column` dengan alignment center. Di kode, children dari `Column` adalah 3 `Container` + `CounterCard`:

| Section | Struktur Sesuai Tree | Fungsi |
|--------|----------------------|--------|
| 1. Image Container | `Container -> Image` | Menampilkan gambar random dari `picsum.photos/200` |
| 2. Question Container | `Container -> Text` | Menampilkan teks **"What image is that"** |
| 3. Category Container | `Container -> Row -> 3 x Column (Icon + Text)` | Menampilkan kategori **Food**, **Scenery**, **People** |
| 4. CounterCard | `Container -> Row -> Text + Container -> Icon` | Menampilkan counter dan tombol tambah |

Icon kategori menggunakan icon bawaan Material:
- `Icons.food_bank` untuk makanan
- `Icons.landscape` untuk pemandangan
- `Icons.people` untuk orang

### 3. CounterCard (StatefulWidget)
Widget interaktif yang mendemonstrasikan **state management** sederhana di Flutter.

| Widget | Fungsi |
|--------|--------|
| `Container` (cyan) | Background cyan dengan margin dan padding |
| `Row` (spaceBetween) | Menyusun teks counter dan tombol di ujung kiri-kanan |
| `Text` | Menampilkan **"Counter here: $_counter"** yang berubah secara dinamis |
| `IconButton` (ditampilkan sebagai `Icon` pada tree) | Tombol `+` yang memanggil `_incrementCounter()` |

Nama state dan method yang digunakan di kelas `_CounterCardState`:
- Variabel state: `_counter`
- Method aksi tombol: `_incrementCounter()`

**Cara Kerja State:**
- Variabel `_counter` (int) menyimpan nilai counter, dimulai dari `0`
- Saat tombol `+` ditekan, method `_incrementCounter()` dipanggil
- Di dalam method tersebut, `setState()` dipanggil untuk mengupdate `_counter++`
- `setState()` memberi tahu Flutter untuk me-rebuild widget ini sehingga UI menampilkan nilai terbaru

```dart
void _incrementCounter() {
  setState(() {
    _counter++; // Update state, trigger rebuild
  });
}
```

## Konsep Flutter yang Digunakan

| Konsep | Penjelasan |
|--------|-----------|
| **StatelessWidget** | Widget yang tidak memiliki state internal (MyApp, RowColumnPage) |
| **StatefulWidget** | Widget yang memiliki state yang bisa berubah (CounterCard) |
| **Column** | Layout widget untuk menyusun children secara vertikal |
| **Row** | Layout widget untuk menyusun children secara horizontal |
| **Container** | Widget serbaguna untuk styling (warna, margin, padding) |
| **MediaQuery** | Mengambil informasi ukuran layar (`mediaQueryData`, `screenWidth`, `screenHeight`) |
| **Image** | Menampilkan gambar dari internet (`Image.network`) |
| **Text** | Menampilkan label/teks pada setiap section |
| **Icon** | Menampilkan ikon kategori dan tombol tambah |
| **setState()** | Method untuk mengupdate state dan trigger rebuild UI |

## Cara Menjalankan

```bash
flutter clean
flutter pub get
flutter run
```


