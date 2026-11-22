# Live TV (standalone)

Just the Horizon Home Live TV guide as its own app: country / category / language / source
filters, live preview, full-screen channel zapping, favourites. No home screen, no accessibility
service, no extra permissions (only INTERNET + network state).

- App id: `com.horizon.livetv` (installs next to Horizon Home, doesn't replace it)
- It reads the channel + guide data straight from the same GitHub data branch the kit uses.
  You do NOT need to deploy the Cloudflare addon for the guide to work.
- Launches from the Android TV app row (banner) or the normal app drawer.
- "Open in Nuvio" still works if Nuvio is installed; otherwise it just shows a short message.

## Build

Option A - GitHub (no setup): push this folder to a repo, open Actions -> "Build Live TV APK"
-> Run workflow, download the `LiveTV` artifact.

Option B - locally (JDK 17+, Python 3, Android SDK with build-tools 30+ and platform android-30):

    ANDROID_HOME=~/Android/Sdk ./build.sh
    # -> build/LiveTV.apk

## Install

    adb connect <tv-ip>:5555
    adb install -r build/LiveTV.apk

Signed with the kit's public `kit.keystore` (same as Horizon Home), so rebuilt versions update in place.
