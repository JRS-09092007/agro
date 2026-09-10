# Public Data Integration Guide - KrishiMitra AI

## Overview

KrishiMitra AI integrates multiple free, public Indian government datasets to provide comprehensive agricultural guidance without requiring any commercial API keys.

---

## 1. Weather Data Integration

### Current Implementation: Open-Meteo API
- **Free Tier**: 10,000 requests/day
- **No Authentication**: Public API
- **Alignment**: Harmonized with IMD (Indian Meteorological Department) standards

### Endpoint
```
GET https://api.open-meteo.com/v1/forecast
```

### Parameters
```dart
queryParameters: {
  'latitude': 20.5937,          // Farm latitude
  'longitude': 78.9629,         // Farm longitude
  'current': 'temperature_2m,relative_humidity_2m,weather_code,wind_speed_10m,precipitation',
  'temperature_unit': 'celsius',
  'wind_speed_unit': 'kmh',
}
```

### Response Example
```json
{
  "current": {
    "temperature_2m": 28.5,
    "relative_humidity_2m": 65,
    "weather_code": 61,
    "wind_speed_10m": 12.4,
    "precipitation": 0.0
  }
}
```

### IMD Data Mapping
- **WMO Codes**: Open-Meteo uses WMO standard codes (same as IMD)
- **Seasonal Data**: Monsoon forecasts aligned with IMD predictions
- **Regional Variations**: Latitude/longitude specific forecasts

### Future: Direct IMD Integration
```
IMD Website: https://www.imd.gov.in/
Public FTP: ftp://ftp.imd.gov.in/ (Contains gridded weather data)
```

---

## 2. Crop Recommendations Data

### Current Implementation
Local database based on **ICAR (Indian Council of Agricultural Research)** and **State Agriculture Department** guidelines.

### Data Structure
```dart
class CropRecommendation {
  final String cropName;      // Rice, Wheat, Cotton, etc.
  final String season;        // Kharif, Rabi, Summer
  final String waterNeeded;   // cm of water required
  final String expectedYield; // quintals per hectare
  final String marketPrice;   // Current market price
}
```

### Data Sources

#### 1. **data.gov.in Agriculture Datasets**
```
Website: https://data.gov.in/
Search: "Agricultural Production", "Crop Data", "Yield"
```

#### 2. **NCDEX Market Prices**
```
Website: https://www.ncdex.com/
Free Data: Historical and current prices
Products: All major agricultural commodities
```

#### 3. **State Agriculture Department Portals**
```
Maharashtra: https://mahaagri.gov.in/
Punjab: https://agriharyana.gov.in/
Karnataka: https://raitamitra.karnataka.gov.in/
```

### Integration Example
```dart
Future<List<CropRecommendation>> getCropRecommendations(
  String soilType,
  String season,
  String waterAvailability,
) async {
  // Logic based on:
  // 1. Soil type classification (ICAR standards)
  // 2. Season (Kharif/Rabi/Summer)
  // 3. Water availability (Low/Medium/High)
  
  return cropRecommendations;
}
```

### Crop Database (by Soil Type)

#### Loamy Soil - Best For:
- Rice (Kharif) - 120-150 cm water
- Wheat (Rabi) - 40-50 cm water
- Maize - 50-80 cm water
- Cotton - 60-80 cm water

#### Black Soil - Best For:
- Cotton - 60-80 cm water
- Jowar - 40-60 cm water
- Sugarcane - 150-200 cm water
- Pulses - 30-40 cm water

#### Red Soil - Best For:
- Groundnut - 50-65 cm water
- Millets - 30-40 cm water
- Spices - Variable
- Pulses - 30-40 cm water

---

## 3. Air Quality Data Integration

### Current Implementation: Open-Meteo AQI API
- **Free Tier**: Unlimited requests
- **CPCB Alignment**: Uses same pollutant standards
- **Real-time Data**: Updated hourly

### Endpoint
```
GET https://air-quality-api.open-meteo.com/v1/air-quality
```

### Parameters
```dart
queryParameters: {
  'latitude': 20.5937,
  'longitude': 78.9629,
  'current': 'pm10,pm2_5,ozone,nitrogen_dioxide,us_air_quality_index',
}
```

### Pollutants Monitored
```
1. PM2.5 (Particulate Matter <2.5μm)  - Dangerous for respiration
2. PM10 (Particulate Matter <10μm)    - Affects air quality
3. Ozone (O3)                         - Crop damage indicator
4. NO2 (Nitrogen Dioxide)             - Pollution level
5. AQI (Air Quality Index)            - 0-500 scale
```

### CPCB Standards Mapping
```
AQI Range   | Category          | Health Impact
0-50        | Good              | Safe to farm
51-100      | Satisfactory      | Minor caution
101-200     | Moderately Poor   | Avoid spraying
201-300     | Poor              | Very unsafe
301-400     | Very Poor         | Highly hazardous
400+        | Severe            | Emergency level
```

### Future: Direct CPCB Integration
```
CPCB Portal: https://www.cpcb.gov.in/
Air Quality Data: Real-time air quality stations
Format: XML/JSON APIs (State wise)
```

---

## 4. Census Data Integration

### Source: data.gov.in
```
URL: https://data.gov.in/
Dataset: Census 2021 Agricultural Data
```

### Relevant Census Fields for Agriculture
```
1. Agricultural Holdings Distribution
   - Small holdings (<2 ha)
   - Marginal holdings (<1 ha)
   - Large holdings (>10 ha)

2. Land Use Classification
   - Forest land
   - Agricultural land
   - Net sown area

3. Crop-wise Area and Production
   - State-wise data
   - District-wise data
   - Season-wise breakdown

4. Rural Population
   - Farmer demographics
   - Literacy rate in rural areas
   - Income levels
```

### API Structure (data.gov.in)
```
{
  "records": [
    {
      "district": "Pune",
      "state": "Maharashtra",
      "totalFarmers": 45230,
      "avgFarmSize": 1.8,
      "primaryCrop": "Sugarcane",
      "secondaryCrop": "Jowar"
    }
  ]
}
```

---

## 5. NFHS Data Integration

### Source: NFHS-5 (2019-2021)
```
Website: https://www.nfhsindia.org/
Free Download: State and district level data
```

### Agriculture-Related NFHS Data
```
1. Rural Infrastructure
   - Road connectivity
   - Electricity access
   - Water supply

2. Health Indicators
   - Nutritional status (relevant to crop selection)
   - Healthcare access (for farmer welfare)

3. Education
   - Literacy rate (adoption of new techniques)
   - Agricultural training access

4. Livelihood
   - Primary occupation (farming)
   - Land ownership percentage
```

### Integration Example
```dart
Future<Map<String, dynamic>> getDemographicData(String district) async {
  // Returns NFHS data for district
  return {
    'district': 'Pune',
    'ruralPopulation': 2500000,
    'literacyRate': 78,
    'avgFarmSize': 1.8,
    'primaryOccupation': 'Agriculture',
    'hasElectricity': 95,
    'hasWaterSupply': 87,
  };
}
```

---

## 6. State Agriculture Department Data

### Access Methods

#### Maharashtra
```
Portal: https://mahaagri.gov.in/
Data: Crop rates, schemes, weather
Format: Web portal, SMS service
```

#### Punjab
```
Portal: https://agriharyana.gov.in/
Data: Procurement rates, equipment subsidy
Format: Web portal, Mobile app
```

#### Karnataka
```
Portal: https://raitamitra.karnataka.gov.in/
Data: Soil health, market prices
Format: Mobile app, Web
```

#### Telangana
```
Portal: https://agriculture.telangana.gov.in/
Data: e-NAM, market prices, weather
Format: Web, e-NAM API
```

### Typical Data Points
```
1. Current Market Prices
   - Wholesale rates
   - Retail rates
   - Trend analysis

2. Weather Advisories
   - Pest warnings
   - Disease alerts
   - Seasonal guidance

3. Subsidy Information
   - Equipment subsidies
   - Seed subsidies
   - Irrigation subsidies

4. Government Schemes
   - PM-KISAN
   - Crop Insurance
   - Agricultural loans
```

---

## 7. Current API Implementations

### Weather Service
```dart
Future<WeatherData> getWeatherData(
  double latitude,
  double longitude,
) async {
  // Calls Open-Meteo API
  // Returns: temp, humidity, rainfall, wind speed, condition
}
```

### Crop Recommendations Service
```dart
Future<List<CropRecommendation>> getCropRecommendations(
  String soilType,
  String season,
  String waterAvailability,
) async {
  // Returns curated crop recommendations
  // Based on local agricultural science data
}
```

### Air Quality Service
```dart
Future<AirQualityData> getAirQuality(
  double latitude,
  double longitude,
) async {
  // Calls Open-Meteo Air Quality API
  // Returns: PM2.5, PM10, O3, NO2, AQI
}
```

### Demographic Data Service
```dart
Future<Map<String, dynamic>> getDemographicData(
  String district,
) async {
  // Returns Census 2021 & NFHS data
  // For targeted interventions
}
```

---

## 8. Adding New Public Data Sources

### Step 1: Identify Data Source
- Check data.gov.in for availability
- Verify free access tier
- Note any registration requirements

### Step 2: API Structure
```dart
// Add method to ApiService
Future<NewDataType> getNewData(String parameter) async {
  try {
    final response = await _dio.get(
      'https://api-endpoint.com/data',
      queryParameters: {'param': parameter},
    );
    
    if (response.statusCode == 200) {
      // Parse response
      return parseResponse(response.data);
    }
  } catch (e) {
    return getDefaultData();
  }
}
```

### Step 3: Model Class
```dart
class NewData {
  final String field1;
  final String field2;
  
  NewData({required this.field1, required this.field2});
}
```

### Step 4: Integration in UI
```dart
// In screen provider
final data = await apiService.getNewData('parameter');
setState(() {
  _newData = data;
});
```

---

## 9. Rate Limits & Quotas

| API | Free Limit | Cost Beyond | Notes |
|-----|-----------|------------|-------|
| Open-Meteo Weather | 10,000/day | €0.003/req | No signup needed |
| Open-Meteo AQI | Unlimited | Unlimited | No signup needed |
| data.gov.in | Unlimited | Unlimited | Free registration |
| NFHS | Unlimited | N/A | Public data |
| State AG Portals | Unlimited | Unlimited | Free access |

---

## 10. Offline Data Strategy

### Cached Data
```dart
// SharedPreferences caching
await _prefs.setString('last_weather', jsonEncode(weatherData));
await _prefs.setString('crop_recommendations', jsonEncode(crops));
await _prefs.setString('air_quality', jsonEncode(aqi));
```

### Update Strategy
```dart
// Check last update time
final lastUpdate = _prefs.getInt('weather_last_update') ?? 0;
final now = DateTime.now().millisecondsSinceEpoch;

if (now - lastUpdate > 3600000) { // 1 hour
  // Fetch fresh data
  await updateWeather();
}
```

---

## 11. Privacy & Security

### Data Collection
✅ No personal data collected beyond farmer's own farm location  
✅ All external APIs use HTTPS  
✅ No tracking or analytics without consent  
✅ Local data stored securely via platform APIs  

### Data Storage
```dart
// Farmer profile stored locally
{
  "name": "Farmer name",
  "village": "Location",
  "landSize": 2.5,
  "soilType": "Loamy",
  "waterSource": "Well",
  "latitude": 20.5937,
  "longitude": 78.9629
}
```

---

## 12. Future Enhancements

### Phase 2: ML Integration
- [ ] Plant disease detection via TensorFlow Lite
- [ ] Crop yield prediction models
- [ ] Pest population forecasting

### Phase 3: Advanced Analytics
- [ ] Market price prediction
- [ ] Seasonal crop suitability maps
- [ ] Water stress prediction
- [ ] Soil health scoring

### Phase 4: Blockchain
- [ ] Farmer credit records
- [ ] Transparent supply chain
- [ ] Direct market access

---

## 13. Testing Public APIs

### Test Weather API
```bash
curl "https://api.open-meteo.com/v1/forecast?latitude=20.5937&longitude=78.9629&current=temperature_2m,relative_humidity_2m"
```

### Test Air Quality API
```bash
curl "https://air-quality-api.open-meteo.com/v1/air-quality?latitude=20.5937&longitude=78.9629&current=pm10,pm2_5,ozone,nitrogen_dioxide"
```

### Test data.gov.in
```
Visit: https://data.gov.in/
Search: "Agricultural Production"
Download: CSV/JSON format
```

---

## 14. Support & Resources

### Official Portals
- **data.gov.in**: https://data.gov.in/
- **IMD**: https://www.imd.gov.in/
- **CPCB**: https://www.cpcb.gov.in/
- **NFHS**: https://www.nfhsindia.org/

### Developer Resources
- **Open-Meteo Docs**: https://open-meteo.com/en/docs
- **Flutter HTTP**: https://pub.dev/packages/http
- **Dio Package**: https://pub.dev/packages/dio

---

**Built on Public Data for Public Good** 🌾

*All data sources are free, public, and government-verified*
