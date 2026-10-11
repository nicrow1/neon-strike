# Neon Strike — сборка APK

Игра лежит в `www/index.html`. APK собирается автоматически в GitHub Actions, ставить Android Studio не нужно.

## Как получить APK
1. Создайте на github.com новый пустой репозиторий (бесплатно).
2. Загрузите в него всё содержимое этой папки (кнопка «Add file → Upload files»). Важно, чтобы папка `.github` тоже загрузилась.
3. Откройте вкладку **Actions** → **Build APK** → **Run workflow**. Сборка идёт 5–10 минут.
4. Когда появится зелёная галочка, откройте запуск и в разделе **Artifacts** скачайте `neon-strike-apk` (внутри `app-debug.apk`).
5. Перенесите файл на телефон и установите. Android попросит разрешить установку из неизвестных источников.

## Сборка на своём компьютере
Нужны Node.js 20, JDK 17 и Android Studio (SDK):
```
npm install
npx cap add android
npx @capacitor/assets generate --android
npx cap sync android
cd android && ./gradlew assembleDebug
```
Файл появится в `android/app/build/outputs/apk/debug/app-debug.apk`.
Чтобы игра была в горизонтальной ориентации, добавьте `android:screenOrientation="sensorLandscape"` к тегу `<activity>` в `android/app/src/main/AndroidManifest.xml`.

## Google Play
Debug-APK подходит для установки у себя и друзей. Для публикации в Google Play нужна подписанная release-сборка (AAB) и аккаунт разработчика.
