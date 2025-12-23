# Gita Path: Verse & Wisdom
This app was developed for a client ,So code is not public 
Bhagavad Gita companion app built with Flutter. The shipped builds on Play Store and App Store contain the complete experience with the features below.

## Feature Highlights
- Ask Gita AI (rule-based): guided Q&A grounded in Gita verses with structured prompts and linked-reading handoffs; no open-ended LLM calls
- Onboarding and guarded navigation using Riverpod + GetX routes
- Email/phone auth with OTP, password reset, and social sign-in providers (Google/Apple)
- Home hub with Ask Gita, Read Gita, profile, feedback, streak, and subscription flows
- Firebase integration: Auth, Cloud Messaging, Crashlytics (uncaught error forwarding), FCM token bootstrap
- In-app updates (Android), in-app purchases/subscriptions with platform router
- Caching and storage via Dio client, shared preferences, and secure storage
- Localization with JSON assets (en, hi, kn, mr, ta, te) and ScreenUtil for adaptive layout
- Rich media helpers: cached network images, audio playback, text-to-speech, share, and image picker

## Distribution
- Google Play: [Play Store link here](https://play.google.com/store/apps/details?id=com.geeta.geeta_app)
- Apple App Store: [App Store link here](https://apps.apple.com/in/app/gitapath-verse-wisdom/id6754448724)
Client code is not included in this repo; server/admin code and credentials stay private.

## Tech Stack
- Flutter (Dart SDK ^3.9.2)
- State: Riverpod 3, GetX routing
- Networking: Dio
- Firebase: Core, Auth, Messaging, Crashlytics
- UX: ScreenUtil, Google Fonts, cached_network_image
- Native bridges: in_app_update, in_app_purchase (Android/iOS), permission_handler, image_picker
- Storage: shared_preferences, flutter_secure_storage

## Key Structure
- lib/main.dart: app bootstrap, Firebase init, Crashlytics wiring, orientation/status bar setup, route selection
- lib/routes/: route names and Get pages
- lib/core/: constants, colors/themes, Dio client, FCM services, purchase manager, exceptions
- lib/features/: onboarding, auth (login/register/otp/reset), home/main tabs, Ask Gita, Read Gita, profile/feedback, streak, subscription router
- lib/provider/: Riverpod providers for auth, profile, sessions, purchases, FCM, navigation, theme, daily content
- assets/: icons, images, localization JSONs

## Setup
1) Install Flutter (3.24+ recommended to pair with Dart 3.9) and run `flutter doctor`.
2) Install dependencies: `flutter pub get`.
3) Generate code (if you change json_serializable models): `dart run build_runner build --delete-conflicting-outputs`.
4) Configure Firebase:
	- Android: place `android/app/google-services.json` (already present) and ensure `com.geeta.geetaApp` matches your Firebase app id.
	- iOS: place `ios/Runner/GoogleService-Info.plist` and match bundle id; run `cd ios && pod install` after changes.
	- If you reconfigure, run `flutterfire configure` and regenerate `lib/firebase_options.dart`.
5) In-app purchases: set up products in Play Console/App Store and update entitlement/product ids in the subscription screens/providers.
6) In-app update (Android): requires Play Store distribution; call path already wired in `_checkForUpdate()`.
7) Notifications: configure FCM server keys for your backend and set APNs keys for iOS if using notifications.

## Running
- Debug: `flutter run`
- Target platform: `flutter run -d android` or `flutter run -d ios`
- Build release (Android): `flutter build appbundle`
- Build release (iOS): `flutter build ipa`

## Localization
- JSON files live in `assets/lang/` (en, hi, kn, mr, ta, te).
- To add a language, drop a new `<lang-code>.json` file and register it in `AppTranslation`.

## Testing
- Unit/widget tests: `flutter test`
- Consider adding integration tests for onboarding/auth flows, subscriptions, and notification handling.

## Troubleshooting
- If routing misbehaves after auth state changes, confirm `AppPrefs` flags (`is_logged_in`, token) are set before navigating.
- For build_runner conflicts, rerun with `--delete-conflicting-outputs`.
- For FCM issues, verify the token printed in logs and platform-specific notification permissions.
