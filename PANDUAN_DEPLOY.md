# 🚀 Panduan Deploy Humas MMS Tracker

## Yang Kamu Butuhkan
- Akun **Google** (untuk Firebase)
- Akun **GitHub** (untuk Netlify)
- File `index.html` (sudah ada di folder ini)

---

## LANGKAH 1 — Upload ke GitHub (5 menit)

1. Buka **https://github.com/new**
2. Nama repository: `humas-mms-tracker`
3. Set ke **Public** → klik **Create repository**
4. Di halaman repository baru, klik **"uploading an existing file"**
5. Drag & drop seluruh isi folder ini:
   - `index.html`
   - `netlify.toml`
   - `_redirects`
6. Klik **Commit changes**

---

## LANGKAH 2 — Deploy ke Netlify (5 menit)

1. Buka **https://app.netlify.com**
2. Login dengan akun GitHub
3. Klik **"Add new site"** → **"Import an existing project"**
4. Pilih **GitHub** → pilih repo `humas-mms-tracker`
5. Build settings biarkan kosong semua
6. Klik **Deploy site**
7. Tunggu ~1 menit → Netlify akan memberikan link seperti:
   `https://random-name-123.netlify.app`
8. **Ganti nama domain:**
   - Buka **Site settings** → **Domain management**
   - Klik **Options** → **Edit site name**
   - Ganti jadi: `humas-mms` → link jadi `https://humas-mms.netlify.app`

✅ Website sudah bisa diakses semua orang dengan link tersebut!

---

## LANGKAH 3 — Sinkronisasi Data Tim via Firebase (15 menit)

> Langkah ini agar data tersimpan di cloud dan bisa diakses bareng seluruh tim
> (bukan hanya di browser masing-masing)

### 3A. Buat Project Firebase

1. Buka **https://console.firebase.google.com**
2. Klik **"Add project"** → nama: `humas-mms-tracker`
3. Matikan Google Analytics (opsional) → klik **Create project**

### 3B. Aktifkan Firestore Database

1. Di sidebar kiri → **Build** → **Firestore Database**
2. Klik **Create database**
3. Pilih **Start in test mode** → klik **Next**
4. Pilih lokasi: **asia-southeast2 (Jakarta)** → klik **Enable**

### 3C. Buat Web App

1. Di halaman utama project → klik icon **`</>`** (Web)
2. Nama app: `humas-tracker` → klik **Register app**
3. Firebase akan menampilkan konfigurasi seperti ini:

```javascript
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "humas-mms-tracker.firebaseapp.com",
  projectId: "humas-mms-tracker",
  storageBucket: "humas-mms-tracker.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

4. **Salin seluruh konfigurasi tersebut** → kirimkan ke saya
5. Saya akan update file `index.html` dengan konfigurasi Firebase-mu
6. Upload ulang file ke GitHub → Netlify otomatis update

### 3D. Atur Security Rules Firestore

Di Firestore → tab **Rules** → paste ini:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Klik **Publish**

---

## HASIL AKHIR

| Fitur | Status |
|-------|--------|
| Website online | ✅ Setelah Langkah 2 |
| Link permanen | ✅ `https://humas-mms.netlify.app` |
| Data tersimpan per browser | ✅ Sudah berjalan |
| Data sinkron antar tim | ✅ Setelah Langkah 3 + update konfigurasi |

---

## ⚡ Tips

- Setiap kali ada update file → upload ulang ke GitHub → Netlify otomatis deploy
- Login pertama: `admin@humas.id` / `admin123` → **segera ganti password**
- Hanya Admin yang bisa daftarkan akun anggota baru

