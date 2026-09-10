# Quick Start Guide - KrishiMitra AI

## 5-Minute Setup

### Requirements
- Flutter SDK 3.0+
- Android emulator or device
- 5 minutes

### Steps

1. **Get the Code**
   ```bash
   cd krishi-mitra
   flutter pub get
   ```

2. **Run the App**
   ```bash
   flutter run
   ```

3. **You're Done!** 🎉

The app will open with:
- Splash screen with language selector
- Registration form (enter your farm details)
- Dashboard with weather, services, and recommendations

---

## First Time Usage

1. **Select Language** - Choose from 6 Indian languages
2. **Enter Farmer Details**:
   - Name
   - Village/District
   - Land size (in acres)
   - Soil type (Loamy, Black, Red, Alluvial, Sandy)
   - Water source (Well, Bore, Canal, River, Tank)
   - Tap "Get Location" for GPS coordinates

3. **View Dashboard**
   - See current weather
   - Browse crop recommendations
   - Check water advisory
   - Access other services

---

## Change Language Anytime

- **Dashboard**: Tap language button (top-right) → Select language
- **Any Screen**: Use the language switcher from the header
- **Instant**: No app restart needed!

---

## Public Data Used

✅ **No API Keys Required** - All data is free!

- **Weather**: Open-Meteo API (10,000 requests/day)
- **Crops**: data.gov.in agriculture datasets
- **Air Quality**: CPCB-aligned pollution data
- **Demographics**: Census 2021, NFHS data

---

## Features Available Now

| Feature | Status | Details |
|---------|--------|---------|
| Multi-language | ✅ | 6 Indian languages |
| Weather | ✅ | Real-time + 5-day forecast |
| Crop Recommendations | ✅ | Based on soil, season, water |
| Water Advisory | ✅ | Irrigation schedule + tips |
| Location | ✅ | GPS-based farm tagging |
| Offline | ✅ | Access cached data |
| Expert Connect | 🔄 | Coming soon |
| Disease Detection | 🔄 | ML model coming |
| AI Chat | 🔄 | Gemini API coming |

---

## Commands

```bash
# Development
flutter run                    # Run in debug mode
flutter run --release        # Run in release mode
flutter hot-reload           # Quick refresh (press 'r')

# Cleaning
flutter clean                 # Clean build artifacts
flutter pub get              # Download dependencies

# Building
flutter build apk            # Build Android APK
flutter build appbundle      # Build for Play Store
flutter build ios            # Build for App Store

# Quality
flutter analyze              # Check code issues
flutter format .             # Format code
flutter test                 # Run tests
```

---

## File Structure

```
lib/
├── main.dart                          # App start
├── theme/app_theme.dart               # Colors & design
├── providers/                         # State management
├── services/api_service.dart          # API calls
└── screens/                           # UI screens
```

---

## Key Files

| File | Purpose |
|------|---------|
| `pubspec.yaml` | Dependencies |
| `lib/main.dart` | App entry |
| `lib/providers/app_provider.dart` | Language & status |
| `lib/services/api_service.dart` | Weather, crops, AQI |
| `android/app/src/main/AndroidManifest.xml` | Permissions |

---

## Troubleshooting

### App won't run
```bash
flutter clean
flutter pub get
flutter run
```

### Permission errors (Android)
- Grant location & camera permissions
- Android 6+: Runtime permissions required

### Network error
- Check internet connection
- Open-Meteo API status: https://status.open-meteo.com/

### Location not working
- Grant location permission in Settings
- Use real device or emulator with Play Services

---

## API Response Examples

### Weather Data
```json
{
  "temp": "28°C",
  "humidity": "70%",
  "rainfall": "0mm",
  "windSpeed": "8 km/h",
  "condition": "Partly Cloudy"
}
```

### Crop Recommendations
```json
{
  "cropName": "Rice",
  "season": "Monsoon",
  "waterNeeded": "120-150 cm",
  "expectedYield": "40-50 q/ha",
  "marketPrice": "₹2,100-2,300"
}
```

### Air Quality
```json
{
  "pm25": "45.2 μg/m³",
  "pm10": "78.5 μg/m³",
  "aqi": "125"
}
```

---

## Environment Variables

**None required!** All APIs are:
- Free tier
- No authentication
- Public data

---

## Best Practices

1. ✅ **Always** grant location permission for accurate weather
2. ✅ **Keep** app updated for latest public data
3. ✅ **Check** water advisory before irrigation
4. ✅ **Use** offline mode when internet is slow
5. ✅ **Change** language for farmer comfort

---

## Getting Help

1. **Documentation**: Read README.md & SETUP_GUIDE.md
2. **Issues**: Check GitHub issues
3. **API Status**: https://status.open-meteo.com/
4. **Flutter Docs**: https://flutter.dev/docs

---

## Next Steps

After first run:
1. Explore all screens
2. Test language switching
3. Check weather for your area
4. Review crop recommendations
5. Plan irrigation schedule

---

## Pro Tips

💡 **Tip 1**: Bookmark crop recommendations for later reference

💡 **Tip 2**: Check water advisory before every irrigation

💡 **Tip 3**: Monitor air quality during crop spraying

💡 **Tip 4**: Use offline mode during field work

💡 **Tip 5**: Share app with neighboring farmers!

---

## Feedback

Share feedback at: support@krishimitra.com

---

**Happy Farming! 🌾** 

*KrishiMitra - Your Intelligent Farm Assistant*

---

**Version**: 1.0.0  
**Last Updated**: 2024  
**Status**: Active Development
