---
layout: page
title: Regenerate HMAC Credential
permalink: /managing-applications/regenerate-hmac-credential
nav_order: 1
parent: Managing Applications
---

# Panduan Membuat Ulang Kredensial HMAC di Mekari Developer

**Bahasa:** [Bahasa Indonesia](#bahasa-indonesia) · [English](#english)

---

## Bahasa Indonesia

### Untuk siapa panduan ini?

Panduan ini untuk **Company Owner** atau **Company Developer** yang mengelola integrasi API Mekari
menggunakan **HMAC Auth** (Client ID dan Client Secret).

### Apa yang terjadi?

Semua HMAC application yang ada sebelumnya sudah **dinonaktifkan**. Request API yang memakai
kredensial lama akan ditolak dengan respons berikut:

```http
HTTP/1.1 401 Unauthorized

{"code":"MAG-003","message":"mag: unauthorized"}
```

Di halaman Applications, aplikasi lama **tetap terlihat seperti biasa** dan tidak ada label
"inactive". Jika integrasi Anda menerima error di atas, ikuti langkah di bawah untuk membuat
kredensial baru.

> **Penting:** tombol **Regenerate Client Secret** pada aplikasi lama **tidak** memulihkan akses.
> Aplikasi lama tetap nonaktif walaupun secret-nya diganti. Anda harus **membuat aplikasi baru**.

### Ringkasan langkah

1. Catat scope dari aplikasi lama.
2. Buat aplikasi HMAC baru dengan scope yang sama.
3. Simpan Client ID dan Client Secret yang baru.
4. Perbarui integrasi Anda dan pastikan berjalan normal.
5. Hapus aplikasi lama.

### Langkah 1: Catat scope dari aplikasi lama

1. Login ke **https://developers.mekari.com**.
2. Buka menu **Applications**.
3. Pada aplikasi lama, klik **Detail**.

![Halaman Applications](/docs/kb/assets/images/regenerate-hmac-1.png)

4. Di tab **Detail**, klik **Show scopes** pada bagian **Authorized scopes**.
5. Catat **semua** scope yang tampil. Anda akan memilih scope yang sama di aplikasi baru.

![Daftar scope aplikasi lama](/docs/kb/assets/images/regenerate-hmac-2.png)

> Jangan klik **Regenerate Client Secret** di tab **Credentials** aplikasi lama. Langkah ini tidak
> mengaktifkan kembali aplikasi lama.
>
> ![Jangan gunakan Regenerate Client Secret pada aplikasi lama](/docs/kb/assets/images/regenerate-hmac-3.png)

### Langkah 2: Buat aplikasi HMAC baru

1. Kembali ke menu **Applications**, lalu klik **Create Application**.
2. Isi **Application Name**, lalu pilih **Company** yang sama dengan aplikasi lama.

![Form HMAC Auth Application](/docs/kb/assets/images/regenerate-hmac-4.png)

3. Setelah company dipilih, daftar **Authorized Scopes** akan muncul. Ketik nama scope di kolom
   pencarian.

![Mencari scope](/docs/kb/assets/images/regenerate-hmac-5.png)

4. Centang setiap scope yang Anda catat di Langkah 1. Scope yang dipilih akan muncul di panel
   **Selected**. Pastikan jumlah dan namanya sama dengan aplikasi lama.
5. Klik **Submit**.

![Scope yang dipilih dan tombol Submit](/docs/kb/assets/images/regenerate-hmac-6.png)

### Langkah 3: Simpan Client ID dan Client Secret yang baru

Setelah submit, **Client ID** dan **Client Secret** baru akan ditampilkan.

![Client ID dan Client Secret baru](/docs/kb/assets/images/regenerate-hmac-7.png)

> **Client Secret hanya ditampilkan sekali.** Salin dan simpan di tempat yang aman (misalnya secret
> manager) sebelum meninggalkan halaman ini. Jangan bagikan secret lewat email atau chat.

Jika secret aplikasi **baru** hilang, Anda bisa memakai **Regenerate Client Secret** di aplikasi baru
tersebut.

### Langkah 4: Perbarui integrasi Anda

1. Ganti Client ID dan Client Secret lama di sistem Anda dengan yang baru. **Client ID juga
   berubah**, bukan hanya secret-nya.
2. Kirim request percobaan dan pastikan sudah tidak ada error `401` dengan kode `MAG-003`.

### Langkah 5: Hapus aplikasi lama

Setelah integrasi berjalan normal dengan kredensial baru:

1. Buka menu **Applications**, lalu klik **Detail** pada aplikasi **lama**. Cek Client ID dan
   Creation Date untuk memastikan Anda tidak membuka aplikasi yang baru.
2. Buka tab **Advanced**, lalu klik **Delete application**.

![Hapus aplikasi lama](/docs/kb/assets/images/regenerate-hmac-8.png)

> Aplikasi **langsung terhapus** saat tombol diklik, tanpa konfirmasi tambahan, dan **tidak bisa
> dibatalkan**.

3. Pesan sukses akan muncul dan aplikasi lama hilang dari daftar.

![Aplikasi berhasil dihapus](/docs/kb/assets/images/regenerate-hmac-9.png)

### Pertanyaan umum

**Saya tidak bisa membuat aplikasi atau company saya tidak muncul.**
Hanya pengguna dengan peran Company Owner atau Company Developer di company tersebut yang bisa
membuat aplikasi. Minta Company Owner Anda untuk memberikan akses.

**Scope yang dulu saya pakai tidak ada di daftar.**
Daftar scope mengikuti produk Mekari yang terhubung dengan company Anda. Jika scope tersebut tidak
muncul, hubungi tim support Mekari.

**Saya punya beberapa aplikasi HMAC lama.**
Ulangi Langkah 1 sampai 5 untuk setiap aplikasi.

**Bolehkah saya memilih semua scope agar lebih mudah?**
Tidak disarankan. Pilih hanya scope yang dibutuhkan integrasi Anda, sama seperti aplikasi lama.

---

## English

### Who is this guide for?

This guide is for a **Company Owner** or **Company Developer** who manages a Mekari API
integration that uses **HMAC Auth** (Client ID and Client Secret).

### What happened?

All existing HMAC applications have been **deactivated**. API requests that use an old credential
are rejected with this response:

```http
HTTP/1.1 401 Unauthorized

{"code":"MAG-003","message":"mag: unauthorized"}
```

Old applications **still look normal** on the Applications page, with no "inactive" label. If your
integration receives the error above, follow the steps below to create a new credential.

> **Important:** **Regenerate Client Secret** on an old application does **not** restore access.
> The old application stays inactive even with a new secret. You must **create a new application**.

### Steps at a glance

1. Note the scopes of the old application.
2. Create a new HMAC application with the same scopes.
3. Save the new Client ID and Client Secret.
4. Update your integration and confirm it works.
5. Delete the old application.

### Step 1: Note the scopes of the old application

1. Log in to **https://developers.mekari.com**.
2. Open **Applications**.
3. On the old application, click **Detail**.

![Applications page](/docs/kb/assets/images/regenerate-hmac-1.png)

4. On the **Detail** tab, click **Show scopes** under **Authorized scopes**.
5. Write down **every** scope listed. You'll select the same scopes on the new application.

![Old application scopes](/docs/kb/assets/images/regenerate-hmac-2.png)

> Don't click **Regenerate Client Secret** on the old application's **Credentials** tab. It won't
> reactivate the old application.
>
> ![Don't use Regenerate Client Secret on the old application](/docs/kb/assets/images/regenerate-hmac-3.png)

### Step 2: Create a new HMAC application

1. Go back to **Applications** and click **Create Application**.
2. Enter an **Application Name** and choose the same **Company** as the old application.

![HMAC Auth Application form](/docs/kb/assets/images/regenerate-hmac-4.png)

3. Once the company is selected, the **Authorized Scopes** list appears. Type a scope name in the
   search box.

![Searching for a scope](/docs/kb/assets/images/regenerate-hmac-5.png)

4. Tick every scope you noted in Step 1. Selected scopes appear in the **Selected** panel. Check
   that the names and count match the old application.
5. Click **Submit**.

![Selected scopes and the Submit button](/docs/kb/assets/images/regenerate-hmac-6.png)

### Step 3: Save the new Client ID and Client Secret

After you submit, the new **Client ID** and **Client Secret** are shown.

![New Client ID and Client Secret](/docs/kb/assets/images/regenerate-hmac-7.png)

> **The Client Secret is shown only once.** Copy it and store it somewhere safe (for example a
> secret manager) before leaving the page. Don't share the secret over email or chat.

If you lose the secret of the **new** application, you can use **Regenerate Client Secret** on that
new application.

### Step 4: Update your integration

1. Replace the old Client ID and Client Secret in your system with the new ones. **The Client ID
   changes too**, not just the secret.
2. Send a test request and confirm you no longer get a `401` with code `MAG-003`.

### Step 5: Delete the old application

Once your integration works with the new credential:

1. Open **Applications** and click **Detail** on the **old** application. Check the Client ID and
   Creation Date so you don't open the new one by mistake.
2. Open the **Advanced** tab and click **Delete application**.

![Delete the old application](/docs/kb/assets/images/regenerate-hmac-8.png)

> The application is **deleted as soon as you click**, with no extra confirmation, and this
> **can't be undone**.

3. A success message appears and the old application disappears from the list.

![Application deleted](/docs/kb/assets/images/regenerate-hmac-9.png)

### FAQ

**I can't create an application, or my company isn't in the list.**
Only users with the Company Owner or Company Developer role in that company can create
applications. Ask your Company Owner for access.

**A scope I used before isn't in the list.**
The scope list follows the Mekari products connected to your company. If a scope is missing,
contact Mekari support.

**I have several old HMAC applications.**
Repeat Steps 1 to 5 for each one.

**Can I just select all scopes to make it easier?**
Not recommended. Select only the scopes your integration needs, the same as the old application.
