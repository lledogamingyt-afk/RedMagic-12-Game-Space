# REDMAGIC-inspired Game Space for Samsung Galaxy A50

This is an Android Studio Kotlin project (minSdk 29, targetSdk 30) based on the screenshots supplied in the chat. It uses the supplied REDMAGIC emblem artwork as a transparent PNG asset, recolored to #FF1E32. No mechanical door intro is included. The wallpaper studio now includes the turbine wallpaper extracted from the user's supplied REDMAGIC atmospheric-map screenshot (with the screenshot's title bar, thumbnail rail, and bottom buttons cropped out), five additional cyber-themed backgrounds, and a user-selectable Gallery image.

This is an independent companion app, not official REDMAGIC software. The brand's proprietary wordmark font and REDMAGIC firmware features are not bundled. The UI uses Android's condensed sans-serif with custom letter spacing as a close, built-in visual substitute.

## Build an APK

1. Install Android Studio and a JDK 17 runtime (Android Studio includes one).
2. Open this extracted project folder in Android Studio: `RedmagicStyleGameSpace`.
3. Let Gradle sync. If prompted, install Android SDK Platform 35 and Build Tools.
4. Select **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. When Android Studio reports the build completed, click **locate** in the notification. The debug APK is normally at `app/build/outputs/apk/debug/app-debug.apk`.
6. Copy `app-debug.apk` to the Galaxy A50 and open it. Allow installation from the app used to open the file if Android asks.

To create a signed release APK: **Build > Generate Signed Bundle / APK > APK > Create new key store**, then complete the wizard and keep the keystore safe.

## Included working functions

- Landscape Game Space dashboard.
- Installed launchable-app scanner, search, pin/unpin, and actual launch via PackageManager launch intents.
- Battery percentage and battery temperature (when reported by Android), available RAM, and network throughput.
- CPU frequency readout when the Samsung kernel exposes the sysfs node; otherwise it displays N/A.
- Eco, Balance, Rise, and Diablo-style profile selections saved as software preferences. They do not modify CPU/GPU clocks or thermal controls.
- Energy Cube overlay service with left and right inward-swipe handles; two inward swipes open the panel.
- Optional pinned FPS badge.
- **Live display FPS estimate:** tap `START LIVE SCREEN FPS`, approve Android's screen-capture prompt, then enter a game. The service uses MediaProjection + ImageReader and samples changed pixels from frames captured from the actual display. This is a real screen-change-based estimate, not a made-up counter. It can be lower than the game's engine FPS because capture delivery can be throttled, image sampling can miss small changes, and it cannot see the game's internal render queue. The Galaxy A50 display is 60Hz, so it cannot display 90/120 unique frames per second.
- Wallpaper studio with the REDMAGIC Turbine Core wallpaper plus five additional built-in cyber wallpapers (Crimson Circuit, Blue Velocity, Violet Grid, Obsidian Shards, Cyan Pulse), a Gallery photo picker, preview, adjustable dimness, Cancel and Apply. The selected wallpaper and dimness are saved and restored behind the Game Space hub.
- Plugins: counter, stopwatch, random card draw, controller input notification, cast settings shortcut, and UsageStats summary (requires Usage Access).
- Settings preferences.

## Permissions and use

1. Start Game Space and tap `ENABLE ENERGY CUBE`. Grant **Display over other apps**.
2. Tap `START LIVE SCREEN FPS` and approve Android's screen recording/capture prompt. Android shows a persistent notification while capture is active.
3. Open a game. Swipe inward from the left or right edge once, then swipe inward a second time to open Energy Cube.
4. Use `PIN INFO` to keep the small FPS badge visible after closing the main panel. `STOP FPS` ends the capture stream.

The capture requires the user's explicit Android consent each time the screen-capture session is started. Some secure screens and protected video content may be excluded by Android. Android may also prevent overlays above selected system or game surfaces.

## Honest device limitations

A normal third-party Android application cannot access another app's private game-engine FPS, control Samsung CPU/GPU frequencies, overclock the GPU, change thermal limits, read GPU clocks on firmware that hides them, clear other apps' RAM, force refresh-rate modes, intercept/reject calls globally, or remap touches inside another app. The FPS feature estimates changed frames in the captured display; it is not a privileged game-engine FPS meter. The mode controls are software profile labels and preferences only. They do not create REDMAGIC Diablo Mode or hardware boosting.

`QUERY_ALL_PACKAGES` is included for the user's personal sideloaded app scanner. Google Play restricts broad app visibility; publishing there requires meeting its policy for this permission.
