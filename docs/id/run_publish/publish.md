# Publikasikan Proyek SubQuery Anda

## Manfaat menghosting proyek Anda dengan SubQuery

- Kami akan menjalankan proyek SubQuery untuk Anda dalam layanan publik berkinerja tinggi, skalabel, dan terkelola.
- Layanan ini disediakan untuk komunitas secara gratis!
- Anda dapat menjadikan proyek Anda publik sehingga akan dicantumkan di [SubQuery Explorer](https://explorer.subquery.network) dan siapa saja di seluruh dunia dapat melihatnya.
- Kami terintegrasi dengan GitHub, jadi siapa pun di organisasi GitHub Anda dapat melihat proyek organisasi bersama.

## Buat proyek pertama Anda di Proyek SubQuery

### Hosting Basis Kode Proyek

Ada dua cara Anda dapat menghosting basis kode proyek SubQuery Anda sebelum dipublikasikan.


**IPFS (Suggested)**: Your project's codebase can be stored in IPFS, you can follow our IPFS hosting guide to see how to [first publish to IPFS](../run_publish/ipfs.md).

**GitHub**: Your project's codebase must be in a public GitHub repository, this process may be deprecated soon.

### Masuk ke Proyek SubQuery

Sebelum memulai, pastikan bahwa basis kode proyek SubQuery Anda online di repositori GitHub publik atau di IPFS. File `schema.graphql` harus berada di root direktori Anda.

Untuk membuat proyek pertama Anda, buka [Proyek SubQuery](https://project.subquery.network). Anda harus mengautentikasi dengan akun GitHub Anda untuk masuk.

Pada login pertama, Anda akan diminta untuk mengotorisasi SubQuery. Kami hanya memerlukan alamat email Anda untuk mengidentifikasi akun Anda, dan kami tidak menggunakan data lain dari akun GitHub Anda untuk alasan lain apa pun. Pada langkah ini, Anda juga dapat meminta atau memberikan akses ke akun Organisasi GitHub Anda sehingga Anda dapat memposting proyek SubQuery di bawah Organisasi GitHub alih-alih akun pribadi Anda.

![Cabut persetujuan dari akun GitHub](/assets/img/project_auth_request.png)

Proyek SubQuery adalah tempat Anda mengelola semua proyek yang dihosting yang diunggah ke platform SubQuery. Anda dapat membuat, menghapus, dan bahkan meningkatkan proyek semua dari aplikasi ini.

![Login Projek](/assets/img/projects-dashboard.png)

Jika Anda memiliki akun Organisasi GitHub yang terhubung, Anda dapat menggunakan pengalih di header untuk mengubah antara akun pribadi Anda dan akun Organisasi GitHub Anda. Proyek yang dibuat di akun Organisasi GitHub dibagikan di antara anggota di Organisasi GitHub tersebut. Untuk menghubungkan akun Organisasi GitHub Anda, Anda dapat [mengikuti langkah-langkah di sini](publish.md#add-github-organization-account-to-subquery-projects).

![Beralih antar akun GitHub](/assets/img/projects-account-switcher.png)

### Buat Proyek Pertama Anda

Ada dua metode untuk membuat proyek di SubQuery Managed Service, Anda dapat menggunakan UI atau langsung melalui alat `subql` cli.

#### Menggunakan UI

Mari kita mulai dengan mengklik "Create Project". Anda akan dibawa ke formulir Proyek Baru. Silakan masukkan yang berikut ini (Anda bisa mengubahnya di masa mendatang):

- **Akun GitHub:** Jika Anda memiliki lebih dari satu akun GitHub, pilih akun mana yang akan dibuat proyek ini. Proyek yang dibuat di akun organisasi GitHub dibagikan di antara anggota di organisasi itu.
- **Nama Projek**
- **Subtitle**
- **Deskripsi**
- **URL Repositori GitHub:** Ini harus berupa URL GitHub yang valid untuk repositori publik yang memiliki proyek SubQuery Anda. File `schema.graphql` harus berada di root direktori Anda ([pelajari lebih lanjut tentang struktur direktori](../build/introduction.md#directory-structure)).
- **Database:** Pelanggan premium dapat mengakses database khusus untuk menghosting proyek SubQuery produksi. Jika ini menarik minat Anda, Anda dapat menghubungi [sales@subquery.network](mailto:sales@subquery.network) untuk mengaktifkan setelan ini.
- **Sumber Penerapan:** Anda dapat memilih agar proyek di-deploy dari repositori GitHub atau sebagai alternatif di-deploy dari IPFS CID, lihat panduan kami tentang [hosting dengan IPFS.](ipfs.md)
- **Sembunyikan proyek:** Jika dipilih, ini akan menyembunyikan proyek dari penjelajah SubQuery publik. Biarkan ini tidak dipilih jika Anda ingin membagikan SubQuery Anda dengan komunitas!

![Buat Proyek pertama Anda](/assets/img/projects-create.png)

Buat proyek Anda dan Anda akan melihatnya di daftar Proyek SubQuery Anda. _Kita hampir sampai! Kita hanya perlu menerapkan versi barunya._

![Membuat Proyek tanpa penerapan](/assets/img/projects-no-deployment.png)

#### Menggunakan CLI

Anda juga dapat menggunakan `@subql/cli` untuk mempublikasikan proyek Anda ke layanan terkelola kami. Hal ini membutuhkan:

- `@subql/cli` versi 1.1.0 atau lebih tinggi.
- Sebuah [SUBQL_ACCESS_TOKEN](../run_publish/ipfs.md#prepare-your-subql-access-token) yang valid sudah siap.

```shell
// Creating a project using the CLI
$ subql project:create-project

// OR using non-interactive, it will prompt you if the required fields are missing
$ subql project:create-project
    --apiVersion=apiVersion      Api version is default to 2
    --description=description    Enter description
    --gitRepo=gitRepo            Enter git repository
    --org=org                    Enter organization name
    --projectName=projectName  Enter project name
```

### Terapkan Versi pertama Anda

Ada dua metode untuk menyebarkan versi baru proyek Anda ke SubQuery Managed Service, Anda dapat menggunakan UI atau secara langsung melalui alat `subql` cli.

#### Menggunakan UI

Saat membuat proyek akan mengatur perilaku tampilan proyek, Anda harus menerapkan sebuah versi sebelum menjadi operasional. Menerapkan versi memicu operasi pengindeksan SubQuery baru untuk memulai, dan menyiapkan layanan kueri yang diperlukan untuk mulai menerima permintaan GraphQL. Anda juga dapat menerapkan versi-versi baru ke proyek yang ada di sini.

Dengan proyek baru Anda, Anda akan melihat tombol Deploy New Version. Klik ini, dan isi informasi yang diperlukan tentang penerapan:

- **Cabang:** Dari GitHub, pilih cabang proyek yang ingin Anda gunakan.
- **Commit Hash:** Dari GitHub, pilih komit spesifik dari versi basis kode proyek SubQuery yang ingin Anda terapkan.
- **IPFS:** Jika menerapkan dari IPFS, tempel CID penerapan IPFS Anda (tanpa awalan `ipfs://`).
- **Ganti Titik Akhir Jaringan dan Kamus:** Anda dapat mengganti titik akhir dalam manifes proyek Anda di sini.
- **Versi Pengindeks:** Ini adalah versi layanan simpul SubQuery yang Anda inginkan untuk menjalankan SubQuery ini. Lihat [`@subql/node`](https://www.npmjs.com/package/@subql/node).
- **Versi Kueri:** Ini adalah versi layanan kueri SubQuery yang Anda inginkan untuk menjalankan SubQuery ini. Lihat [`@subql/query`](https://www.npmjs.com/package/@subql/query).

![Terapkan Proyek pertama Anda](https://static.subquery.network/media/projects/projects-first-deployment.png)

Jika berhasil diterapkan, Anda akan melihat pengindeks mulai bekerja dan melaporkan kembali kemajuan pengindeksan chain saat ini. Proses ini mungkin memakan waktu hingga mencapai 100%.

#### Menggunakan CLI

Anda juga dapat menggunakan `@subql/cli` untuk membuat deployment baru dari proyek Anda ke layanan terkelola kami. Hal ini membutuhkan:

- `@subql/cli` versi 1.1.0 atau lebih tinggi.
- Sebuah [SUBQL_ACCESS_TOKEN](../run_publish/ipfs.md#prepare-your-subql-access-token) yang valid sudah siap.

```shell
// Deploy using the CLI
$ subql deployment:deploy

// OR Deploy using non-interactive CLI
$ subql deployment:deploy

  -d, --useDefaults                Use default values for indexerVerion, queryVersion, dictionary, endpoint
  --dict=dict                      Enter dictionary
  --endpoint=endpoint              Enter endpoint
  --indexerVersion=indexerVersion  Enter indexer-version
  --ipfsCID=ipfsCID                Enter IPFS CID
  --org=org                        Enter organization name
  --projectName=projectName        Enter project name
  --queryVersion=queryVersion      Enter query-version
  --type=(stage|primary)           [default: primary]
```

## Langkah Selanjutnya - Hubungkan ke Proyek Anda

Setelah penerapan Anda berhasil diselesaikan dan node kami telah mengindeks data Anda dari chain, Anda akan dapat terhubung ke proyek Anda melalui titik akhir Kueri GraphQL yang ditampilkan.

![Proyek sedang diterapkan dan disinkronkan](/assets/img/projects-deploy-sync.png)

Atau, Anda dapat mengklik tiga titik di samping judul proyek Anda, dan melihatnya di SubQuery Explorer. Di sana Anda dapat menggunakan taman bermain dalam browser untuk memulai - [baca selengkapnya tentang cara menggunakan Explorer kami di sini](../run_publish/query.md).

![Proyek di SubQuery Explorer](/assets/img/projects-explorer.png)

## Tambahkan Akun Organisasi GitHub ke Proyek SubQuery

Umum untuk mempublikasikan proyek SubQuery Anda dengan nama akun Organisasi GitHub Anda daripada akun GitHub pribadi Anda. Kapan pun Anda dapat mengubah akun yang dipilih saat ini di [Proyek SubQuery](https://project.subquery.network) menggunakan pengalih akun.

![Beralih antar akun GitHub](/assets/img/projects-account-switcher.png)

Jika Anda tidak dapat melihat akun Organisasi GitHub Anda tercantum di pengalih, Anda mungkin perlu memberikan akses ke SubQuery untuk Organisasi GitHub Anda (atau memintanya dari administrator). Untuk melakukan ini, Anda harus terlebih dahulu mencabut izin dari akun GitHub Anda ke Aplikasi SubQuery. Untuk melakukannya, masuk ke pengaturan akun Anda di GitHub, buka Aplikasi, dan di bawah tab Aplikasi OAuth Resmi, cabut SubQuery - [Anda dapat mengikuti langkah-langkah yang tepat di sini](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/reviewing-your-authorized-applications-oauth). **Jangan khawatir, ini tidak akan menghapus proyek SubQuery Anda dan Anda tidak akan kehilangan data apa pun.**

![Cabut akses ke akun GitHub](/assets/img/project_auth_revoke.png)

Setelah Anda mencabut akses, keluar dari [Proyek SubQuery](https://project.subquery.network) dan masuk kembali. Anda harus diarahkan ke halaman berjudul _Otorisasi SubQuery_ di mana Anda dapat meminta atau memberikan akses SubQuery ke akun Organisasi GitHub Anda. Jika Anda tidak memiliki izin admin, Anda harus membuat permintaan kepada administrator untuk mengaktifkannya untuk Anda.

![Cabut persetujuan dari akun GitHub](/assets/img/project_auth_request.png)

Setelah permintaan ini disetujui oleh administrator Anda (atau jika dapat mengabulkannya sendiri), Anda akan melihat akun Organisasi GitHub yang benar di pengalih akun.
