# Android Studio launch fix

Date fixed: 24 June 2026

## Problem

Android Studio 2026.1.1 Patch 2 stopped launching after its boot runtime was changed to the custom JetBrains Runtime (JBR) 25.0.3.

The JVM Class Data Sharing warning was harmless and was not the cause of the launch failure.

## Fix applied

The custom runtime override file was renamed from:

```text
C:\Users\91855\AppData\Roaming\Google\AndroidStudio2026.1.1\studio64.exe.jdk
```

to this backup:

```text
C:\Users\91855\AppData\Roaming\Google\AndroidStudio2026.1.1\studio64.exe.jdk.disabled
```

With the override disabled, Android Studio uses its bundled JetBrains Runtime again.

## Verified result

- Android Studio launched successfully.
- The `CollegeCutoffAnalyser` project opened successfully.
- The IDE log confirmed JetBrains OpenJDK 21.0.10 as the active runtime.

## Recommendation

Keep Android Studio on its bundled JBR 21. Configure a separate JDK under **Settings > Build, Execution, Deployment > Build Tools > Gradle** when a different Gradle JDK is required. Do not select JBR 25 as the boot runtime for this Android Studio build.

## Reverting the fix

To restore the custom runtime, close Android Studio and rename `studio64.exe.jdk.disabled` back to `studio64.exe.jdk`. This is not recommended unless the custom runtime is known to be compatible.
