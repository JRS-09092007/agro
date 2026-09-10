# KrishiMitra AI - Flutter Project Summary

## Overview

**KrishiMitra AI** is a comprehensive Flutter mobile application designed specifically for Indian farmers, leveraging public government datasets to provide AI-powered agricultural guidance, real-time weather monitoring, crop recommendations, water management, and expert connections.

## Architecture

```
KrishiMitra AI (Flutter App)
│
├── Presentation Layer (Screens)
│   ├── Splash Screen
│   ├── Registration Screen
│   ├── Dashboard Screen
│   ├── Crop Recommendation Screen
│   ├── Water Advisory Screen
│   ├── Weather Alerts Screen
│   ├── Disease Detection Screen
│   ├── Expert Connection Screen
│   └── Offline Mode Screen
│
├── State Management (Provider)
│   ├── AppProvider (Language, Online/Offline status)
│   └── FarmerProvider (Farmer profile, location data)
│
├── Services Layer (API Integration)
│   └── ApiService
│       ├── Weather Data (Open-Meteo, IMD harmonized)
│       ├── Crop Recommendations (data.gov.in)
│       ├── Air Quality (CPCB aligned)
│       └── Demographic Data (Census, NFHS)
│
└── Data Layer
    └── Local Storage (SharedPreferences)
```

## Public Data Sources

### 1. **Open-Meteo API** (Free, No Key Required)
- Real-time weather forecasts
- Historical weather data
- Air quality index (AQI)
- Aligned with IMD standards
- Rate: 10,000 requests/day (free tier)

### 2. **data.gov.in** (Free, Optional Registration)
- Census 2021 data
- NFHS datasets
- Agricultural statistics
- Crop production data
- State agriculture department datasets

### 3. **IMD Data** (Via Open-Meteo)
- Monsoon forecasts
- Seasonal weather predictions
- Agricultural weather advisories

### 4. **CPCB Air Quality** (Via Open-Meteo)
- PM2.5, PM10 levels
- Ozone and NO2 measurements
- AQI calculations

## Key Features

### ✅ Implemented
1. **Splash Screen** - Green agriculture theme, language selector
2. **Registration** - Farmer profile with geotagging
3. **Dashboard** - Personalized greeting, weather widget, service cards
4. **Crop Recommendations** - Based on soil type, season, water availability
5. **Water Advisory** - Soil moisture gauge, irrigation schedule, water forecast
6. **Multilingual Support** - 6 Indian languages with instant switching
7. **Offline Mode** - Cached data access without internet
8. **Provider State Management** - Scalable architecture
9. **Location Services** - GPS-based farm coordinates
10. **Local Storage** - SharedPreferences for user data

### 🔄 Extensible
1. **Disease Detection** - ML model integration ready
2. **Weather Alerts** - Push notifications framework
3. **Expert Connection** - Video call integration ready
4. **Chat with AI** - AI service placeholder
5. **Google Maps** - Framework ready (no API key needed now)
6. **Image Upload** - Camera and gallery integration

## File Structure

```
krishi_mitra/
├── pubspec.yaml                          # Dependencies & project config
├── analysis_options.yaml                 # Linting rules
├── README.md                             # Main documentation
├── SETUP_GUIDE.md                        # Installation & setup
├── PROJECT_SUMMARY.md                    # This file
│
├── lib/
│   ├── main.dart                         # App entry point
│   ├── theme/
│   │   └── app_theme.dart               # Color, typography, theme
│   ├── providers/
│   │   ├── app_provider.dart            # Language & online status
│   │   └── farmer_provider.dart         # Farmer data management
│   ├── services/
│   │   └── api_service.dart             # Public API integration
│   └── screens/
│       ├── splash_screen.dart
│       ├── registration_screen.dart
│       ├── dashboard_screen.dart
│       ├── crop_recommendation_screen.dart
│       └── water_advisory_screen.dart
│
├── android/
│   ├── app/build.gradle                 # Android build config
│   └── app/src/main/AndroidManifest.xml # Permissions & config
│
├── ios/
│   ├── Runner/Info.plist                # iOS permissions
│   └── Podfile                          # iOS dependencies
│
└── assets/
    ├── images/                          # Image assets
    ├── icons/                           # Icon assets
    └── fonts/                           # Custom fonts (Poppins, Inter)
```

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| flutter | SDK | Framework |
| provider | ^6.0.0 | State management |
| http / dio | ^1.1.0 | API calls |
| shared_preferences | ^2.2.0 | Local storage |
| geolocator | ^9.0.2 | Location services |
| intl | ^0.19.0 | Localization |
| google_maps_flutter | ^2.5.0 | Map integration |
| image_picker | ^1.0.4 | Camera/gallery |
| permission_handler | ^11.4.3 | Permissions |
| fl_chart | ^0.65.0 | Charts & graphs |
| awesome_notifications | ^0.8.1 | Push notifications |
| connectivity_plus | ^5.0.0 | Network status |

## API Endpoints

### Weather (Open-Meteo)
```
GET https://api.open-meteo.com/v1/forecast
Parameters:
  - latitude, longitude
  - current: temperature_2m, relative_humidity_2m, weather_code, etc.
  - temperature_unit: celsius
  - wind_speed_unit: kmh
```

### Air Quality (Open-Meteo)
```
GET https://air-quality-api.open-meteo.com/v1/air-quality
Parameters:
  - latitude, longitude
  - current: pm10, pm2_5, ozone, nitrogen_dioxide, us_air_quality_index
```

### Crop Recommendations (data.gov.in)
```
Local mock data based on Indian agricultural science
Future: Direct API integration via data.gov.in
```

## Localization

### Supported Languages
1. English (en)
2. Hindi (hi) - हिंदी
3. Marathi (mr) - मराठी
4. Telugu (te) - తెలుగు
5. Tamil (ta) - தமிழ்
6. Kannada (kn) - ಕನ್ನಡ

### How to Add New Language
1. Open `lib/providers/app_provider.dart`
2. Add new language object in translations map
3. Add UI option in language selector

## Theme Colors

- **Primary Green**: `#1B5E20` (Forest green)
- **Accent Gold**: `#F59E0B` (Golden harvest)
- **Sky Blue**: `#0369A1` (Agricultural blue)
- **Earth Brown**: `#92400E` (Soil tone)
- **White**: `#FFFFFF` (Clean background)
- **Light Gray**: `#F3F4F6` (Secondary background)
- **Medium Gray**: `#D1D5DB` (Border & text)
- **Dark Gray**: `#374151` (Primary text)

## Development Workflow

### Setup
```bash
git clone <repo-url>
cd krishi-mitra
flutter pub get
flutter doctor
```

### Development
```bash
flutter run                  # Debug mode
flutter run --release       # Release mode
flutter analyze              # Code analysis
flutter format .            # Format code
```

### Building
```bash
flutter build apk           # Android debug APK
flutter build apk --release # Android release APK
flutter build appbundle     # Google Play App Bundle
flutter build ios           # iOS app
```

## API Rate Limits & Quotas

| API | Rate Limit | Cost |
|-----|-----------|------|
| Open-Meteo | 10,000 req/day | Free |
| data.gov.in | Varies | Free |
| Google Maps | (Future) | ~$7/1000 req |

## Security Considerations

1. **No sensitive data** stored locally (except farmer location)
2. **All API calls** use HTTPS
3. **Permissions** requested at runtime (Android 6+)
4. **User location** only accessed with explicit permission
5. **Local data** encrypted via platform defaults

## Performance Optimizations

1. **Image optimization** for low bandwidth
2. **Caching** with SharedPreferences
3. **Lazy loading** of screens
4. **Provider** for efficient state management
5. **Null safety** enabled throughout

## Testing Strategy

### Unit Tests
- Provider logic tests
- API service mock tests
- Data model tests

### Widget Tests
- Screen rendering tests
- Interaction tests
- Navigation tests

### Integration Tests
- End-to-end flows
- API integration
- Real device testing

## Deployment

### Android
1. Build release APK: `flutter build apk --release`
2. Upload to Google Play Store
3. Targeting: API 21+ (Android 5.0+)

### iOS
1. Build release bundle: `flutter build ios --release`
2. Upload via TestFlight/App Store Connect
3. Targeting: iOS 11.0+

## Future Enhancements

### Phase 2
- [ ] Real-time disease detection with TensorFlow Lite
- [ ] Farmer-to-expert video consultation
- [ ] Market price tracking dashboard
- [ ] Agricultural scheme finder
- [ ] Soil health card integration

### Phase 3
- [ ] Blockchain farmer credit system
- [ ] Farmer-to-farmer marketplace
- [ ] Supply chain tracking
- [ ] Crop insurance integration
- [ ] Government subsidy portal

## Monitoring & Analytics

### Future Implementation
- Firebase Crashlytics for error tracking
- Firebase Analytics for user behavior
- Sentry for performance monitoring
- Custom analytics dashboard

## Support & Contact

- **Email**: support@krishimitra.com
- **Website**: www.krishimitra.com
- **Documentation**: See README.md & SETUP_GUIDE.md
- **Issues**: GitHub Issues

## License

MIT License - See LICENSE file for details

## Credits

- **Data Sources**: data.gov.in, IMD, CPCB, Census 2021, NFHS
- **API Provider**: Open-Meteo (Free weather/AQI data)
- **Framework**: Flutter by Google
- **Packages**: Community packages from pub.dev

---

## Deployment Checklist

- [ ] Update version in pubspec.yaml
- [ ] Run `flutter analyze` - no errors
- [ ] Run `flutter test` - all pass
- [ ] Update README with changes
- [ ] Test on Android device
- [ ] Test on iOS device
- [ ] Generate signed APK
- [ ] Upload to Play Store
- [ ] Create release notes
- [ ] Monitor crash reports

---

**KrishiMitra AI - Empowering Indian Farmers with Technology** 🌾

*Built with Flutter | Powered by Public Data | For Every Indian Farm*
