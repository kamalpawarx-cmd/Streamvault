# StreamVault

Minimal mobile app for watching movies, web series and anime, with offline downloads. Built with Expo (React Native), so one codebase runs on Android and iOS.

## Run it

```bash
npm install
npx expo install --fix   # aligns package versions with Expo SDK 53
npx expo start           # scan the QR code with Expo Go
```

## Structure

```
App.js                      navigation (tabs + detail + player)
src/theme.js                colors
src/data.js                 catalog (placeholder, replace this)
src/downloads.js            download manager (expo-file-system + AsyncStorage)
src/components/PosterCard.js
src/screens/HomeScreen.js       search, Movie/Series/Anime filters, poster grid
src/screens/DetailScreen.js     info, play, download, episode list
src/screens/PlayerScreen.js     landscape player, uses the offline file if present
src/screens/DownloadsScreen.js  downloaded titles, progress, delete
```

## Offline behavior

Tapping Download saves the video to the app's document directory and records it in AsyncStorage. The player checks for a local copy first and falls back to streaming, so downloaded titles play with no connection.

## Uploading your own videos

Tap **＋ Upload** on Home to pick one or more videos from the device. They are copied into the app's storage, appear under the **My Uploads** filter, and play offline like any download. Open an upload and tap Delete to remove it. Implemented in `src/uploads.js` with `expo-document-picker`.

## Content

`src/data.js` ships with freely licensed sample videos (Big Buck Bunny, Sintel and others) so the app works out of the box. Replace them with content you have the rights to, or fetch the list from your own backend. Each episode only needs an `id`, `title` and a direct video `url` (mp4 or HLS).

## Next steps

- Continue watching (save playback position in AsyncStorage)
- Pause/resume downloads
- HLS streams with multiple audio and subtitle tracks
- Wi-Fi-only download setting
