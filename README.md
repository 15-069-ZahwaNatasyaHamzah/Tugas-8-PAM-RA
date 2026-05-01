# MyProfile & Notes App - Kotlin Multiplatform

Aplikasi manajemen catatan (Notes App) ini merupakan pengembangan lanjutan berbasis **Compose Multiplatform** yang kini mengimplementasikan **Dependency Injection menggunakan Koin** untuk mengelola seluruh dependensi aplikasi secara terstruktur. Aplikasi tetap menggunakan **SQLDelight** dengan pendekatan *offline-first* serta mendukung fitur utama seperti **CRUD**, **pencarian**, dan **pengaturan** dengan **DataStore**. Selain itu, ditambahkan fitur **Device Info** dan **Network Monitor** berbasis *expect/actual* untuk mendukung multiplatform, yang ditampilkan pada halaman Settings dan indikator status jaringan di halaman utama. Dengan arsitektur **MVVM** dan pengelolaan **UI state** yang baik, aplikasi menjadi lebih modular, responsif, dan siap digunakan di berbagai platform.

## Fitur

1. **Dependency Injection Koin**: Seluruh aplikasi telah dimigrasikan menggunakan Koin untuk Dependency Injection. Semua komponen (Repository, ViewModel, dan layanan platform) kini dikelola dan di-*inject* melalui Koin.
2. **DeviceInfo Multiplatform**: Implementasi `DeviceInfo` menggunakan `expect/actual` untuk mendapatkan informasi perangkat seperti nama device, sistem operasi, dan versi pada Android, iOS, JVM, dan Web.
3. **NetworkMonitor Real-time**: Implementasi `NetworkMonitor` menggunakan `expect/actual` untuk memantau status koneksi internet secara real-time.
4. **Integrasi Settings**: Informasi perangkat ditampilkan secara dinamis pada halaman Profile/Settings.
5. **Indikator Status Jaringan**: Indikator "Mode Offline" akan muncul di halaman utama ketika perangkat kehilangan koneksi internet.
6. **ViewModel dengan Koin**: ViewModel disediakan menggunakan `koinViewModel()` dari library `io.insert-koin:koin-compose-viewmodel`.

## Architecture Diagram

Aplikasi ini menggunakan pendekatan Arsitektur Bersih dengan Koin sebagai kontainer Injeksi Ketergantungan utama.

```mermaid
graph TD
    subgraph "UI Layer (Common)"
        App[App.kt - Main Entry]
        Screens[Screens - Notes, Profile, Add/Edit]
        ViewModels[ViewModels - NotesViewModel, ProfileViewModel]
    end

    subgraph "Domain/Data Layer (Common)"
        Repository[NoteRepository]
        Database[NoteDatabase - SQLDelight]
    end

    subgraph "Platform Layer (Expect/Actual)"
        DeviceInfo[DeviceInfo Interface]
        NetworkMonitor[NetworkMonitor Interface]
        DI_Platform[Platform DI Module]
    end

    subgraph "DI (Koin)"
        Koin[Koin Container]
    end

    ViewModels --> Repository
    Repository --> Database
    ViewModels --> DeviceInfo
    App --> NetworkMonitor
    Koin --> ViewModels
    Koin --> Repository
    Koin --> DeviceInfo
    Koin --> NetworkMonitor
```

## Tech Stack

-   **UI Framework**: [Compose Multiplatform](https://www.jetbrains.com/lp/compose-multiplatform/)
-   **Dependency Injection**: [Koin 4.0.0](https://insert-koin.io/)
-   **Database**: [SQLDelight](https://cashapp.github.io/sqldelight/)
-   **Navigation**: [Jetpack Navigation Compose](https://developer.android.com/jetpack/compose/navigation)

## Cara Menjalankan Project

1. **Persiapan Resource**: Pastikan file `profile_user.png` berada di folder `composeApp/src/commonMain/composeResources/drawable/`.
2. **Sync Project**: Lakukan *Gradle Sync* di Android Studio.
3. **Run**:
   - Untuk Android: Pilih modul `composeApp` lalu klik **Run**.
   - Untuk Desktop: Jalankan perintah `./gradlew :composeApp:run` di terminal.

## Dokumentasi Visual

| Device Info (Settings) | Network Indicator (Offline) |
| :---: | :---: |
|<img width="484" height="867" alt="image" src="https://github.com/user-attachments/assets/d5a000a5-27fc-4876-819d-ab42c4c90152" /> | <img width="490" height="870" alt="image" src="https://github.com/user-attachments/assets/bae5acb1-91f5-45b8-b2f5-99dad0b40b66" /> |

## Video Demo
Video demo fitur aplikasi dapat diakses melalui tautan berikut : https://youtube.com/shorts/Eypx0dphVhA?si=yh4oL_Qskx9HwC2l

---
