# Catatan Perubahan Hari 1

## Perubahan

- Menambahkan logika prize gacha ke `index.html`.
- Menambahkan data hadiah untuk rarity `SSR`, `Epic`, `Rare`, dan `Common`.
- Menambahkan sistem peluang:
  - SSR: 3% atau pasti saat pity mencapai 10 tarikan.
  - Epic: sampai ambang 10%.
  - Rare: sampai ambang 30%.
  - Common: hasil default.
- Menambahkan penghitung total tarikan, jumlah SSR, progress pity, animasi kartu, dan riwayat 12 tarikan terakhir.
- Menambahkan daftar hadiah di bawah riwayat agar semua prize yang mungkin didapat terlihat.

## Catatan Testing

- Runtime smoke test lewat Node berhasil.
- Yang dicek:
  - Daftar hadiah berisi 12 item.
  - Tombol `TARIK 1x` menambah total menjadi 1.
  - Tombol `TARIK 10x` menambah total menjadi 11.
  - Riwayat tarikan terisi 11 chip.
  - Nilai pity tetap dalam rentang 0 sampai 9 setelah tarikan.

## Perubahan Lanjutan - One Piece Character Gacha

- Mengubah tema dari prize gacha ETHJKT menjadi One Piece character gacha.
- Mengambil character pool dari `https://www.onepieceapi.com/api/characters` setelah endpoint awal redirect dari `https://onepieceapi.com/api/characters`.
- Menambahkan fallback karakter lokal jika API gagal dimuat.
- Mengubah kartu hasil gacha agar menampilkan:
  - Nama karakter.
  - Rarity berdasarkan bounty.
  - Bounty, status, tinggi badan, dan blood type.
  - Initial avatar jika API tidak menyediakan gambar.
- Mengubah rarity menjadi:
  - `Legend` untuk bounty minimal 1.000.000.000.
  - `Yonko Tier` untuk bounty minimal 500.000.000.
  - `Supernova` untuk bounty minimal 100.000.000.
  - `Crewmate` untuk karakter tanpa bounty besar.
- Mempertahankan sistem pity 10 tarikan untuk hasil `Legend`.
- Memodernisasi UI menjadi layout dashboard dua kolom dengan glass panel, kartu karakter besar, stats, history, dan daftar character pool.

## Catatan Testing Lanjutan

- API berhasil dicek lewat `curl.exe -L https://onepieceapi.com/api/characters`.
- Response API berupa array character dengan field seperti `name.en`, `status`, `height`, `blood_type`, `image_url`, dan `bounties`.
- Header API tidak menampilkan `Access-Control-Allow-Origin`, jadi browser bisa saja memblokir direct fetch karena CORS. Karena itu halaman tetap punya fallback lokal agar gacha tidak kosong.
- Runtime smoke test lewat Node dengan mocked API berhasil.
- Yang dicek:
  - Character pool dari API mock berisi 4 item.
  - Tombol aktif setelah data selesai dimuat.
  - Tombol `Tarik 1x` menambah total menjadi 1.
  - Tombol `Tarik 10x` menambah total menjadi 11.
  - Riwayat dibatasi maksimal 8 item.
  - Nilai pity tetap dalam rentang 0 sampai 9.
  - Kartu hasil selalu menampilkan nama karakter.
