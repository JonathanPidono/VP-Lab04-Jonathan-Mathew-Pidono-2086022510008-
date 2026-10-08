# Lab 04

1. Bagian aturan mana yang dilanggar, dan oleh widget apa?
Bagian "constraints go down", dan pelakunya adalah Row (parent). Row memberi anak yang tidak fleksibel (Text) lebar yang tidak terbatas pada sumbu utamanya, padahal ruang yang tersisa terbatas. Text lalu memilih ukurannya sendiri ("sizes go up") sepanjang isinya, dan hasilnya lebih besar dari ruang yang ada. Tidak ada yang menyuruh teks itu mengalah. Expanded atau Flexible memperbaikinya karena membuat Row mengirim batas lebar yang nyata ke Text.

2. Kenapa width: 150 salah, walau stripe hilang?
Karena itu memperbaiki angkanya, bukan hubungannya. Angka 150 hanya cocok untuk satu lebar layar dan satu panjang teks. Di layar yang lebih sempit, atau saat pengguna memperbesar ukuran font, overflow kembali. Di layar yang lebih lebar, ruang terbuang. Bug-nya pindah ke ukuran layar lain, bukan hilang.

3. Test mana yang gagal, dan kenapa penting kalau datanya dari API?
Test 7 (500 items) gagal, karena shrinkWrap: true memaksa list menghitung tinggi seluruh item, sehingga semuanya dibangun sekaligus (jumlah MenuTile melebihi 100). Kalau datanya dari API dan jumlahnya tidak kamu kontrol, layar jadi lambat dibuka, boros memori, dan gulungan tersendat.

4. Kenapa LayoutBuilder, bukan MediaQuery.sizeOf(context)?
MediaQuery hanya tahu ukuran seluruh layar. LayoutBuilder membaca constraint yang diberikan parent ke widget ini ("constraints go down"). Kalau layar yang sama ditaruh di panel samping, split view, atau dialog, layar fisik bisa lebar sedangkan widget-nya sempit. Keputusan layout harus berdasarkan ruang yang dimiliki widget, bukan ruang yang dimiliki perangkat.

5. Kenapa crash data kosong termasuk lab layout?
Karena layout yang tangguh harus selamat dari bentuk data apa pun, bukan hanya dari satu ukuran layar. Nol item adalah ujung ekstrem dari "jumlah item", sama seperti 500 item dan nama 200 karakter. promos[0] asumsi data selalu ada, sama seperti width: 200 berasumsi layar selalu lebar. Empty state juga sebuah keadaan layout yang harus dirancang (ikon, pesan, aksi), bukan layar kosong.