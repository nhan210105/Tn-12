# Reg Mod Cache 2.0.3 — crash-fixed reconstruction

This project is a source reconstruction from the supplied `Reg Mod Cache 2.0.3` IPA. The IPA contains a stripped arm64 Mach-O, so the original Swift source cannot be recovered byte-for-byte.

## What was found
- SwiftUI app classes including `APIService`, `LocalizationManager`, `ThemeManager`, `GunModView`, `HitboxModView`, `GameGuideView`, `SettingsView`, `LoginView`, and `ContentView`.
- Network endpoints and JSON handling in the binary.
- Crash signatures including `Down-casted Array element failed to match the target type`, `NSArray element failed to match the Swift Array Element type`, and `Fatal error`.
- File importer / filesystem operations.

## Crash-focused changes
1. API JSON decoding is now tolerant of missing/wrong fields.
2. HTTP/non-JSON responses no longer reach unsafe casts.
3. File importer callbacks use explicit `Result` handling and never force-unwrap a URL.
4. UI callbacks are returned to the main actor/thread before mutating published state.
5. Persistent session decoding is optional; corrupt saved data is ignored instead of terminating startup.
6. UIKit appearance setup is isolated to app initialization.
7. Compatibility classes are safe stubs rather than unsafe process/container injection.

## Build
Open `RegMod.xcodeproj` in Xcode, choose your Signing Team, then Build/Archive.

Bundle identifier: `com.cheatiosvn.modstudio`
Version: `2.0.3 (3)`
Minimum iOS: `15.0`
