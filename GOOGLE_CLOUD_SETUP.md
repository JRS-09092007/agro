# Google Cloud Integration Setup Guide

## Overview

KrishiMitra now integrates with Google Cloud services for real AI capabilities and multilingual voice support:

- **Gemini API**: Real AI responses powered by Google's advanced LLM
- **Cloud Speech-to-Text**: Voice input in all 6 Indian languages
- **Cloud Text-to-Speech**: Voice output in all 6 Indian languages
- **Translation API**: Real-time translation support

---

## Prerequisites

- Google Cloud Project
- Billing enabled on Google Cloud
- Flutter development environment

---

## Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click "Create Project"
3. Enter project name: "KrishiMitra"
4. Click "Create"
5. Wait for project to be created
6. Select the new project from the dropdown

---

## Step 2: Enable Required APIs

In the Google Cloud Console, enable these APIs:

### Enable Gemini API
1. Search for "Generative AI API" or "Gemini API"
2. Click on result
3. Click "Enable"

### Enable Speech-to-Text API
1. Search for "Cloud Speech-to-Text API"
2. Click on result
3. Click "Enable"

### Enable Text-to-Speech API
1. Search for "Cloud Text-to-Speech API"
2. Click on result
3. Click "Enable"

### Enable Translation API (Optional)
1. Search for "Cloud Translation API"
2. Click on result
3. Click "Enable"

---

## Step 3: Create API Keys

### Create Gemini API Key
1. Go to "APIs & Services" > "Credentials"
2. Click "Create Credentials" > "API Key"
3. Copy the API key
4. (Optional but recommended) Click the pencil icon to restrict the key:
   - Application restrictions: Android apps / iOS apps
   - API restrictions: Select "Generative AI API"
5. Save the key somewhere safe

### Create Service Account for Speech/Text Services
1. Go to "APIs & Services" > "Credentials"
2. Click "Create Credentials" > "Service Account"
3. Enter name: "krishi-mitra-voice"
4. Click "Create and Continue"
5. Grant role: "Editor"
6. Click "Continue" > "Done"
7. Click on the created service account
8. Go to "Keys" tab > "Add Key" > "Create new key"
9. Select "JSON"
10. Click "Create"
11. A JSON file will download - keep it safe

---

## Step 4: Add API Keys to Flutter App

### For Gemini API (Dart/Flutter)

Create a file `lib/config/api_keys.dart`:

```dart
class ApiKeys {
  static const String geminiApiKey = 'YOUR_GEMINI_API_KEY_HERE';
  // Replace with your actual API key from Step 3
}
```

Update `lib/screens/ai_chat_screen.dart`:

```dart
void _initializeServices() {
  _geminiService = GeminiAIService(apiKey: ApiKeys.geminiApiKey);
  _voiceService = VoiceService();
}
```

### For Speech Services (Android/iOS specific)

#### Android Setup:
1. Add to `android/app/build.gradle`:
```gradle
dependencies {
    implementation 'com.google.cloud:google-cloud-speech:2.2.0'
}
```

2. Add to `android/app/src/main/AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET" />
```

#### iOS Setup:
1. Add to `ios/Podfile`:
```ruby
pod 'GoogleCloudSpeech'
```

2. Add to `ios/Runner/Info.plist`:
```xml
<key>NSMicrophoneUsageDescription</key>
<string>KrishiMitra needs microphone access for voice input</string>
<key>NSSpeechRecognitionUsageDescription</key>
<string>KrishiMitra needs speech recognition for voice farming assistance</string>
```

3. Run `flutter pub get` and `cd ios && pod install && cd ..`

---

## Step 5: Configure Dependencies

The pubspec.yaml already includes required packages:

```yaml
google_generative_ai: ^0.4.0
speech_to_text: ^6.1.0
flutter_tts: ^0.6.1
google_cloud_speech: ^1.0.0
```

Run:
```bash
flutter pub get
```

---

## Step 6: Test the Integration

### Test Gemini AI:
1. Open app
2. Register farmer profile
3. Go to Dashboard > AI Assistant
4. Type a farming question
5. See Gemini-powered response in your language

### Test Voice Input:
1. In AI Chat, tap microphone icon
2. Speak a farming question in your language
3. Message auto-fills with recognized text
4. Tap send to get AI response

### Test Voice Output:
1. AI response auto-plays in your language
2. Tap response message to play again
3. Tap speaker icon to control volume

---

## Cost Estimation

**Free Tier Benefits:**
- Gemini API: 60 requests per minute (free tier)
- Speech-to-Text: 60 minutes per month (free)
- Text-to-Speech: 1 million characters per month (free)
- Translation: 500,000 characters per month (free)

**Expected Monthly Cost** (with 100 daily users):
- Gemini API: ~$5-10
- Speech-to-Text: ~$2-5
- Text-to-Speech: ~$5-10
- Translation: ~$0-2
- **Total: ~$12-27/month**

---

## Troubleshooting

### "API Key Invalid" Error
- Check that you copied the full API key correctly
- Verify the API is enabled in Google Cloud Console
- Ensure billing is enabled on the project

### Speech Recognition Not Working
- Check microphone permissions on device
- Verify Speech-to-Text API is enabled
- Check device language matches selected language

### Voice Output Not Playing
- Check device volume is not muted
- Verify Text-to-Speech API is enabled
- Check supported languages match device

### Gemini API Timeout
- Check internet connection
- Verify API quota hasn't been exceeded
- Try again in a few moments

---

## Language Support

### Fully Supported (All 6 Indian Languages):
- **English** (en-US)
- **Hindi** (hi-IN)
- **Marathi** (mr-IN)
- **Telugu** (te-IN)
- **Tamil** (ta-IN)
- **Kannada** (kn-IN)

All languages supported for:
- Gemini AI responses
- Speech-to-Text input
- Text-to-Speech output
- Translation (if needed)

---

## Best Practices

1. **Secure API Keys**
   - Never commit API keys to GitHub
   - Use environment variables in production
   - Rotate keys regularly

2. **Rate Limiting**
   - Implement request throttling
   - Cache responses when possible
   - Monitor API usage in Cloud Console

3. **Error Handling**
   - Always provide fallback responses
   - Log errors for debugging
   - Show user-friendly error messages

4. **Offline Support**
   - Cache recent responses
   - Detect connectivity
   - Use fallback responses when offline

---

## Production Deployment

For App Store/Play Store release:

1. **Use Application Restrictions**
   - Set API key to specific app package names
   - Restrict to Android/iOS as appropriate

2. **Use Service Accounts**
   - Create service account for backend operations
   - Download JSON key
   - Secure in backend infrastructure

3. **Set Up Usage Alerts**
   - Go to Billing > Budgets & alerts
   - Set monthly budget limit
   - Get notified if usage exceeds threshold

4. **Monitor Usage**
   - Use Cloud Console dashboard
   - Review API usage metrics
   - Optimize inefficient queries

---

## Additional Resources

- [Gemini API Documentation](https://ai.google.dev/tutorials/python_quickstart)
- [Cloud Speech-to-Text Docs](https://cloud.google.com/speech-to-text/docs)
- [Cloud Text-to-Speech Docs](https://cloud.google.com/text-to-speech/docs)
- [Flutter Google Generative AI](https://pub.dev/packages/google_generative_ai)
- [Speech to Text Flutter](https://pub.dev/packages/speech_to_text)

---

## Support

For issues with:
- **Flutter packages**: Check pub.dev documentation
- **Google Cloud APIs**: Visit [Google Cloud Support](https://cloud.google.com/support)
- **KrishiMitra app**: Check project documentation

