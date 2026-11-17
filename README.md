# cline-terminal

<p align="center">
  <a href="https://code.visualstudio.com/" title="Visual Studio Code">
    <img src="https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" alt="Visual Studio Code">
  </a>
  <a href="https://www.linux.org/" title="Linux">
    <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux">
  </a>
  <a href="https://www.microsoft.com/" title="Microsoft">
    <img src="https://img.shields.io/badge/Microsoft-5E5E5E?style=for-the-badge&logo=microsoft&logoColor=white" alt="Microsoft">
  </a>
</p>

Repositori ini mengandungi sumber **Code - OSS** (Visual Studio Code open source) di bawah folder [`vscode/`](vscode). Projek ini digunakan sebagai workspace untuk membangunkan, mengubah, dan membina Code - OSS daripada kod sumber.

> **Nota:** Folder `vscode/` ialah sumber upstream Code - OSS. Keselamatan, pengendalian data, integrasi Copilot, dan komponen lain harus dinilai sebelum digunakan dalam pengeluaran.

## Kandungan

- [Keperluan](#keperluan)
- [Persediaan menggunakan Dev Container](#persediaan-menggunakan-dev-container)
- [Persediaan setempat](#persediaan-setempat)
- [Jalankan Code - OSS](#jalankan-code---oss)
- [Arahan pembangunan](#arahan-pembangunan)
- [Struktur projek](#struktur-projek)
- [Ujian](#ujian)
- [Lesen](#lesen)

## Keperluan

Untuk build penuh, disyorkan sekurang-kurangnya:

- 4 CPU core
- 8 GB RAM
- 9 GB RAM untuk Dev Container
- Node.js 24.22.1, seperti yang ditetapkan oleh [`vscode/.nvmrc`](vscode/.nvmrc)
- pnpm 12.16.0, seperti yang ditetapkan dalam [`vscode/package.json`](vscode/package.json)
- Git
- Docker Desktop atau Docker Engine dengan sokongan Dev Container jika menggunakan container

## Persediaan menggunakan Dev Container

1. Pasang VS Code dan sambungan **Dev Containers**.
2. Buka folder repositori root ini dalam VS Code.
3. Jalankan arahan `Dev Containers: Reopen in Container`.
4. Konfigurasi container secara automatik:
   - memasang pnpm,
   - menjalankan `pnpm install`,
   - dan memuat turun Electron melalui skrip post-create.

Konfigurasi berada di [`vscode/.devcontainer/devcontainer.json`](vscode/.devcontainer/devcontainer.json). Portal noVNC tersedia pada port `6080`, manakala VNC tersedia pada port `5901`.

Setelah container siap:

```bash
cd vscode
./scripts/code.sh
```

Maklumat lanjut tersedia di [`vscode/.devcontainer/README.md`](vscode/.devcontainer/README.md).

## Persediaan setempat

Gunakan Node.js 24.22.1 dan masuk ke folder sumber:

```bash
cd vscode
nvm use
npm install --global pnpm@12.16.0
pnpm install
pnpm run electron
```

`pnpm install` juga akan menghormati versi pnpm yang ditetapkan dalam `package.json`.

## Jalankan Code - OSS

Daripada folder `vscode/`:

```bash
./scripts/code.sh
```

Untuk memulakan Electron dan memuatkan perubahan sumber anda, skrip itu menjalankan langkah prapelancaran dan membuka aplikasi Code - OSS secara pembangunan.

Untuk pembangunan berterusan, jalankan watch:

```bash
cd vscode
pnpm run watch
```

## Arahan pembangunan

Semua arahan berikut dijalankan daripada folder `vscode/`.

| Arahan | Tujuan |
| --- | --- |
| `pnpm install` | Pasang semua workspace dan dependencies |
| `pnpm run compile` | Compile client dan extension Copilot |
| `pnpm run compile-client` | Compile Code - OSS client |
| `pnpm run compile-copilot` | Compile extension Copilot |
| `pnpm run watch` | Jalankan watch untuk client, extensions, dan Copilot |
| `pnpm run watch-transpile` | Jalankan watch transpilation tanpa watch penuh |
| `pnpm run electron` | Muat turun atau sediakan Electron |
| `pnpm run typecheck-client` | Semak TypeScript client tanpa emit |
| `pnpm run hygiene` | Jalankan pemeriksaan hygiene/lint projek |
| `pnpm run core-ci` | Jalankan set pemeriksaan CI teras |

Untuk senarai script penuh, rujuk [`vscode/package.json`](vscode/package.json).

## Struktur projek

```text
cline-terminal/
├── README.md
└── vscode/
    ├── src/                 # Kemasukan dan implementasi teras VS Code
    ├── extensions/          # Built-in extensions
    ├── build/               # Sistem build, tooling, dan tugas Gulp
    ├── scripts/             # Skrip build, launch, smoke test, dan utiliti
    ├── test/                # Unit, integration, browser, automation, dan smoke tests
    ├── remote/              # Komponen remote/server
    ├── cli/                 # Kod CLI
    ├── .devcontainer/       # Konfigurasi Dev Container dan Codespaces
    ├── package.json         # Script dan dependencies utama
    └── pnpm-workspace.yaml  # Senarai package dalam monorepo
```

## Ujian

Daripada folder `vscode/`, beberapa kategori ujian boleh dijalankan dengan:

```bash
# Unit test Node.js
pnpm run test-node

# Unit test browser
pnpm run test-browser-no-install

# Smoke test
pnpm run smoketest

# Pemeriksaan build scripts
pnpm run test-build-scripts

# Semakan TypeScript client
pnpm run typecheck-client
```

Gunakan fokus test yang paling kecil untuk perubahan anda sebelum menjalankan suite penuh. Skrip test juga memerlukan build atau prasyarat tertentu; rujuk output skrip jika dependency atau output compile belum tersedia.

## Lesen

Kod dalam folder `vscode/` merupakan Code - OSS yang dilindungi di bawah [lesen MIT](vscode/LICENSE.txt).