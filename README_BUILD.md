# CyberRoad — Build Installer di Windows

## Persiapan
1. Install **Inno Setup 6.x**: https://jrsoftware.org/isdl.php
2. Copy seluruh folder `bedah exe/` ke Windows PC (atau via shared drive)

## Struktur folder yang diperlukan
```
bedah exe/
├── CyberRoad_Setup.iss      ← Script installer ini
├── extracted/
│   └── app/
│       ├── CyberRoad.exe         ← Main exe (sudah dipatch: icon + nama)
│       ├── bridge.exe
│       ├── WebView2Loader.dll
│       ├── WebView2Installer.exe
│       ├── avcodec-60.dll
│       ├── avdevice-60.dll
│       ├── avfilter-9.dll
│       ├── avformat-60.dll
│       ├── avutil-58.dll
│       ├── postproc-57.dll
│       ├── swresample-4.dll
│       ├── swscale-7.dll
│       ├── sys_config.toml       ← brand_name = "CyberRoad"
│       ├── icon.ico
│       └── tools/
│           ├── adb.exe
│           ├── AdbWinApi.dll
│           ├── AdbWinUsbApi.dll
│           ├── assistant.apk
│           ├── hidmanager.apk
│           ├── XWKeyboard.apk
│           ├── client-updater.exe
│           ├── updater.exe
│           ├── dpinst64.exe
│           ├── dpinst.xml
│           ├── dpscat.exe
│           ├── wdi-simple.exe
│           ├── XWCaptureScreen
│           └── util
└── output/                  ← Hasil installer akan ada di sini (dibuat otomatis)
```

## Cara Build

### Metode 1: GUI (mudah)
1. Buka `CyberRoad_Setup.iss` dengan Inno Setup
2. Klik menu **Build → Compile** (atau Ctrl+F9)
3. Installer selesai di: `bedah exe/output/CyberRoad_v8.337_Setup.exe`

### Metode 2: Command Line
```cmd
"C:\Program Files (x86)\Inno Setup 6\ISCC.exe" "CyberRoad_Setup.iss"
```

## Hasil
File installer: `output/CyberRoad_v8.337_Setup.exe`
- Installer akan otomatis install **WebView2 Runtime** jika belum ada
- Membuat shortcut di Desktop & Start Menu
- Menginstall **USB ADB driver** secara silent

## Apa yang sudah dimodifikasi
| File | Perubahan |
|------|-----------|
| `CyberRoad.exe` | Icon diganti + semua string "xiaowei/Panda/touping" → "cyberrd/Cyber" |
| `sys_config.toml` | brand_name = "CyberRoad" |
| Version Info | CompanyName=cyberrd, ProductName=CyberRo |

## Catatan
- App masih terhubung ke server backend `guanli.cyberrd.run`
- Nama brand di header UI ("Panda", "www.some3c.com") di-fetch dari server
  menggunakan `brand_code = "6WPTMA9HZO"` di sys_config.toml
- Untuk fullganti brand UI, perlu akses ke panel reseller di server
