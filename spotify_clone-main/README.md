# Spotify Clone 🎵

A modern and fully functional Spotify clone built with Flutter. This app leverages the power of various Flutter packages to provide a seamless music streaming experience with clean architecture principles.

![Flutter](https://img.shields.io/badge/Flutter-3.4.3+-02569B?logo=flutter)
![Dart](https://img.shields.io/badge/Dart-3.0+-0175C2?logo=dart)
![Firebase](https://img.shields.io/badge/Firebase-Enabled-FFCA28?logo=firebase)

## 📱 Features

- **User Authentication**: Secure user authentication using Firebase Authentication
- **State Management**: Efficient state management with Hydrated Bloc and Flutter Bloc
- **Audio Playback**: Smooth and responsive audio playback with Just Audio
- **Database Integration**: Real-time data synchronization using Cloud Firestore
- **Service Locator**: Easy dependency injection with Get It
- **Immutable State**: Use of Equatable and Dartz for robust and reliable state management
- **Theme Support**: Dark and light mode with persistent theme selection
- **Custom Icons**: Beautiful app icons with Flutter Launcher Icons
- **SVG Support**: Scalable vector graphics support using Flutter SVG
- **Favorite Songs**: Add/remove songs to favorites with real-time sync
- **Playlists**: Browse and play curated playlists
- **User Profiles**: View and manage user profiles

## 🏗️ Architecture

This project follows **Clean Architecture** principles:

```
├── lib/
│   ├── auth/           # Authentication gate
│   ├── common/         # Shared widgets, helpers, and BLoC
│   ├── core/           # Configs (theme, assets, constants)
│   ├── data/           # Models, repository implementations, data sources
│   ├── domain/         # Entities, repository interfaces, use cases
│   └── presentation/   # UI pages, BLoC, widgets
```

**Benefits:**
- Separation of concerns
- Testable code
- Maintainable and scalable
- Independent of frameworks

## 📦 Packages Used

| Package | Version | Purpose |
|---------|---------|---------|
| cupertino_icons | ^1.0.6 | iOS style icons |
| flutter_svg | latest | SVG rendering |
| hydrated_bloc | ^9.1.5 | Persistent state management |
| flutter_bloc | ^8.1.6 | State management |
| path_provider | ^2.1.3 | File system paths |
| flutterfire_cli | ^1.0.0 | Firebase CLI integration |
| firebase_core | ^3.2.0 | Firebase initialization |
| firebase_auth | ^5.1.2 | User authentication |
| get_it | ^7.7.0 | Dependency injection |
| dartz | ^0.10.1 | Functional programming |
| cloud_firestore | ^5.1.0 | Firestore database |
| just_audio | ^0.10.5 | Audio playback |
| equatable | ^2.0.5 | Value equality |
| flutter_launcher_icons | ^0.13.1 | App launcher icons |

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

1. **Flutter SDK** (3.4.3 or higher)
   ```bash
   flutter --version
   ```
   Download from: https://flutter.dev/docs/get-started/install

2. **Firebase Account**
   - Create a project at [Firebase Console](https://console.firebase.google.com)
   - Enable Authentication (Email/Password)
   - Enable Cloud Firestore
   - Add your app to the Firebase project (Android/iOS/Web)

3. **IDE** (choose one)
   - Android Studio with Flutter plugin
   - VS Code with Flutter extension
   - IntelliJ IDEA with Flutter plugin

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AlizaKhawar/MAD_Project.git
   cd MAD_Project/spotify_clone-main
   ```

2. **Install dependencies**
   ```bash
   flutter pub get
   ```

3. **Firebase Setup**
   
   Install FlutterFire CLI:
   ```bash
   dart pub global activate flutterfire_cli
   ```
   
   Configure Firebase for your project:
   ```bash
   flutterfire configure
   ```
   
   This will:
   - Create `firebase_options.dart` in your lib folder
   - Register your app with Firebase
   - Download the necessary configuration files

4. **Run the app**
   
   For development:
   ```bash
   flutter run
   ```
   
   For release build:
   ```bash
   # Android
   flutter build apk --release
   
   # iOS
   flutter build ios --release
   ```

### Troubleshooting

**Issue: Firebase configuration errors**
- Ensure `firebase_options.dart` exists in the `lib/` directory
- Re-run `flutterfire configure` if needed
- Check that your Firebase project has the correct platform enabled

**Issue: Build fails**
- Run `flutter clean` and then `flutter pub get`
- Check Flutter version: `flutter --version`
- Update Flutter: `flutter upgrade`

**Issue: Dependency conflicts**
- Delete `pubspec.lock`
- Run `flutter pub get` again

**Issue: Audio playback not working**
- Check device volume settings
- Ensure audio files/URLs are accessible
- Grant necessary permissions (Android)

## 🎨 Screenshots

| Splash Screen | Login | Home | Song Player |
|---------------|-------|------|-------------|
| ![Splash](flutter_01.png) | ![Login](flutter_02.png) | Coming soon | Coming soon |

## 🏃‍♂️ Running Tests

```bash
# Run all tests
flutter test

# Run tests with coverage
flutter test --coverage

# Run specific test file
flutter test test/widget_test.dart
```

## 📝 Project Structure

```
spotify_clone-main/
├── android/              # Android native code
├── ios/                  # iOS native code
├── lib/                  # Main application code
│   ├── auth/            # Authentication logic
│   ├── common/          # Shared components
│   ├── core/            # Core configurations
│   ├── data/            # Data layer (models, repos)
│   ├── domain/          # Domain layer (entities, use cases)
│   ├── presentation/    # UI layer (pages, widgets, BLoC)
│   └── main.dart        # Entry point
├── assets/              # Images, fonts, vectors
├── test/                # Test files
├── web/                 # Web-specific files
├── pubspec.yaml         # Dependencies
└── README.md            # This file
```

## 🤝 Contributing

We welcome contributions! Please see our [CONTRIBUTING.md](CONTRIBUTING.md) for details on:
- Setting up the development environment
- Coding standards and guidelines
- Submitting pull requests
- Project architecture details

### Quick Start for Contributors

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'feat: add some amazing feature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 🔧 Built With

- [Flutter](https://flutter.dev/) - UI framework
- [Firebase](https://firebase.google.com/) - Backend services
- [BLoC Pattern](https://bloclibrary.dev/) - State management
- [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) - Architecture pattern

## 📄 License

This project is available for educational purposes. Please check with the repository owner for specific licensing terms.

## 👥 Authors

- **Aliza Khawar** - [AlizaKhawar](https://github.com/AlizaKhawar)

## 🙏 Acknowledgments

- Flutter community for amazing packages
- Firebase for backend services
- Clean Architecture principles by Robert C. Martin

## 📧 Contact

For questions or suggestions, please open an issue on GitHub.

---

**Happy Coding! 🎵**
