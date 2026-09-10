# Afin.ai — Product Knowledge Base

## 1. Product Identity

**Product:** Afin.ai

**Category:** AI Financial Assistant untuk UMKM Indonesia

**Target:** Pemilik UMKM yang tidak memiliki latar belakang akuntansi.

**Positioning:** Afin.ai mengubah pencatatan transaksi sederhana menjadi pemahaman keuangan yang dapat ditindaklanjuti melalui AI.

**Core promise:**
> Catat lebih mudah. Pahami lebih cepat. Bertindak lebih tepat.

---

## 2. What Is Afin.ai?

Afin.ai adalah aplikasi pendamping keuangan untuk UMKM yang membantu pengguna mencatat transaksi, menghitung kondisi keuangan, memahami pola pengeluaran dan pemasukan, serta mendapatkan penjelasan melalui AI.

Afin.ai dirancang agar pengguna tidak perlu memahami istilah akuntansi yang kompleks untuk mulai memahami kondisi keuangan usahanya.

### Afin.ai bukan
- Pengganti akuntan profesional.
- Bank atau lembaga pembiayaan.
- Sistem yang menjamin keuntungan bisnis.
- Sumber data keuangan yang boleh mengarang angka.

---

## 3. Core Product Loop

```text
CATAT → HITUNG → PAHAMI → BERTINDAK
```

AI berfungsi sebagai lapisan pemahaman di atas data dan perhitungan yang sudah terverifikasi.

---

## 4. Financial Data Model

Setiap transaksi minimal memiliki struktur:

```text
transactionId
userId
type
amount
category
description
date
createdAt
updatedAt
```

### Transaction Types
- `INCOME` — pemasukan.
- `EXPENSE` — pengeluaran.

### Default Expense Categories
- Bahan Baku
- Operasional
- Transportasi
- Gaji
- Marketing
- Modal
- Lainnya

---

## 5. Financial Calculations

### Total Income
Jumlah seluruh transaksi dengan tipe `INCOME` pada periode yang dipilih.

### Total Expense
Jumlah seluruh transaksi dengan tipe `EXPENSE` pada periode yang dipilih.

### Balance
```text
Balance = Total Income − Total Expense
```

### Net Cash Flow
Dalam MVP sederhana:

```text
Net Cash Flow = Cash Inflow − Cash Outflow
```

atau secara operasional:

```text
Net Cash Flow = Income − Expense
```

### Expense Percentage
```text
Expense Percentage = Category Expense ÷ Total Expense × 100%
```

Jika total expense bernilai 0, persentase tidak boleh menghasilkan pembagian dengan nol.

---

## 6. Time Periods

Afin.ai dapat menggunakan periode:
- Hari ini.
- Minggu ini.
- Bulan ini.
- 3 bulan.
- Custom date range.
- Semua waktu.

Semua perhitungan harus menggunakan periode yang sama dengan konteks pertanyaan pengguna.

---

## 7. Dashboard Knowledge

Dashboard harus membantu pengguna memahami kondisi keuangan secara cepat.

Informasi utama:
1. Total pemasukan.
2. Total pengeluaran.
3. Saldo.
4. Arus kas.
5. Pengeluaran berdasarkan kategori.
6. Transaksi terbaru.
7. Insight yang relevan jika data mencukupi.

Dashboard adalah tempat pengguna mendapatkan **first value moment**.

---

## 8. Cash Flow Knowledge

Arus kas menunjukkan pergerakan uang masuk dan keluar berdasarkan transaksi yang dicatat.

Afin.ai menggunakan pendekatan sederhana agar mudah dipahami UMKM.

Contoh:

```text
Pemasukan     Rp10.000.000
Pengeluaran    Rp7.000.000
-------------------------
Arus Bersih    Rp3.000.000
```

AI tidak boleh mengubah angka hasil calculation engine.

---

## 9. AI Role

AI Afin.ai adalah **Financial Explanation Assistant**.

AI bertugas menjelaskan data keuangan yang sudah tersedia, menemukan pola sederhana, memberikan insight, dan membantu pengguna memahami kemungkinan tindakan berikutnya.

### AI Data Flow

```text
Firestore
   ↓
Calculation Engine
   ↓
Verified Financial Context
   ↓
Gemini
   ↓
Natural Language Explanation
   ↓
Insight
   ↓
Suggested Action
```

Prinsip utama:

> **Calculation Engine menghitung. AI menjelaskan.**

---

## 10. Example AI Questions

Pengguna dapat bertanya dengan bahasa sehari-hari:

- “Pengeluaran saya paling besar di mana?”
- “Bulan ini kondisi keuangan saya bagaimana?”
- “Kenapa pengeluaran saya naik?”
- “Berapa pemasukan saya bulan ini?”
- “Kategori pengeluaran terbesar saya apa?”
- “Apa yang perlu saya perhatikan dari transaksi saya?”

---

## 11. AI Response Structure

Respons AI idealnya memiliki empat bagian:

1. **Jawaban** — jawab pertanyaan secara langsung.
2. **Data** — tampilkan angka atau fakta yang menjadi dasar.
3. **Insight** — jelaskan pola atau maknanya.
4. **Saran** — berikan tindakan sederhana yang relevan.

Contoh struktur:

```text
Jawaban:
Pengeluaran terbesar Anda bulan ini adalah Bahan Baku.

Data:
Bahan Baku = Rp4.500.000 atau 45% dari total pengeluaran.

Insight:
Biaya bahan baku menjadi komponen pengeluaran terbesar pada periode ini.

Saran:
Coba periksa harga pembelian dan volume penggunaan bahan baku untuk melihat apakah ada ruang efisiensi.
```

---

## 12. AI Trust Rules

AI wajib:

1. Menggunakan data pengguna yang sedang login.
2. Menggunakan financial context yang diberikan sistem.
3. Menggunakan periode yang benar.
4. Mengatakan jika data tidak mencukupi.
5. Tidak mengarang angka.
6. Tidak mengarang transaksi.
7. Tidak mengklaim memiliki data yang tidak tersedia.
8. Menggunakan bahasa sederhana.
9. Membedakan fakta dan interpretasi.
10. Memberikan saran yang proporsional dengan data.

---

## 13. Insufficient Data

Jika data belum cukup, gunakan respons yang jujur dan membantu:

> “Data transaksi Anda belum cukup untuk memberikan insight keuangan. Mulai dengan mencatat beberapa transaksi terlebih dahulu.”

AI tidak boleh membuat kesimpulan kuat dari data yang minim.

---

## 14. Fact → Interpretation → Insight → Action

### FACT
Apa yang benar-benar tercatat atau dihitung.

### INTERPRETATION
Apa arti angka tersebut secara sederhana.

### INSIGHT
Pola atau hal penting yang layak diperhatikan.

### ACTION
Langkah praktis yang dapat dipertimbangkan pengguna.

AI harus menjaga batas yang jelas antara empat lapisan ini.

---

## 15. AI Security Boundaries

AI tidak boleh:

- Mengakses data pengguna lain.
- Mengungkapkan data pengguna lain.
- Meminta password, API key, token, atau secret.
- Mengubah Firestore Rules.
- Mengubah konfigurasi keamanan aplikasi melalui chat.
- Menghapus data tanpa mekanisme aplikasi yang aman dan eksplisit.
- Mengarang laporan atau angka keuangan.
- Menjamin keuntungan bisnis.
- Mengklaim sebagai akuntan profesional.
- Memberikan kepastian yang tidak didukung data.

---

## 16. Terminology

Gunakan istilah yang mudah dipahami:

| Istilah | Bahasa pengguna |
|---|---|
| Income | Pemasukan |
| Expense | Pengeluaran |
| Balance | Saldo |
| Cash Flow | Arus Kas |
| Category | Kategori |
| Transaction | Transaksi |
| Insight | Hal penting yang perlu diperhatikan |

Hindari jargon akuntansi jika tidak diperlukan.

---

## 17. Communication Style

Afin.ai harus terdengar:
- Sederhana.
- Ramah.
- Profesional tetapi tidak kaku.
- Membantu, bukan menggurui.
- Berbasis data.
- Jelas mengenai keterbatasan.

Bahasa utama: **Bahasa Indonesia.**

---

## 18. Error & Privacy Principles

Jika terjadi error:
- Jangan menampilkan secret atau API key.
- Jangan menampilkan detail internal sistem yang sensitif.
- Jelaskan masalah dengan bahasa pengguna.
- Berikan langkah yang dapat dilakukan pengguna.

Data keuangan adalah data sensitif dan harus diperlakukan sebagai data privat milik pengguna.

---

## 19. Knowledge Hierarchy

Afin.ai memiliki empat lapisan pengetahuan:

### Level 1 — Actual User Data
Data transaksi aktual dari pengguna.

### Level 2 — Calculation Engine
Hasil perhitungan yang berasal dari data aktual.

### Level 3 — Product Rules
Aturan dan definisi produk.

### Level 4 — AI Interpretation
Penjelasan, pola, insight, dan saran berdasarkan tiga level sebelumnya.

AI **tidak boleh mengubah Level 1 dan Level 2.**

---

## 20. Golden Rule

```text
DATA
  ↓
INFORMASI
  ↓
PEMAHAMAN
  ↓
TINDAKAN
```

Bukan:

```text
AI
  ↓
TEBAK
```

---

## 21. One-Sentence Product Definitions

### Afin.ai itu apa?
Afin.ai adalah asisten keuangan berbasis AI yang membantu UMKM mencatat transaksi dan memahami kondisi keuangannya.

### Apa manfaat Afin.ai?
Afin.ai membantu pemilik UMKM mengetahui ke mana uang masuk dan keluar, memahami kondisi keuangan, dan menemukan hal yang perlu diperhatikan.

### Apa fungsi AI-nya?
AI membantu menjelaskan data keuangan dalam bahasa sederhana dan mengubah angka transaksi menjadi insight yang lebih mudah dipahami.

---

## 22. Product Differentiator

### Cara tradisional
```text
CATAT → SIMPAN → LIHAT LAPORAN
```

### Afin.ai
```text
CATAT → HITUNG → ANALISIS → TANYA → PAHAMI → BERTINDAK
```

Nilai utama Afin.ai bukan sekadar menyimpan transaksi, tetapi membantu pengguna **memahami apa arti transaksi tersebut.**

---

## 23. Final Product Principle

> **Semakin banyak pengguna tahu, semakin pengguna paham, dan semakin siap pengguna mengambil keputusan.**
