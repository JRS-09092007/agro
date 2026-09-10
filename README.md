# KrishiMitra AI - Flutter Farmer Assistant App

A comprehensive Flutter application designed to help Indian farmers access AI-powered agricultural guidance, weather data, crop recommendations, water management, disease detection, and expert connection through public Indian government datasets.

## Features

### 1. **Multilingual Support** 🌐
- English (English)
- Hindi (हिंदी)
- Marathi (मराठी)
- Telugu (తెలుగు)
- Tamil (தமிழ்)
- Kannada (ಕನ್ನಡ)
- Change language instantly from any screen

### 2. **AI Crop Recommendations** 🌾
- Based on soil type, season, and water availability
- Uses **data.gov.in Agriculture Department Datasets**
- Market price information from NCDEX data
- Expected yield forecasts

### 3. **Water Advisory System** 💧
- Real-time soil moisture monitoring
- 5-day water forecast
- Daily irrigation schedule recommendations
- Water-saving tips and best practices
- Based on **IMD (Indian Meteorological Department)** weather data

### 4. **Weather Monitoring** 🌤️
- Real-time weather from **Open-Meteo API** (aligned with IMD standards)
- Temperature, humidity, rainfall, wind speed
- 5-day forecasts
- Weather alerts for extreme conditions

### 5. **Air Quality Monitoring** 🌍
- Real-time AQI data based on **CPCB Standards**
- PM2.5, PM10, Ozone, NO2 monitoring
- Air quality impact on crops
- Uses **Open-Meteo Air Quality API** (aligned with CPCB standards)

### 6. **Disease Detection** 🔍
- Plant disease identification system
- Treatment recommendations
- Prevention tips
- Severity levels

### 7. **Expert Connection** 👨‍🌾
- Connect with agricultural experts
- Government helpline numbers
- Farm visit booking
- Real-time consultation

### 8. **Offline Mode** 📱
- Access cached data without internet
- Sync status indicator
- Key features available offline

## Public Data Sources Integrated

### 1. **data.gov.in Datasets**
   - Census 2021 data
   - NFHS (National Family Health Survey) data
   - Agricultural statistics
   - Crop production data
   - Agricultural department datasets

### 2. **IMD Weather Data**
   - Real-time weather information
   - Monsoon predictions
   - Seasonal forecasts
   - Agricultural weather advisories

### 3. **CPCB Air Quality Data**
   - Air quality index (AQI)
   - Pollution levels monitoring
   - Crop impact assessment

### 4. **Census/NFHS Datasets**
   - Demographic information
   - Rural population statistics
   - Literacy rates
   - Agricultural holdings data

### 5. **State Agriculture Department Data**
   - Crop variety recommendations
   - Seed availability
   - Subsidy information
   - Agricultural schemes

## Technology Stack

- **Framework**: Flutter 3.x
- **State Management**: Provider
- **HTTP Client**: Dio
- **Local Storage**: SharedPreferences
- **Location Services**: Geolocator
- **Maps**: Google Maps Flutter
- **Charts**: FL Chart

## Project Structure

```
lib/
├── main.dart                           # App entry point
├── theme/
│   └── app_theme.dart                 # Theme configuration
├── providers/
│   ├── app_provider.dart              # App state & language
│   └── farmer_provider.dart           # Farmer data management
├── services/
│   └── api_service.dart               # API integration
└── screens/
    ├── splash_screen.dart
    ├── registration_screen.dart
    ├── dashboard_screen.dart
    ├── crop_recommendation_screen.dart
    └── water_advisory_screen.dart
```

## Installation

### Prerequisites
- Flutter SDK 3.0+
- Android Studio or Xcode
- Dart 3.0+

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/krishi-mitra.git
   cd krishi-mitra
   ```

2. **Get dependencies**
   ```bash
   flutter pub get
   ```

3. **Configure permissions** (for Android)
   - Location permission for farm coordinates
   - Camera permission for disease detection

4. **Run the app**
   ```bash
   flutter run
   ```

## API Integration Guide

### Weather Data (Open-Meteo)
```dart
final weather = await apiService.getWeatherData(latitude, longitude);
// Returns: temperature, humidity, rainfall, wind speed, condition
```

### Crop Recommendations (data.gov.in)
```dart
final crops = await apiService.getCropRecommendations(
  soilType, 
  season, 
  waterAvailability
);
// Returns: crop name, season, water needed, yield, price
```

### Air Quality (CPCB/Open-Meteo)
```dart
final airQuality = await apiService.getAirQuality(latitude, longitude);
// Returns: PM2.5, PM10, Ozone, NO2, AQI
```

## Public APIs Used

1. **Open-Meteo Weather API** (Free, no authentication)
   - Weather forecasts
   - Air quality data
   - Historical data

2. **data.gov.in APIs** (Free, registered)
   - Agricultural statistics
   - Census data
   - Government datasets

3. **IMD Data** (Via public weather API)
   - Integrated through Open-Meteo harmonization

4. **CPCB Data** (Via public air quality API)
   - Integrated through Open-Meteo harmonization

## Localization

All text strings are managed through `AppProvider.t()` method supporting:
- English
- Hindi
- Marathi
- Telugu
- Tamil
- Kannada

Add translations in `lib/providers/app_provider.dart`:
```dart
'key': {
  'en': 'English text',
  'hi': 'हिंदी पाठ',
  'mr': 'मराठी मजकूर',
  ...
}
```

## Features in Development

- [ ] Real-time disease detection with ML model
- [ ] Blockchain-based farmer credit system
- [ ] Market price tracking dashboard
- [ ] Agricultural scheme finder
- [ ] Soil health card integration
- [ ] Farmer to farmer marketplace

## Screenshots

- **Splash Screen**: Beautiful green agriculture-themed intro with language selector
- **Dashboard**: Personalized farmer greeting, weather widget, service cards
- **Crop Recommendations**: Filtered recommendations by soil type, season, water
- **Water Advisory**: Soil moisture gauge, irrigation schedule, water forecast
- **Weather Alerts**: Real-time weather and air quality monitoring

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see LICENSE file for details.

## Support

For support, email support@krishimitra.com or visit our website.

## Acknowledgments

- **data.gov.in** for providing public agricultural datasets
- **IMD** (Indian Meteorological Department)
- **CPCB** (Central Pollution Control Board)
- **Open-Meteo** for free weather and air quality APIs
- **Flutter Community** for amazing libraries and support

---

**Built with ❤️ for Indian Farmers**

*Empowering agriculture through technology and data*
