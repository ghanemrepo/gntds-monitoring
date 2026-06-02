# Registered Repos

Semua repo yang terhubung ke monitoring hub ini.
Tambah baris baru di tabel untuk mendaftarkan repo baru.

<!-- REPOS-START -->
| Repo | Type | Stack | Owner | Status |
|------|------|-------|-------|--------|
| hendradi1187/rapidsk-web-app | frontend | React + Vite + TypeScript | hendradi1187 | active |
| hendradi1187/dataspace | backend | Node.js + pnpm monorepo (14 services) | hendradi1187 | active |
<!-- REPOS-END -->

---

## Cara Daftar Repo Baru

1. Tambah baris di tabel di atas (antara marker `REPOS-START` dan `REPOS-END`)
2. Copy file `notify-monitor.yml` ke repo baru:
   ```
   .github/workflows/notify-monitor.yml
   ```
3. Tambah secret `MONITOR_PAT` di repo baru
4. Commit + push → langsung terpantau
