# KrishiMitra AI - Complete Setup Guide

## Table of Contents
1. [Flutter Installation](#flutter-installation)
2. [Project Setup](#project-setup)
3. [Android Configuration](#android-configuration)
4. [iOS Configuration](#ios-configuration)
5. [API Configuration](#api-configuration)
6. [Running the App](#running-the-app)
7. [Building APK](#building-apk)

---

## Flutter Installation

### For Windows
1. Download Flutter SDK from https://flutter.dev/docs/get-started/install/windows
2. Extract to a location (e.g., `C:\flutter`)
3. Add Flutter to PATH:
   - System Properties → Environment Variables
   - Add `C:\flutter\bin` to PATH
4. Open Command Prompt and run:
   ```bash
   flutter doctor
   ```

### For macOS
1. Download Flutter SDK from https://flutter.dev/docs/get-started/install/macos
2. Extract to home directory:
   ```bash
   cd ~/
   tar xf ~/Downloads/flutter_macos_*.tar.xz
   ```
3. Add to PATH in `.zshrc` or `.bash_profile`:
   ```bash
   export PATH="$PATH:~/flutter/bin"
   ```
4. Run:
   ```bash
   flutter doctor
   ```

### For Linux
1. Download Flutter SDK:
   ```bash
   cd ~/
   tar xf ~/Downloads/flutter_linux_*.tar.xz
   ```
2. Add to PATH:
   ```bash
   export PATH="$PATH:$HOME/flutter/bin"
   ```
3. Run:
   ```bash
   flutter doctor
   ```

---

## Project Setup

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/krishi-mitra.git
cd krishi-mitra
```

### 2. Get Flutter Packages
```bash
flutter pub get
```

### 3. Check Setup
```bash
flutter doctor
```

Expected output should show:
- ✓ Flutter version
- ✓ Android toolchain
- ✓ Xcode (macOS/iOS)
- ✓ VS Code (or other IDE)

---

## Android Configuration

### Prerequisites
- Android SDK API level 21+
- Android emulator or physical device

### Steps

1. **Create Android Emulator**
   ```bash
   flutter emulators --create --name "krishi_emulator"
   flutter emulators --launch krishi_emulator
   ```

2. **Check Connected Devices**
   ```bash
   flutter devices
   ```

3. **Configure Permissions** (AndroidManifest.xml - already configured)
   - Location access (GPS)
   - Camera access
   - File storage

4. **Kotlin Version** (in android/app/build.gradle)
   - Already set to Java 1.8 compatible

---

## iOS Configuration

### Prerequisites
- macOS with Xcode installed
- iOS deployment target 11.0+

### Steps

1. **Install Pods**
   ```bash
   cd ios
   pod install
   cd ..
   ```

2. **Update Deployment Target**
   - Open `ios/Podfile`
   - Ensure platform version is 11.0+
   - Run `pod install` again

3. **Configure Permissions** (ios/Runner/Info.plist)
   ```xml
   <key>NSLocationWhenInUseUsageDescription</key>
   <string>This app needs your location to provide weather and water advisory for your farm.</string>
   <key>NSCameraUsageDescription</key>
   <string>This app needs camera access for disease detection.</string>
   <key>NSPhotoLibraryUsageDescription</key>
   <string>This app needs photo library access for crop images.</string>
   ```

---

## API Configuration

### 1. Public APIs (No Configuration Needed)

#### Open-Meteo Weather API
- **Endpoint**: https://api.open-meteo.com/v1/forecast
- **Rate Limit**: 10,000 free requests/day
- **No authentication needed**
- Used for: Weather data, air quality

#### data.gov.in Agriculture APIs
- **Website**: https://data.gov.in
- **Registration**: Free, optional for unlimited access
- **Used for**: Crop recommendations, agricultural statistics

### 2. Location Services (Already Configured)

#### Android
- Add to `android/app/src/main/AndroidManifest.xml`:
  ```xml
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  ```

#### iOS
- Permissions configured in `Info.plist` (see iOS Configuration)

### 3. Optional: Google Maps Integration (Future)

When integrating Google Maps:

1. **Get Google Maps API Key**
   - Go to Google Cloud Console
   - Create a new project
   - Enable Maps JavaScript API
   - Create API key
   - Restrict to Android/iOS

2. **Android Configuration**
   - Add to `android/app/src/main/AndroidManifest.xml`:
     ```xml
     <meta-data
         android:name="com.google.android.geo.API_KEY"
         android:value="YOUR_API_KEY" />
     ```

3. **iOS Configuration**
   - Add to `ios/Runner/Info.plist`:
     ```xml
     <key>MAPS_API_KEY</key>
     <string>YOUR_API_KEY</string>
     ```

---

## Running the App

### Debug Mode
```bash
flutter run
```

### Release Mode (Android)
```bash
flutter run --release
```

### Hot Reload
- Press `r` during debug session
- Hot Restart: `R`

---

## Building APK

### Debug APK
```bash
flutter build apk --debug
# Output: build/app/outputs/apk/debug/app-debug.apk
```

### Release APK
```bash
flutter build apk --release
# Output: build/app/outputs/apk/release/app-release.apk
```

### App Bundle (for Google Play)
```bash
flutter build appbundle --release
# Output: build/app/outputs/bundle/release/app-release.aab
```

### Signing APK
1. Create keystore:
   ```bash
   keytool -genkey -v -keystore ~/krishi-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias krishi-key
   ```

2. Update `android/key.properties`:
   ```properties
   storePassword=YOUR_STORE_PASSWORD
   keyPassword=YOUR_KEY_PASSWORD
   keyAlias=krishi-key
   storeFile=../krishi-key.jks
   ```

3. Build:
   ```bash
   flutter build apk --release
   ```

---

## Public Data Integration

### IMD Weather Data
- **Source**: Open-Meteo API (harmonized with IMD standards)
- **Endpoints**: 
  - `/v1/forecast` - Weather forecasts
  - Updated: Real-time

### Census 2021 Data
- **Source**: data.gov.in
- **Available**: Population, agriculture holdings, demographics
- **Format**: REST API, JSON

### NFHS Data
- **Source**: data.gov.in
- **Available**: Health, nutrition, rural statistics
- **Format**: REST API, JSON

### CPCB Air Quality
- **Source**: Open-Meteo AQI (aligned with CPCB)
- **Endpoints**: `/v1/air-quality`
- **Pollutants**: PM2.5, PM10, O3, NO2

### State Agriculture Department
- Varies by state
- Access through state portals or data.gov.in

---

## Troubleshooting

### Flutter Doctor Issues
```bash
flutter doctor -v
```

### Permission Denied
- Android: Check `AndroidManifest.xml` and runtime permissions
- iOS: Check `Info.plist` and Settings → Privacy

### API Errors
- Check internet connection
- Verify Open-Meteo API status: https://status.open-meteo.com/
- Check rate limits (Open-Meteo: 10,000/day)

### Build Errors
```bash
flutter clean
flutter pub get
flutter pub upgrade
```

---

## Development Tips

1. **Enable null safety**: Already enabled in project
2. **Format code**: `flutter format .`
3. **Analyze code**: `flutter analyze`
4. **Test app**: `flutter test`
5. **Profile app**: `flutter run --profile`

---

## Resources

- [Flutter Docs](https://flutter.dev/docs)
- [Dart Docs](https://dart.dev/guides)
- [data.gov.in APIs](https://data.gov.in)
- [Open-Meteo API](https://open-meteo.com/en)
- [Android Docs](https://developer.android.com/)
- [iOS Docs](https://developer.apple.com/ios/)

---

## Support

For issues or questions:
1. Check Flutter documentation
2. Search GitHub issues
3. Post on Stack Overflow with `flutter` tag
4. Contact support@krishimitra.com

---

**Happy Farming with Technology! 🌾**
