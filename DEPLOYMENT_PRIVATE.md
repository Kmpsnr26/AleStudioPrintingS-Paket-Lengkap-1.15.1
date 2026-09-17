# Deployment private repo — AleStudioPrintingS

Repository tetap **private**. GitHub Actions hanya mengirim folder `projects/` ke hosting melalui SSH/SFTP.

## GitHub Actions secrets yang harus diisi

Buka repository → **Settings → Secrets and variables → Actions → New repository secret**.

Tambahkan:

- `DEPLOY_HOST` — hostname/IP SSH hosting.
- `DEPLOY_USER` — username SSH/SFTP hosting.
- `DEPLOY_SSH_KEY` — private key SSH khusus deployment. Jangan commit key ke repository.
- `DEPLOY_PROJECTS_PATH` — folder tujuan di server yang memetakan ke `https://aleprinting.my.id/projects/`, contoh umum `/home/USERNAME/public_html/projects`.
- `DEPLOY_PORT` — opsional; jika kosong workflow memakai port `22`.

## Cara kerja

Setiap push ke branch `main` yang mengubah isi `projects/**` akan menjalankan workflow deployment.

Contoh:

- Repository: `projects/alestoreCollection/index.html`
- Hosting: `<DEPLOY_PROJECTS_PATH>/alestoreCollection/index.html`
- URL publik: `https://aleprinting.my.id/projects/alestoreCollection/`

Workflow tidak melakukan `--delete` untuk mengurangi risiko menghapus file server jika path salah. Homepage root `index.html` tidak ikut dikirim oleh workflow ini.

## Keamanan

Gunakan SSH key khusus deployment dengan hak akses hanya ke folder website bila hosting mendukungnya. Jangan menyimpan password, API key, token, atau private key di file repository.
