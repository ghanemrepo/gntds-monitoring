# gntds-monitoring

Central monitoring hub untuk semua repo di project Dataspace (GNT).

Repo ini tidak berisi application code — hanya **activity log**, **changelog aggregate**, dan **PM tools**.

---

## Cara Kerja

Setiap repo yang terdaftar punya workflow `notify-monitor.yml`. Setiap kali ada:
- **Push ke branch** → tercatat di `logs/ACTIVITY_LOG.md`
- **PR dibuka / merged** → tercatat di `logs/ACTIVITY_LOG.md`
- **Release diterbitkan** → tercatat di `changelogs/CHANGELOG.md`
- **Setiap Senin 09:00 WIB** → Weekly digest dibuat sebagai GitHub Issue

```
Dev push / PR / Release
        ↓
   notify-monitor.yml (di tiap source repo)
        ↓  repository_dispatch
   gntds-monitoring workflows
        ↓
   logs/ACTIVITY_LOG.md  ←── semua aktivitas
   changelogs/CHANGELOG.md ←── hanya releases
   GitHub Issues ←── weekly digest & backlog
```

---

## Isi Repo

| Path | Isi |
|------|-----|
| `logs/ACTIVITY_LOG.md` | Live feed semua push & PR dari semua repo |
| `changelogs/CHANGELOG.md` | Aggregate changelog, update otomatis per release |
| `docs/REPOS.md` | Registry semua repo yang terhubung |
| `.github/workflows/receive-activity.yml` | Listener push + PR events |
| `.github/workflows/receive-release.yml` | Listener release events |
| `.github/workflows/weekly-digest.yml` | Setiap Senin — buat GitHub Issue laporan mingguan |

---

## Menambah Repo Baru

1. Tambah baris di `docs/REPOS.md`
2. Copy `.github/workflows/notify-monitor.yml` ke repo baru
3. Tambah secret `MONITOR_PAT` di repo baru (Settings → Secrets → Actions)
4. Push — otomatis mulai terpantau

---

## Secrets yang Dibutuhkan

| Secret | Di mana | Untuk apa |
|--------|---------|-----------|
| `MONITOR_PAT` | Setiap source repo | PAT `ghanemrepo` dengan scope `repo` — untuk fire dispatch ke hub |

> Buat PAT: https://github.com/settings/tokens/new → scope: `repo` → simpan sebagai `MONITOR_PAT` di tiap source repo
