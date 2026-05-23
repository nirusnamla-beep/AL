# Sistem Presensi Mahasiswa - Decision Tree Interaktif

README ini berisi panduan penggunaan program **Presensi Mahasiswa** berbasis Python. Program ini dibuat untuk menentukan status kehadiran mahasiswa menggunakan konsep **Decision Tree sederhana** dengan logika `if-else`.

---

## 1. Deskripsi Program

Program ini adalah aplikasi sederhana berbasis terminal atau command prompt yang digunakan untuk menentukan status mahasiswa berdasarkan data kehadiran.

Melalui program ini, pengguna dapat:

- Mencari data mahasiswa berdasarkan nama.
- Menampilkan daftar seluruh mahasiswa.
- Menambahkan data mahasiswa baru.
- Melihat statistik kehadiran mahasiswa.
- Keluar dari program.

Program ini dibuat sesuai ketentuan tugas, yaitu:

- Menggunakan bahasa pemrograman **Python**.
- Input data menggunakan **array/list**.
- Tidak menggunakan library machine learning.
- Menggunakan konsep **Decision Tree sederhana** melalui percabangan `if-else`.

---

## 2. Tujuan Program

Tujuan pembuatan program ini adalah:

1. Menerapkan konsep Decision Tree sederhana dalam program Python.
2. Menentukan status mahasiswa berdasarkan tingkat kehadiran.
3. Memberikan skor dan keterangan berdasarkan kombinasi kehadiran dan tugas.
4. Menyimpan data mahasiswa menggunakan list dua dimensi.
5. Membuat program interaktif yang mudah dijalankan melalui menu.
6. Menampilkan statistik sederhana dari data mahasiswa.

---

## 3. Konsep Decision Tree

Decision Tree adalah metode pengambilan keputusan yang menggunakan aturan tertentu untuk menentukan hasil atau klasifikasi.

Pada program ini, konsep Decision Tree dibuat secara sederhana menggunakan percabangan `if-else`.

Aturan utama yang digunakan adalah:

| Kehadiran | Status |
|---|---|
| Tinggi | Aktif |
| Rendah | Tidak Aktif |

Contohnya:

- Jika kehadiran mahasiswa **Tinggi**, maka statusnya adalah **Aktif**.
- Jika kehadiran mahasiswa **Rendah**, maka statusnya adalah **Tidak Aktif**.

Selain menentukan status, program juga memberikan **skor** dan **keterangan** berdasarkan kombinasi antara kehadiran dan tugas.

---

## 4. Struktur Data Mahasiswa

Data mahasiswa disimpan menggunakan **list dua dimensi**.

Format data yang digunakan:

```python
[NIM, Nama, Kehadiran, Tugas]
```

Contoh data:

```python
["2021001", "Andi", "Tinggi", "Lengkap"]
```

Keterangan:

| Kolom | Penjelasan |
|---|---|
| NIM | Nomor Induk Mahasiswa |
| Nama | Nama mahasiswa |
| Kehadiran | Nilai kehadiran, yaitu Tinggi atau Rendah |
| Tugas | Status tugas, yaitu Lengkap atau Tidak Lengkap |

---

## 5. Data Awal Mahasiswa

Data awal yang digunakan dalam program adalah sebagai berikut:

| NIM | Nama | Kehadiran | Tugas |
|---|---|---|---|
| 2021001 | Andi | Tinggi | Lengkap |
| 2021002 | Budi | Rendah | Tidak Lengkap |
| 2021003 | Citra | Tinggi | Tidak Lengkap |
| 2021004 | Deni | Rendah | Lengkap |
| 2021005 | Eka | Tinggi | Lengkap |

---

## 6. Aturan Keterangan dan Skor

Program tidak hanya menentukan status, tetapi juga memberikan keterangan dan skor.

| Kehadiran | Tugas | Keterangan | Skor |
|---|---|---|---|
| Tinggi | Lengkap | Mahasiswa Disiplin ★ | 100 |
| Tinggi | Tidak Lengkap | Aktif, tapi tugas perlu dilengkapi | 75 |
| Rendah | Lengkap | Tugas baik, tapi kehadiran kurang | 70 |
| Rendah | Tidak Lengkap | Perlu pembinaan akademik | 50 |

---

## 7. Fitur Program

### 7.1 Cari Mahasiswa

Fitur ini digunakan untuk mencari data mahasiswa berdasarkan nama.

Jika mahasiswa ditemukan, program akan menampilkan:

- NIM
- Nama
- Kehadiran
- Tugas
- Status
- Skor
- Keterangan

Jika mahasiswa tidak ditemukan, program akan menampilkan pesan bahwa data mahasiswa tidak tersedia dan menampilkan daftar nama mahasiswa yang ada.

---

### 7.2 Tampilkan Daftar Mahasiswa

Fitur ini digunakan untuk menampilkan seluruh data mahasiswa yang tersimpan di dalam list.

Data yang ditampilkan meliputi:

- NIM
- Nama
- Kehadiran
- Tugas

---

### 7.3 Tambah Data Mahasiswa

Fitur ini digunakan untuk menambahkan data mahasiswa baru.

Data yang harus dimasukkan adalah:

- NIM
- Nama
- Kehadiran
- Tugas

Program juga melakukan validasi input agar data yang dimasukkan sesuai format.

Format input yang benar:

| Data | Format yang Benar |
|---|---|
| Kehadiran | Tinggi atau Rendah |
| Tugas | Lengkap atau Tidak Lengkap |

Jika input tidak sesuai format, data tidak akan ditambahkan.

---

### 7.4 Statistik Kehadiran

Fitur ini digunakan untuk menampilkan statistik sederhana dari seluruh data mahasiswa.

Statistik yang ditampilkan adalah:

- Total mahasiswa.
- Jumlah mahasiswa dengan kehadiran tinggi.
- Jumlah mahasiswa dengan kehadiran rendah.
- Jumlah mahasiswa dengan tugas lengkap.
- Jumlah mahasiswa dengan tugas tidak lengkap.

---

### 7.5 Keluar

Fitur ini digunakan untuk menghentikan program.

Saat pengguna memilih menu keluar, program akan menampilkan pesan penutup dan berhenti berjalan.

---

## 8. Penjelasan Fungsi Program

### 8.1 Fungsi `tentukan_status(kehadiran)`

Fungsi ini digunakan untuk menentukan status mahasiswa berdasarkan kehadiran.

Logikanya:

```python
if kehadiran == "Tinggi":
    return "Aktif"
else:
    return "Tidak Aktif"
```

Artinya:

- Kehadiran **Tinggi** menghasilkan status **Aktif**.
- Kehadiran selain **Tinggi** menghasilkan status **Tidak Aktif**.

---

### 8.2 Fungsi `tentukan_keterangan_skor(kehadiran, tugas)`

Fungsi ini digunakan untuk menentukan keterangan dan skor mahasiswa.

Penentuan dilakukan berdasarkan kombinasi antara kehadiran dan tugas.

Contoh:

Jika mahasiswa memiliki kehadiran **Tinggi** dan tugas **Lengkap**, maka mahasiswa tersebut mendapat:

- Status: Aktif
- Skor: 100
- Keterangan: Mahasiswa Disiplin ★

---

### 8.3 Fungsi `tampilkan_menu()`

Fungsi ini digunakan untuk menampilkan menu utama program.

Menu yang ditampilkan adalah:

1. Cari mahasiswa
2. Tampilkan daftar mahasiswa
3. Tambah data mahasiswa
4. Statistik kehadiran
5. Keluar

---

### 8.4 Fungsi `cari_mahasiswa()`

Fungsi ini digunakan untuk mencari mahasiswa berdasarkan nama.

Pencarian dibuat tidak sensitif terhadap huruf besar dan kecil menggunakan `.lower()`.

Contoh:

Jika data mahasiswa bernama **Andi**, pengguna tetap bisa mencari dengan mengetik:

```text
andi
```

atau

```text
ANDI
```

Program tetap akan menemukan data tersebut.

---

### 8.5 Fungsi `tampilkan_daftar_mahasiswa()`

Fungsi ini digunakan untuk menampilkan seluruh data mahasiswa.

Data ditampilkan menggunakan perulangan `for`.

---

### 8.6 Fungsi `tambah_data_mahasiswa()`

Fungsi ini digunakan untuk menambahkan data mahasiswa baru ke dalam list `data_mahasiswa`.

Sebelum data ditambahkan, program akan memeriksa apakah input kehadiran dan tugas sudah sesuai format.

---

### 8.7 Fungsi `tampilkan_statistik()`

Fungsi ini digunakan untuk menghitung dan menampilkan statistik sederhana.

Statistik dihitung dari seluruh data yang tersimpan di dalam list.

---

### 8.8 Fungsi `main()`

Fungsi `main()` adalah fungsi utama yang menjalankan program.

Di dalam fungsi ini terdapat perulangan:

```python
while True:
```

Perulangan tersebut membuat menu terus tampil sampai pengguna memilih menu keluar.

---

## 9. Cara Menjalankan Program

Ikuti langkah-langkah berikut untuk menjalankan program.

### Langkah 1: Pastikan Python Sudah Terinstal

Pastikan Python sudah terinstal di komputer atau laptop.

Untuk mengecek versi Python, buka terminal atau command prompt, lalu ketik:

```bash
python --version
```

atau:

```bash
python3 --version
```

---

### Langkah 2: Buat File Program

Buat file Python dengan nama:

```text
presensi_mahasiswa.py
```

Kemudian salin source code program ke dalam file tersebut.

---

### Langkah 3: Jalankan Program

Buka terminal atau command prompt pada folder tempat file disimpan, lalu jalankan perintah:

```bash
python presensi_mahasiswa.py
```

Jika menggunakan Python 3 di beberapa perangkat, gunakan:

```bash
python3 presensi_mahasiswa.py
```

---

### Langkah 4: Pilih Menu

Setelah program berjalan, pengguna dapat memilih menu dengan memasukkan angka 1 sampai 5.

Contoh:

```text
Pilih menu (1-5): 1
```

---

## 10. Contoh Tampilan Program

Saat program dijalankan, tampilan awalnya kurang lebih seperti berikut:

```text
======================================================================
SISTEM PRESENSI MAHASISWA - DECISION TREE
Teknik Informatika | Tahun Akademik 2024/2025
======================================================================
Waktu Akses : 23 May 2026    14:30:20
======================================================================

MENU UTAMA
1. Cari mahasiswa
2. Tampilkan daftar mahasiswa
3. Tambah data mahasiswa
4. Statistik kehadiran
5. Keluar
Pilih menu (1-5):
```

---

## 11. Contoh Penggunaan Menu Cari Mahasiswa

Misalnya pengguna memilih menu **Cari mahasiswa** dan mengetik nama **Andi**.

Contoh output:

```text
--------------------------------------------------
NIM         : 2021001
Nama        : Andi
Kehadiran   : Tinggi
Tugas       : Lengkap
Status      : Aktif
Skor        : 100 / 100
Keterangan  : Mahasiswa Disiplin ★
--------------------------------------------------
```

Dari output tersebut, dapat disimpulkan bahwa Andi memiliki kehadiran tinggi dan tugas lengkap, sehingga statusnya adalah aktif dengan skor 100.

---

## 12. Source Code Program

Simpan kode berikut dengan nama file `presensi_mahasiswa.py`.

```python
# ============================================================
# Program Presensi Mahasiswa - Decision Tree Interaktif
# ============================================================
# Program ini digunakan untuk menentukan status kehadiran mahasiswa
# berdasarkan data kehadiran dan tugas.
#
# Konsep yang digunakan:
# - Decision Tree sederhana menggunakan percabangan IF-ELSE
# - Input data menggunakan array/list
# - Tidak menggunakan library machine learning
#
# Aturan Decision Tree:
# Jika Kehadiran = Tinggi -> Status = Aktif
# Jika Kehadiran = Rendah -> Status = Tidak Aktif
# ============================================================

from datetime import datetime


# ============================================================
# DATA MAHASISWA
# ============================================================
# Data mahasiswa disimpan menggunakan list 2 dimensi.
#
# Format data:
# [NIM, Nama, Kehadiran, Tugas]
# ============================================================

data_mahasiswa = [
    ["2021001", "Andi", "Tinggi", "Lengkap"],
    ["2021002", "Budi", "Rendah", "Tidak Lengkap"],
    ["2021003", "Citra", "Tinggi", "Tidak Lengkap"],
    ["2021004", "Deni", "Rendah", "Lengkap"],
    ["2021005", "Eka", "Tinggi", "Lengkap"]
]


# ============================================================
# FUNGSI MENENTUKAN STATUS MAHASISWA
# ============================================================
# Fungsi ini menentukan status mahasiswa berdasarkan kehadiran.
#
# Jika kehadiran Tinggi, maka status Aktif.
# Jika kehadiran Rendah, maka status Tidak Aktif.
# ============================================================

def tentukan_status(kehadiran):
    if kehadiran == "Tinggi":
        return "Aktif"
    else:
        return "Tidak Aktif"


# ============================================================
# FUNGSI MENENTUKAN KETERANGAN DAN SKOR
# ============================================================
# Fungsi ini menentukan keterangan dan skor berdasarkan
# kombinasi antara kehadiran dan tugas mahasiswa.
# ============================================================

def tentukan_keterangan_skor(kehadiran, tugas):
    if kehadiran == "Tinggi" and tugas == "Lengkap":
        return "Mahasiswa Disiplin ★", 100

    elif kehadiran == "Tinggi" and tugas == "Tidak Lengkap":
        return "Aktif, tapi tugas perlu dilengkapi", 75

    elif kehadiran == "Rendah" and tugas == "Lengkap":
        return "Tugas baik, tapi kehadiran kurang", 70

    else:
        return "Perlu pembinaan akademik", 50


# ============================================================
# HEADER PROGRAM
# ============================================================
# Bagian ini menampilkan judul program, identitas program,
# dan waktu akses ketika program dijalankan.
# ============================================================

print("=" * 70)
print("SISTEM PRESENSI MAHASISWA - DECISION TREE")
print("Teknik Informatika | Tahun Akademik 2024/2025")
print("=" * 70)
print("Waktu Akses :", datetime.now().strftime("%d %b %Y    %H:%M:%S"))
print("=" * 70)


# ============================================================
# FUNGSI MENAMPILKAN MENU UTAMA
# ============================================================

def tampilkan_menu():
    print("\nMENU UTAMA")
    print("1. Cari mahasiswa")
    print("2. Tampilkan daftar mahasiswa")
    print("3. Tambah data mahasiswa")
    print("4. Statistik kehadiran")
    print("5. Keluar")


# ============================================================
# FUNGSI CARI MAHASISWA
# ============================================================
# Fungsi ini digunakan untuk mencari data mahasiswa
# berdasarkan nama yang dimasukkan oleh pengguna.
# ============================================================

def cari_mahasiswa():
    nama_cari = input("Masukkan nama mahasiswa : ").strip()

    mahasiswa_ditemukan = None

    for mhs in data_mahasiswa:
        if mhs[1].lower() == nama_cari.lower():
            mahasiswa_ditemukan = mhs
            break

    print("\n" + "-" * 50)

    if mahasiswa_ditemukan:
        nim, nama, kehadiran, tugas = mahasiswa_ditemukan

        status = tentukan_status(kehadiran)
        keterangan, skor = tentukan_keterangan_skor(kehadiran, tugas)

        print(f"NIM         : {nim}")
        print(f"Nama        : {nama}")
        print(f"Kehadiran   : {kehadiran}")
        print(f"Tugas       : {tugas}")
        print(f"Status      : {status}")
        print(f"Skor        : {skor} / 100")
        print(f"Keterangan  : {keterangan}")

    else:
        print(f"Maaf, mahasiswa dengan nama '{nama_cari}' tidak ditemukan.")
        print("Daftar nama yang tersedia:")
        print(", ".join([mhs[1] for mhs in data_mahasiswa]))

    print("-" * 50)


# ============================================================
# FUNGSI MENAMPILKAN DAFTAR MAHASISWA
# ============================================================
# Fungsi ini menampilkan seluruh data mahasiswa
# yang ada di dalam list data_mahasiswa.
# ============================================================

def tampilkan_daftar_mahasiswa():
    print("\n" + "-" * 50)
    print("DAFTAR MAHASISWA")

    for mhs in data_mahasiswa:
        print(f"{mhs[0]} - {mhs[1]} | Kehadiran: {mhs[2]} | Tugas: {mhs[3]}")

    print("-" * 50)


# ============================================================
# FUNGSI TAMBAH DATA MAHASISWA
# ============================================================
# Fungsi ini digunakan untuk menambahkan data mahasiswa baru.
# Data yang dimasukkan akan divalidasi terlebih dahulu.
# ============================================================

def tambah_data_mahasiswa():
    print("\nTambah data mahasiswa baru")

    nim = input("Masukkan NIM : ").strip()
    nama = input("Masukkan nama : ").strip().title()
    kehadiran = input("Kehadiran (Tinggi/Rendah) : ").strip().title()
    tugas = input("Tugas (Lengkap/Tidak Lengkap) : ").strip().title()

    if kehadiran not in ["Tinggi", "Rendah"] or tugas not in ["Lengkap", "Tidak Lengkap"]:
        print("Input tidak valid. Gunakan format yang benar.")
        return

    data_mahasiswa.append([nim, nama, kehadiran, tugas])

    print(f"Data mahasiswa {nama} berhasil ditambahkan.")


# ============================================================
# FUNGSI STATISTIK MAHASISWA
# ============================================================
# Fungsi ini menampilkan statistik sederhana berdasarkan
# data mahasiswa yang tersimpan.
# ============================================================

def tampilkan_statistik():
    total = len(data_mahasiswa)

    hadir_tinggi = sum(1 for mhs in data_mahasiswa if mhs[2] == "Tinggi")
    hadir_rendah = total - hadir_tinggi

    tugas_lengkap = sum(1 for mhs in data_mahasiswa if mhs[3] == "Lengkap")
    tugas_tidak = total - tugas_lengkap

    print("\n" + "-" * 50)
    print("STATISTIK MAHASISWA")
    print(f"Total mahasiswa    : {total}")
    print(f"Kehadiran Tinggi   : {hadir_tinggi}")
    print(f"Kehadiran Rendah   : {hadir_rendah}")
    print(f"Tugas Lengkap      : {tugas_lengkap}")
    print(f"Tugas Tidak Lengkap: {tugas_tidak}")
    print("-" * 50)


# ============================================================
# FUNGSI UTAMA PROGRAM
# ============================================================
# Fungsi main() digunakan untuk menjalankan menu utama.
# Program akan terus berjalan sampai pengguna memilih keluar.
# ============================================================

def main():
    while True:
        tampilkan_menu()

        pilihan = input("Pilih menu (1-5): ").strip()

        if pilihan == "1":
            cari_mahasiswa()

        elif pilihan == "2":
            tampilkan_daftar_mahasiswa()

        elif pilihan == "3":
            tambah_data_mahasiswa()

        elif pilihan == "4":
            tampilkan_statistik()

        elif pilihan == "5":
            print("\nTerima kasih. Program selesai.")
            break

        else:
            print("Pilihan tidak valid. Silakan coba lagi.")

    input("Tekan Enter untuk keluar...")


# ============================================================
# PEMANGGILAN PROGRAM
# ============================================================
# Baris ini memastikan program berjalan ketika file dijalankan
# secara langsung.
# ============================================================

if __name__ == "__main__":
    main()
```

---

## 13. Kesimpulan

Program Presensi Mahasiswa ini merupakan contoh penerapan konsep **Decision Tree sederhana** menggunakan bahasa pemrograman Python.

Program menentukan status mahasiswa berdasarkan kehadiran. Jika kehadiran mahasiswa tinggi, maka mahasiswa dinyatakan **Aktif**. Jika kehadiran mahasiswa rendah, maka mahasiswa dinyatakan **Tidak Aktif**.

Program ini juga dilengkapi dengan fitur pencarian mahasiswa, penampilan daftar mahasiswa, penambahan data mahasiswa baru, dan statistik sederhana.

Dengan menggunakan list sebagai tempat penyimpanan data dan percabangan `if-else` sebagai logika Decision Tree, program ini sudah sesuai dengan ketentuan tugas karena menggunakan Python, input data berupa array/list, dan tidak menggunakan library machine learning.
