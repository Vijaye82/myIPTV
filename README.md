# MyIPTV – Android TV / Google TV IPTV player

A small, private IPTV player for Chromecast with Google TV, Google TV Streamer and other
Android TV boxes. Dark, rail-based interface: scrollable top tabs, a hero banner for the
highlighted channel, and tiles you can move around with the remote.

## Sections
| Tab | What it does |
|---|---|
| Home | Continue watching, Favourites, one row per live category |
| Live TV | Search, category filter, tile grid |
| Movies | Loaded from your URL on first open; search + categories; OK plays |
| TV Series | Search + categories; OK opens seasons/episodes; OK plays an episode |
| Guide | Every channel with Now / Next |
| Catch-up | Channels with TV archive; pick one, then a past programme to watch again |
| Favourites | Hold OK on any channel tile to add/remove |
| Recordings | Active recordings (OK stops), saved recordings (OK plays, hold OK deletes), free space |

## Playlists and failover
- Settings holds any number of playlists, each with username, password, **primary URL** and **3 backups**.
  Passwords are stored encrypted. Favourites and recents are kept per playlist.
- Start-up: tries the primary, then each backup in order.
- Playback: if a stream fails, the same item is tried on the other servers (HLS first, then TS).

## Player keys
- **Live:** Up/Down (or CH +/-) change channel, **Left** starts/stops recording, **Right** toggles favourite, OK shows info.
- **Movies / episodes / catch-up / recordings:** OK pause/play, Left/Right skip 10 s, media keys work too.

## Recording
- "Record now" from live TV (Left). It records until the current programme ends (+2 min) if guide data
  exists, otherwise for 1 hour. Press Left again to stop early.
- Files are raw `.ts` saved in the app's own folder (`Android/data/com.example.myiptv/files/Movies`).
  Uninstalling the app deletes them. Check free space in the Recordings tab; boxes often have little storage.
- Many providers allow only 1–2 simultaneous connections. Watching and recording at once may use two.
- No scheduled/future recordings yet.

## Works with
Providers using the standard **Xtream Codes** API (`player_api.php`). Enter URLs as `http://host:port`.
Plain `.m3u` links are not supported. Guide, catch-up, movies and series appear only if your provider supplies them.

## Build (small APK)
1. Install Android Studio (current stable).
2. File > Open > select this `MyIPTV` folder; let Gradle sync.
3. Build Variants > `release`, then Build > Build APK(s), or run `./gradlew assembleRelease`.
   Output: `app/build/outputs/apk/release/app-release.apk` (code and resource shrinking on).

## Install on the box
1. Settings > System > About > tap *Build* 7 times, then Developer options > **Network debugging** on.
2. Note the box's IP address.
3. On your computer:
   ```
   adb connect 192.168.x.x:5555
   adb install app-release.apk
   ```

## Tips
- Typing on a TV is slow: use the Google TV phone app's keyboard, or a USB/Bluetooth keyboard.
