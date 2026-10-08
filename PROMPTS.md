# Jurnal Prompt

Catat prompt penting selama membangun aplikasi: apa yang kamu minta, hasilnya, dan perbaikan yang dilakukan. Beri tanda **[SENDIRI]** untuk prompt yang kamu tulis sendiri (bukan dari lembar kerja).

## US-01 Katalog dari database

**Prompt: Baca AGENTS.md dan docs/user-stories.md bagian US-01.

Ubah app/page.jsx supaya daftar produk diambil dari tabel "produk" di Supabase, di sisi server, memakai SUPABASE_URL dan SUPABASE_SECRET_KEY dari environment variable. Buat koneksi Supabase untuk server di folder lib/supabase.

Tampilkan produk dengan komponen KartuProduk yang sudah ada, tanpa mengubah tampilannya. Kalau gagal mengambil data, tampilkan pesan error yang jelas di halaman. Kalau tabel kosong, tampilkan tulisan "Belum ada produk". Hapus CatatanBelumAktif dari halaman ini.**

**Hasil: File yang Ditambahkan & Diubah

lib/supabase/server.js & lib/supabase/index.js (Baru)

Membuat inisialisasi client Supabase di sisi server menggunakan SUPABASE_URL dan SUPABASE_SECRET_KEY dari environment variable.

app/page.jsx (Diubah)

Mengambil data produk langsung dari tabel produk di Supabase pada Server Component.
Menghapus penggunaan data contoh (produkContoh) dan komponen CatatanBelumAktif.
Menampilkan kartu produk dengan komponen KartuProduk.
Menampilkan pesan "Belum ada produk" jika tabel tidak memiliki data.
Menampilkan pesan error yang informatif jika proses pengambilan data gagal.**

**Perbaikan:**

## US-02 Detail produk

**Prompt:Baca docs/user-stories.md bagian US-02.

Ubah app/produk/[id]/page.jsx supaya mengambil satu produk dari tabel "produk" di Supabase berdasarkan id di URL, di sisi server, memakai koneksi Supabase yang sudah dibuat di lib/supabase. Kalau produk tidak ditemukan, panggil notFound(). Jangan ubah tampilannya. Hapus CatatanBelumAktif dari halaman ini, tapi biarkan tombol WhatsApp.**

**Hasil: Fitur US-02: Detail produk telah selesai diimplementasikan.

File yang Diubah
app/produk/[id]/page.jsx
Mengambil data satu produk dari tabel produk di Supabase berdasarkan parameter dinamis id pada sisi server.
Menggunakan koneksi Supabase server dari lib/supabase/server.js.
Memanggil notFound() apabila produk dengan id tersebut tidak ditemukan atau terjadi kesalahan query.
Menghapus komponen CatatanBelumAktif dan fungsi pembacaan data contoh (cariProdukContoh), dengan tetap mempertahankan tombol TombolWhatsApp serta seluruh tampilan dan layout sebelumnya.**

**Perbaikan:**

## US-03 Pesan via WhatsApp

**Prompt: Baca docs/rancangan-teknis.md bagian "Pesan WhatsApp (US-03)".

Ubah components/TombolWhatsApp.jsx menjadi tautan yang membuka https://wa.me/ ke nomor di lib/toko.js, dengan pesan otomatis berisi nama dan harga produk dalam format rupiah. Pesan di-encode dengan encodeURIComponent dan dibuka di tab baru. Pertahankan tampilan tombolnya. Hapus CatatanBelumAktif yang menyebut US-03 di halaman detail produk.**

**Hasil:Fitur US-03: Pesan via WhatsApp telah selesai diimplementasikan.

File yang Diubah
components/TombolWhatsApp.jsx
Diubah dari elemen <button> menjadi tautan <a> dengan styling tampilan tombol yang sama persis (bg-utama, hover:bg-utama-gelap, dsb).
Tautan mengarah ke https://wa.me/<nomor>?text=<pesan> menggunakan nomor WhatsApp dari lib/toko.js.
Pesan otomatis dibuat dengan nama dan harga produk dalam format rupiah menggunakan fungsi formatRupiah dan di-encode menggunakan encodeURIComponent.
Dilengkapi atribut target="_blank" dan rel="noopener noreferrer" agar terbuka di tab baru.
app/produk/[id]/page.jsx
Komponen CatatanBelumAktif terkait US-03 telah dibersihkan dari halaman detail produk.**

**Perbaikan:**

## US-04 Login admin

**Prompt: Baca AGENTS.md bagian aturan keamanan dan docs/user-stories.md bagian US-04.

Buat login admin memakai Supabase Auth (email dan password) dengan @supabase/ssr dan cookie, memakai SUPABASE_URL dan SUPABASE_PUBLISHABLE_KEY. Login diproses dengan Server Action di app/admin/actions.js dan disambungkan ke form di app/admin/login/page.jsx. Login berhasil diarahkan ke /admin; login gagal menampilkan pesan error yang jelas di halaman login. Buat juga tombol "Keluar" di components/NavAdmin.jsx berfungsi: mengakhiri sesi lalu kembali ke /admin/login. Jangan ubah tampilan. Hapus CatatanBelumAktif dari halaman login.**

**Hasil: Fitur US-04: Login admin telah selesai diimplementasikan.

File yang Ditambahkan & Diubah
lib/supabase/session.js (Baru)
Membuat fungsi createSessionClient() menggunakan @supabase/ssr dan cookies() dari next/headers dengan SUPABASE_URL dan SUPABASE_PUBLISHABLE_KEY untuk mengelola sesi admin.
lib/supabase/index.js (Diubah)
Menambahkan re-export untuk session.js.
app/admin/actions.js (Baru)
Server Action login: memproses autentikasi email dan password via supabase.auth.signInWithPassword. Jika berhasil dialihkan ke /admin, jika gagal mengembalikan pesan error.
Server Action keluar: memanggil supabase.auth.signOut() untuk menghapus cookie sesi dan mengalihkan kembali ke /admin/login.
app/admin/login/page.jsx (Diubah)
Menggunakan useActionState untuk menghubungkan form login dengan Server Action login.
Menampilkan pesan error di bawah judul jika login gagal.
Menghapus komponen CatatanBelumAktif tanpa mengubah styling layout.
components/NavAdmin.jsx (Diubah)
Menghubungkan tombol "Keluar" ke Server Action keluar dengan form submission tanpa mengubah tampilan tombol.**

**Perbaikan:**

## US-05 Ganti password

**Prompt:Baca docs/user-stories.md bagian US-05.

Buat Server Action ganti password di app/admin/actions.js untuk admin yang sedang login, memakai Supabase Auth. Validasi di server: password baru minimal 8 karakter dan harus sama dengan konfirmasi. Tampilkan pesan berhasil atau pesan error yang jelas di halaman. Sambungkan ke form di app/admin/password/page.jsx tanpa mengubah tampilannya. Hapus CatatanBelumAktif dari halaman ini.**

**Hasil:**

**Perbaikan:**

## US-06 Proteksi halaman admin

**Prompt:Baca AGENTS.md aturan keamanan nomor 3 dan 4, dan docs/user-stories.md bagian US-06.

Buat file proxy.js di root proyek (Next.js 16). Semua rute /admin kecuali /admin/login wajib login dengan Supabase Auth; kalau belum login, alihkan ke /admin/login. Pastikan juga setiap Server Action yang mengubah data memeriksa login di server. Hapus CatatanBelumAktif dari halaman /admin.**

**Hasil:**

**Perbaikan:**

## Debugging dan fitur bonus

Tambahkan bagian baru untuk setiap error yang kamu perbaiki atau fitur bonus yang kamu kerjakan.
