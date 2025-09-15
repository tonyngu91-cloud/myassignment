# NIT3213 Android Assignment — Three-screen App (Login → Dashboard → Details)

## What it does
- **Login** with `username` (first name) and `password` (student ID digits only), selecting a **campus**.
- On success, a `keypass` is returned and used to request the **Dashboard**.
- **Dashboard** shows a list of `entities` (summary only). Tapping opens **Details** with all fields.
- **Error/Loading states** handled via a `UiState` sealed class.

## Build & Run
- **Android Studio** Iguana+ (AGP 8.x), **JDK 17 or 11**
- **Min SDK 28**, **Target/Compile 34**
- Open the project, **Sync Gradle**, then Run.

## API config
- Base URL is in `NetworkModule.kt` (`https://nit3213api.onrender.com/`).
- Login tries `/{campus}/auth` first; on 404, falls back to `/auth/{campus}`.
- Change campus via the Login screen dropdown (or set default in code).

## Project structure
- `data/remote` — `ApiService`, DTOs.
- `data/local` — `SessionStore` using **DataStore** to persist `keypass` and `campus`.
- `data/Repository.kt` — API calls and 404-fallback logic.
- `ui/login|dashboard|details` — Fragments, Adapter, and ViewModels.
- `di/NetworkModule.kt` — Hilt DI for Retrofit/OkHttp/Moshi.
- `util/UiState.kt` — Loading/Success/Error state model.

## Tests
- Run all unit tests: `./gradlew test`
- Instrumented: `./gradlew connectedAndroidTest` (requires device/emulator).

## Known issues / Notes
- Auto-resume to Dashboard on app start can be added by reading `SessionStore.keypass` and navigating if present.
- Minify (R8/Proguard) is off in `release` by default.