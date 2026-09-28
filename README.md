# Sistem Manajemen Data Menu Restoran

## Nama: Muhammad Arzad
## Kelas: A'2025
## NIM: 2509116014

## 1. Deskripsi Proyek

Sistem Manajemen Data Menu Restoran merupakan program berbasis Java yang digunakan untuk mengelola data kategori dan menu restoran melalui tampilan terminal. Program ini memiliki fitur untuk menambah, menampilkan, mengubah, dan menghapus data menu, serta menambah dan menampilkan data kategori.

Program ini dibuat untuk memenuhi tugas Ujian Tengah Semester (UTS) mata kuliah Pemrograman Berorientasi Objek (PBO) dengan studi kasus pengelolaan menu restoran. Data disimpan sementara di dalam memori menggunakan `ArrayList`, sehingga saat program ditutup data akan kembali ke data awal.

---

## 2. Fitur Program

### 2.1 Tambah Kategori

Pengguna memasukkan ID kategori, nama kategori, dan deskripsi. Program memeriksa ID terlebih dahulu agar tidak ada ID yang sama.

### 2.2 Tampilkan Kategori

Program menampilkan seluruh kategori yang tersimpan, yaitu ID, nama, dan deskripsi kategori.

### 2.3 Tambah Menu

Pengguna memasukkan ID menu, nama menu, kategori, harga, dan jenis menu (Makanan atau Minuman). Program memeriksa ID menu terlebih dahulu agar tidak ada ID yang sama.

### 2.4 Tampilkan Menu

Program menampilkan seluruh menu yang tersimpan. Informasi yang muncul menyesuaikan jenis menu, yaitu Jenis Makanan untuk menu makanan dan Jenis Minuman untuk menu minuman.

### 2.5 Update Menu

Pengguna memasukkan ID menu, lalu memperbarui nama, kategori, harga, dan jenis makanan atau minuman.

### 2.6 Hapus Menu

Pengguna memasukkan ID menu yang ingin dihapus. Jika ID ditemukan, menu dihapus dari daftar. Jika tidak, program menampilkan pesan bahwa menu tidak ditemukan.

---

## 3. Struktur Program

```
Ujian_Tengah_Semester_Matkul_PBO/
├── pom.xml
├── README.md
└── src/main/java/com/mycompany/sistemmanajemendatamenurestoran/
    ├── SistemManajemenDataMenuRestoran.java
    └── model/
        ├── Kategori.java
        ├── Menu.java
        ├── MenuMakanan.java
        ├── MenuMinuman.java
        └── Restoran.java
```

| Class | Fungsi |
|-------|--------|
| `SistemManajemenDataMenuRestoran` | Class utama. Berisi `main()`, menu utama, dan input pengguna. |
| `Restoran` | Mengelola daftar menu dan daftar kategori (tambah, cari, update, hapus). |
| `Kategori` | Menyimpan data kategori: `idKategori`, `namaKategori`, `deskripsi`. |
| `Menu` | Class dasar (superclass) berisi data umum menu: `idMenu`, `namaMenu`, `kategori`, `harga`. |
| `MenuMakanan` | Turunan `Menu` dengan tambahan `jenisMakanan`. |
| `MenuMinuman` | Turunan `Menu` dengan tambahan `jenisMinuman`. |

---

## 4. Alur Program

### 4.1 Inisialisasi Data

Saat program dijalankan, sistem membuat object `Restoran` beserta data awal:

- Kategori `K001 - Makanan` dan `K002 - Minuman`
- Menu `M001 - Nasi Goreng` dan `M002 - Es Teh`

### 4.2 Menu Utama

Setelah data awal siap, program menampilkan menu utama:

1. Tambah Kategori
2. Tampilkan Kategori
3. Tambah Menu
4. Tampilkan Menu
5. Update Menu
6. Hapus Menu
7. Keluar

Pengguna memilih fitur dengan memasukkan nomor 1 sampai 7.

### 4.3 Proses Setiap Pilihan

- **Tambah Kategori**: pengguna mengisi ID, nama, dan deskripsi. Jika ID belum dipakai, kategori disimpan.
- **Tampilkan Kategori**: program menampilkan semua kategori satu per satu.
- **Tambah Menu**: pengguna mengisi data menu dan memilih jenis menu. Jika memilih makanan, program membuat object `MenuMakanan`. Jika memilih minuman, program membuat object `MenuMinuman`.
- **Tampilkan Menu**: program menampilkan semua menu dengan method `tampilkanInfo()`.
- **Update Menu**: program mencari menu berdasarkan ID, menampilkan data saat ini, lalu pengguna mengisi data baru.
- **Hapus Menu**: program mencari menu berdasarkan ID, lalu menghapusnya dari daftar.
- **Keluar**: perulangan utama berhenti dan program selesai.

Setelah setiap proses selesai (kecuali Keluar), program kembali menampilkan menu utama.

---

## 5. Elemen Wajib dan Penerapan Konsep PBO

| Elemen Wajib | Penerapan pada Program |
|--------------|------------------------|
| Inheritance (minimal 2 tipe) | `MenuMakanan` dan `MenuMinuman` merupakan turunan dari `Menu` |
| Polymorphism | Method overriding pada `tampilkanInfo()` di `MenuMakanan` dan `MenuMinuman` |
| Condition (if else) | Pengecekan ID, jenis menu, dan hasil operasi pada `Restoran` dan class utama |
| Looping | `while` pada menu utama dan input, `for` pada pencarian dan penampilan data |

### 5.1 Inheritance

`MenuMakanan` dan `MenuMinuman` mewarisi attribute dan method dari `Menu`. Dengan demikian terdapat dua tipe turunan dari satu superclass:

```java
public class MenuMakanan extends Menu
public class MenuMinuman extends Menu
```

Keduanya memakai data umum dari `Menu` (ID, nama, kategori, harga) dan menambahkan data khusus masing-masing, yaitu `jenisMakanan` pada `MenuMakanan` dan `jenisMinuman` pada `MenuMinuman`.

### 5.2 Polymorphism

Daftar menu bertipe `Menu`, tetapi dapat berisi `MenuMakanan` maupun `MenuMinuman`:

```java
private ArrayList<Menu> daftarMenu;
```

`MenuMakanan` dan `MenuMinuman` melakukan overriding terhadap method `tampilkanInfo()` milik `Menu`:

```java
@Override
public void tampilkanInfo() {
    // menampilkan data menu beserta jenisMakanan
}
```

Saat menampilkan menu, method yang berjalan menyesuaikan jenis object yang sebenarnya:

```java
for (Menu menu : restoran.getDaftarMenu()) {
    menu.tampilkanInfo();
}
```

### 5.3 Condition (If Else)

Kondisi digunakan untuk menentukan alur program. Contoh pada proses tambah kategori:

```java
if (restoran.tambahKategori(kategoriBaru)) {
    System.out.println(">> Kategori berhasil ditambahkan");
} else {
    System.out.println(">> ID Kategori sudah digunakan");
}
```

Contoh lain pada proses update, untuk menentukan jenis menu yang diperbarui:

```java
if (menu instanceof MenuMakanan) {
    MenuMakanan makanan = (MenuMakanan) menu;
    makanan.setJenisMakanan(jenisBaru);
} else if (menu instanceof MenuMinuman) {
    MenuMinuman minuman = (MenuMinuman) menu;
    minuman.setJenisMinuman(jenisBaru);
}
```

### 5.4 Looping

Perulangan `while` menjaga program tetap berjalan sampai pengguna memilih Keluar:

```java
while (berjalan) {
    tampilkanMenuUtama();
    // proses pilihan pengguna
}
```

Perulangan `for` digunakan untuk mencari data pada daftar, misalnya pada pencarian menu:

```java
for (Menu menu : daftarMenu) {
    if (menu.getIdMenu().equals(idMenu)) {
        return menu;
    }
}
```

### 5.5 Encapsulation (Tambahan)

Attribute dibuat `private` dan hanya bisa diakses lewat getter dan setter:

```java
private String namaMenu;

public String getNamaMenu() {
    return namaMenu;
}

public void setNamaMenu(String namaMenu) {
    this.namaMenu = namaMenu;
}
```

Class `Restoran` juga melindungi daftar internalnya dengan `Collections.unmodifiableList()`, sehingga daftar tidak bisa diubah langsung dari luar class.

---

## 6. Validasi Input

Program memiliki validasi agar data yang dimasukkan sesuai aturan.

| Kondisi | Pesan Program |
|---------|---------------|
| Input dikosongkan | `>> Input tidak boleh kosong` |
| Pilihan menu bukan angka | `>> Input harus berupa angka` |
| Pilihan di luar rentang | `>> Pilihan harus antara 1 dan 7` |
| Harga bukan angka | `>> Harga harus berupa angka` |
| Harga negatif | `>> Harga tidak boleh negatif` |
| ID menu sudah dipakai | `>> ID Menu sudah digunakan` |
| ID kategori sudah dipakai | `>> ID Kategori sudah digunakan` |
| ID kategori tidak ditemukan | `>> Kategori tidak ditemukan` |

---

## 7. Dokumentasi Program

Dokumentasi program digunakan untuk menunjukkan hasil penggunaan fitur yang telah dibuat.

### 7.1 Tampilan Menu Utama

Menampilkan pilihan fitur yang dapat digunakan oleh pengguna.

**Dokumentasi:**

<img width="363" height="190" alt="image" src="https://github.com/user-attachments/assets/e286c8cb-4a6e-4417-bf8e-50fd823727d7" />


### 7.2 Menampilkan Kategori

Menampilkan data kategori yang telah tersedia di dalam sistem.

**Dokumentasi:**

<img width="371" height="393" alt="image" src="https://github.com/user-attachments/assets/644f190c-293c-4bdf-8a8f-df0889cdf249" />


### 7.3 Menampilkan Menu

Menampilkan data menu yang telah tersedia, termasuk dummy data yang diberikan pada saat program dijalankan.

<img width="359" height="467" alt="image" src="https://github.com/user-attachments/assets/24e06034-6533-448d-8ef5-21a356f7dfdf" />

---

<img width="355" height="212" alt="image" src="https://github.com/user-attachments/assets/046e69f0-4e60-4a7e-a87f-8669f6067f50" />


### 7.4 Menambahkan Kategori

Menampilkan proses ketika pengguna menambahkan kategori baru.

**Dokumentasi:**

<img width="359" height="319" alt="image" src="https://github.com/user-attachments/assets/9b331b88-60d6-437e-a75b-db2b01c49c03" />


### 7.5 Menambahkan Menu

Menampilkan proses penambahan menu baru dengan memilih kategori dan jenis menu.

**Dokumentasi:**

<img width="361" height="569" alt="image" src="https://github.com/user-attachments/assets/4fec72c1-fd7d-444e-b223-84da828bb3b6" />


### 7.6 Memperbarui Menu

Menampilkan proses perubahan data menu yang meliputi nama, kategori, harga, dan jenis menu.

**Dokumentasi:**

<img width="359" height="640" alt="image" src="https://github.com/user-attachments/assets/3dbadf98-e7d6-4f7a-ac08-cc526dd8f5e3" />

### 7.7 Menghapus Menu

Menampilkan proses penghapusan data menu berdasarkan ID menu.

**Dokumentasi:**

<img width="355" height="277" alt="image" src="https://github.com/user-attachments/assets/36ee38a1-c040-4272-9ba8-2670bcd9f3aa" />

### 7.8 Validasi Input

Menampilkan contoh ketika program menangani input yang tidak sesuai, seperti input kosong, harga negatif, atau input bukan angka.

**Dokumentasi:**

<img width="368" height="230" alt="image" src="https://github.com/user-attachments/assets/66fc279f-fc7b-497f-baac-06e3c7769eec" />

---

<img width="362" height="274" alt="image" src="https://github.com/user-attachments/assets/2c455e39-1725-474f-9ed6-c905e7b48c02" />

---

<img width="357" height="652" alt="image" src="https://github.com/user-attachments/assets/2e3aba16-bc94-40f1-80f6-cfe5d800e89c" />

---
