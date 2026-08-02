# PATCH — Iterasi 1 dari Uji Pengguna
MR KPR · perbaikan berdasarkan masukan pengguna nyata

Tempel berkas ini ke folder proyek, lalu minta Claude Code mengerjakannya. Perbaiki **berurutan**, jangan sekaligus, dan periksa satu per satu.

---

## Masukan yang masuk

| # | Kata pengguna | Terjemahannya |
|---|---|---|
| 1 | "Begitu buka link, bingung karena langsung disodorin form. Tidak ada perkenalan atau aba-aba dulu." | Tidak ada konteks. Pengguna tidak tahu ini situs apa dan kenapa ia harus mengisi |
| 2 | "Sudah dapat hasil angka-angka, tapi bingung habis itu harus apa?" | Tidak ada langkah lanjutan yang jelas setelah momen paling menentukan |
| 3 | "Angka rupiah tidak ada titiknya jadi bingung. Persentasenya perlu ada, tenornya dalam bulan saja." | Isian sulit dibaca dan satuannya tidak sesuai kebiasaan |

---

# PERBAIKAN 1 — Beri konteks sebelum formulir

## Apa yang salah

Rancangan sekarang bertaruh bahwa pengunjung langsung paham begitu melihat kalkulator. Ternyata tidak. Mereka butuh tahu **ini situs apa** dan **kenapa harus mengisi** sebelum menyentuh isian pertama.

## Yang TIDAK boleh dilakukan

Jangan mengembalikan halaman perkenalan panjang sebelum kalkulator. Itu rancangan lama yang sudah dibuang, dan mengembalikannya berarti membuang keunggulan utamanya: nilai muncul dalam sepuluh detik.

Perbaikannya harus **menambah konteks tanpa menambah langkah.**

## Yang dibangun

Di atas tiga isian, tambahkan blok pengantar singkat. Seluruhnya tetap terlihat tanpa perlu menggulir.

**Susunannya dari atas ke bawah:**

1. **Nama layanan** — `MR KPR` dengan penanda kecil di bawahnya: `Konsultan penurunan cicilan KPR`

2. **Judul besar** (tetap seperti sekarang):
   > **Cicilan KPR Anda naik?**
   > **Lihat berapa yang bisa turun.**

3. **Paragraf pengantar — INI YANG BARU.** Dua kalimat, tidak lebih:
   > "Setelah masa bunga tetap habis, cicilan KPR ikut naik dan banyak orang mengira itu tidak bisa diubah. Isi tiga angka di bawah, dan Anda langsung tahu berapa cicilan Anda berpotensi turun."

4. **Tiga penanda kepercayaan** dalam satu baris, ikon kecil dan teks pendek:
   - `Gratis` — tanpa biaya jasa
   - `Tanpa daftar` — tidak perlu akun
   - `± 30 detik` — cukup tiga angka

   Ini menjawab kecemasan yang tidak diucapkan: "apakah saya akan ditagih?" dan "apakah data saya diminta?"

5. **Judul kecil di atas isian:** `Isi tiga angka ini`

6. Baru tiga isiannya

## Yang harus dijaga

Seluruh blok ini **tidak boleh mendorong tombol hitung keluar dari layar pertama** pada ponsel ukuran sedang. Kalau ternyata terdorong, perpendek paragrafnya, jangan hapus penanda kepercayaannya.

## Cara mengujinya

Buka di HP tanpa menggulir. Harus terlihat sekaligus: nama layanan, judul, paragraf, tiga penanda, tiga isian, dan tombolnya.

---

# PERBAIKAN 2 — Perjelas langkah setelah hasil

## Apa yang salah

Ini masukan yang paling mahal. Pengguna sampai di momen paling menentukan — sudah melihat angkanya, sudah tertarik — lalu berhenti karena tidak tahu harus apa.

Kemungkinan penyebabnya: ada terlalu banyak hal yang bisa diklik setelah hasil muncul, sehingga tidak ada yang menonjol. Tombol "mau dibantu", tautan "hitung ulang", dan bagian penjelasan di bawah saling berebut perhatian.

## Yang dibangun

**a. Satu kalimat penutup di dalam kartu hasil**

Tepat di bawah angka besarnya, sebelum kotak peringatan estimasi:

> "Angka ini bisa jadi kenyataan kalau KPR Anda dipindahkan ke bank dengan penawaran lebih rendah. Pengurusannya kami yang kerjakan."

**b. Blok "Langkah selanjutnya" — INI YANG PALING PENTING**

Persis di bawah kartu hasil, sebuah kartu berisi tiga langkah bernomor:

> **Langkah selanjutnya**
>
> **1. Isi data KPR Anda** — Delapan pertanyaan singkat, dijawab sambil ngobrol. Sekitar dua menit.
>
> **2. Konsultan kami menilai kasus Anda** — Kami cek kelayakannya dan tentukan jalur yang paling masuk akal.
>
> **3. Kami hubungi lewat WhatsApp** — Kalau layak, kami urus dokumennya sampai akad. Anda tidak keluar biaya apa pun ke kami.

Lalu tombol oranye lebar penuh: **"Mulai, isi data KPR saya"**

**c. Kurangi yang berebut perhatian**

- Tautan "Hitung ulang dengan angka lain" dikecilkan dan dipindah ke **bawah** tombol utama, bukan sejajar dengannya
- Bagian penjelasan "kenapa ini terjadi" diberi jarak pemisah yang jelas, dan didahului judul kecil: `Masih ragu? Ini penjelasannya.`

  Dengan begitu, penjelasan itu jadi jalur bagi yang ragu, bukan penghalang bagi yang sudah siap.

**d. Satu tindakan utama saja**

Aturan yang dipegang: dalam satu layar hanya boleh ada **satu tombol berwarna penuh**. Sisanya berupa tautan teks atau tombol bergaris. Kalau ada dua tombol sama mencoloknya, pengguna berhenti untuk memilih, dan berhenti adalah musuhnya.

## Cara mengujinya

Tunjukkan layar hasil ke orang lain, tanya: "menurutmu apa yang harus dilakukan sekarang?" Kalau ragu lebih dari dua detik, belum selesai.

---

# PERBAIKAN 3 — Perbaiki isian dan satuan

## 3a. Titik ribuan otomatis pada isian rupiah

Berlaku untuk isian **cicilan per bulan** dan **plafon awal**.

**Perilaku:** saat pengguna mengetik, angkanya otomatis diberi titik pemisah ribuan. Mengetik `12500000` tampil sebagai `12.500.000`.

**Cara membangunnya:**

```javascript
function pasangFormatRupiah(el){
  el.setAttribute('type','text');        // wajib, karena input number menolak titik
  el.setAttribute('inputmode','numeric'); // papan tik ponsel tetap menampilkan angka
  el.addEventListener('input', function(){
    var posisi = el.selectionStart;
    var panjangLama = el.value.length;
    var bersih = el.value.replace(/\D/g,'');
    el.value = bersih ? Number(bersih).toLocaleString('id-ID') : '';
    // jaga posisi kursor supaya tidak melompat ke ujung saat menyunting
    var selisih = el.value.length - panjangLama;
    el.setSelectionRange(posisi + selisih, posisi + selisih);
  });
}

// ambil nilai angkanya saat dihitung
function angkaDari(el){
  return Number(String(el.value).replace(/\D/g,'')) || 0;
}
```

**Penting:** jenis isian berubah dari `number` menjadi `text`, karena isian `number` menolak titik. Karena itu setiap tempat yang membaca nilainya **wajib** memakai `angkaDari()`, bukan `+el.value`. Kalau ada satu saja yang terlewat, perhitungannya akan menghasilkan nol atau NaN.

**Awalan Rp di dalam isian:** tampilkan `Rp` sebagai teks abu-abu tetap di sisi kiri dalam kotak isian, bukan sebagai bagian dari nilainya. Cukup dengan wadah berposisi relatif dan `padding-left` pada isiannya.

## 3b. Tanda persen pada isian bunga

Tampilkan `%` sebagai teks abu-abu tetap di sisi **kanan** dalam kotak isian bunga. Bukan bagian dari nilainya, hanya penanda.

Isian bunga tetap menerima desimal — pengguna bisa mengetik `10,5` atau `10.5`. Saat dibaca, koma diubah jadi titik lebih dulu:

```javascript
function persenDari(el){
  return parseFloat(String(el.value).replace(',','.')) || 0;
}
```

Orang Indonesia menulis desimal dengan koma. Kalau hanya titik yang diterima, `10,5` akan terbaca sebagai `10` dan hasilnya meleset tanpa ada yang sadar.

## 3c. Sisa tenor dalam bulan, bukan tahun

**Ini perubahan yang menyentuh banyak tempat. Kerjakan dengan teliti.**

**Yang berubah:**

1. Label isian: `Sisa tenor (bulan)` dengan petunjuk: *"Berapa bulan lagi KPR Anda berjalan. Contoh: 132 bulan untuk 11 tahun."*
2. Nilai disimpan sebagai `sisaBulan`, bukan `sisaTenor`
3. Perhitungan memakai `sisaBulan` langsung, **hapus perkalian `× 12`**
4. Validasi: minimal 1 bulan, maksimal 360 bulan
5. **Setiap tempat yang menampilkan tenor** harus ikut diubah:
   - Ringkasan data klien di halaman Proses Saya
   - Lembar detail konsultan
   - Kartu prospek mitra bank
   - Kolom CSV: ubah judulnya jadi `Sisa tenor (bulan)`
   - Pesan WhatsApp
6. **Data contoh di bagian 13 brief** harus dikonversi: 11 tahun jadi 132, 9 tahun jadi 108, 14 tahun jadi 168

**Bantuan pembacaan:** di bawah isian, tampilkan terjemahannya secara langsung. Mengetik `132` memunculkan tulisan kecil: *"= 11 tahun"*. Ini menjawab orang yang hafal tenornya dalam tahun.

**Peringatan:** aturan penilaian di bagian 6 brief **tidak memakai sisa tenor sama sekali**, jadi mesin penilaiannya tidak terpengaruh. Pastikan Claude Code tidak "merapikan" bagian itu sekalian.

---

# Urutan pengerjaan

Kerjakan berurutan. Setiap nomor selesai, periksa dulu, baru lanjut.

1. **Perbaikan 3** dulu, karena paling teknis dan paling mudah dipastikan benar atau salah
2. **Perbaikan 2**, karena dampaknya paling besar
3. **Perbaikan 1**, karena paling ringan

---

# Titik periksa setelah semuanya selesai

- [ ] Mengetik di isian cicilan memunculkan titik ribuan otomatis
- [ ] Kursor tidak melompat ke ujung saat menyunting angka di tengah
- [ ] `Rp` terlihat di kiri isian, `%` di kanan isian bunga
- [ ] Mengetik `10,5` pada bunga menghasilkan perhitungan yang benar, bukan `10`
- [ ] Isian tenor berlabel bulan, mengetik `132` memunculkan "= 11 tahun"
- [ ] Perhitungan tetap benar: 12.500.000 / 10 / 132 menghasilkan penghematan yang masuk akal
- [ ] Seluruh tampilan tenor sudah dalam bulan: Proses Saya, detail konsultan, kartu bank, CSV, pesan WhatsApp
- [ ] Data contoh sudah dikonversi ke bulan dan jalurnya tetap `hi`, `hi`, `mid`, `alt`
- [ ] Layar hasil punya blok "Langkah selanjutnya" berisi tiga langkah
- [ ] Hanya ada satu tombol berwarna penuh di layar hasil
- [ ] Halaman depan punya paragraf pengantar dan tiga penanda kepercayaan
- [ ] Di HP, tombol hitung masih terlihat tanpa perlu menggulir
- [ ] Mesin penilaian di bagian 6 tidak berubah sama sekali

---

# Untuk slide Iterate Fast

Brief meminta **satu** perubahan cepat, bukan semuanya. Kalau slide-mu hanya memuat satu, pilih **Perbaikan 2**.

Alasannya bisa kamu tulis begini:

> **Masukan:** "Sudah dapat hasil angka-angka, tapi bingung habis itu harus apa?"
>
> **Yang saya perbaiki:** menambahkan blok "Langkah selanjutnya" berisi tiga langkah tepat di bawah hasil perhitungan, dan menyisakan hanya satu tombol utama di layar itu.
>
> **Kenapa ini yang dipilih:** pengguna berhenti tepat di titik paling menentukan — sudah melihat angkanya dan sudah tertarik. Kebingungan di titik itu jauh lebih mahal daripada kebingungan di awal, karena semua usaha menariknya sampai ke situ jadi sia-sia.

Ambil tangkapan layar sebelum dan sesudahnya.

Dua perbaikan lainnya tetap bisa kamu sebut sebagai "perbaikan tambahan yang dikerjakan bersamaan", supaya tidak terlihat diabaikan.
