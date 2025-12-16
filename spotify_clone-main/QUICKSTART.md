# Quick Start Guide

Get up and running with Spotify Clone in 5 minutes! ⚡

## Prerequisites Checklist

- [ ] Flutter SDK 3.4.3+ installed
- [ ] Git installed
- [ ] Firebase account created
- [ ] Code editor (VS Code or Android Studio)

## 5-Minute Setup

### Step 1: Clone & Install (1 min)

```bash
# Clone the repository
git clone https://github.com/AlizaKhawar/MAD_Project.git
cd MAD_Project/spotify_clone-main

# Install dependencies
flutter pub get
```

### Step 2: Firebase Setup (2 min)

```bash
# Install FlutterFire CLI
dart pub global activate flutterfire_cli

# Configure Firebase (follow the prompts)
flutterfire configure
```

**What this does:**
- Creates `firebase_options.dart` automatically
- Connects your app to Firebase
- Downloads configuration files

### Step 3: Enable Firebase Services (1 min)

Go to [Firebase Console](https://console.firebase.google.com):

1. Select your project
2. Go to **Authentication** → **Sign-in method**
3. Enable **Email/Password**
4. Go to **Firestore Database** → **Create database**
5. Start in **test mode** (for development)

### Step 4: Run the App (1 min)

```bash
# Check everything is ready
flutter doctor

# Run the app
flutter run
```

## What's Next?

### First Time Contributors

1. **Read the docs:**
   - [CONTRIBUTING.md](CONTRIBUTING.md) - How to contribute
   - [DEVELOPMENT.md](DEVELOPMENT.md) - Development guidelines
   - [README.md](README.md) - Project overview

2. **Explore the code:**
   ```
   lib/
   ├── presentation/  # Start here - UI code
   ├── domain/        # Business logic
   └── data/          # Data layer
   ```

3. **Make your first change:**
   - Pick an issue labeled `good first issue`
   - Create a branch: `git checkout -b feature/my-feature`
   - Make changes and test
   - Submit a PR!

### Common First Tasks

**Easy:**
- Add new theme colors
- Update UI text/labels
- Add new assets (images, icons)
- Improve documentation

**Medium:**
- Add new widget components
- Implement new screen layouts
- Add validation to forms

**Advanced:**
- Add new features (playlist management, search)
- Optimize performance
- Add comprehensive tests

## Quick Commands

```bash
# Format code
flutter format .

# Check for issues
flutter analyze

# Run tests
flutter test

# Clean build
flutter clean && flutter pub get

# Hot reload (while app is running)
# Press 'r' in terminal

# Hot restart (while app is running)
# Press 'R' in terminal
```

## Troubleshooting Quick Fixes

### "Flutter not found"
```bash
# Add Flutter to PATH
export PATH="$PATH:/path/to/flutter/bin"
```

### "Firebase error"
```bash
# Reconfigure Firebase
flutterfire configure --force
```

### "Build failed"
```bash
# Clean and rebuild
flutter clean
flutter pub get
flutter run
```

### "Package conflicts"
```bash
# Delete lock file and reinstall
rm pubspec.lock
flutter pub get
```

## Getting Help

- **Issues:** Found a bug? [Open an issue](https://github.com/AlizaKhawar/MAD_Project/issues)
- **Questions:** Not sure about something? Check [CONTRIBUTING.md](CONTRIBUTING.md)
- **Docs:** Need details? Read [DEVELOPMENT.md](DEVELOPMENT.md)

## Project Structure Quick Reference

```
spotify_clone-main/
├── lib/
│   ├── main.dart              # App entry point
│   ├── auth/                  # Auth logic
│   ├── common/                # Shared widgets
│   ├── core/                  # Config & theme
│   ├── data/                  # Data layer
│   ├── domain/                # Business logic
│   └── presentation/          # UI layer
├── assets/                    # Images, fonts, SVGs
├── test/                      # Tests
└── pubspec.yaml              # Dependencies
```

## Development Tips

1. **Use hot reload** - Speeds up development significantly
2. **Check Flutter doctor** - `flutter doctor -v` for diagnostics
3. **Read error messages** - They're usually helpful!
4. **Use const constructors** - Better performance
5. **Follow the architecture** - Keep layers separated

## Resources

- 📚 [Flutter Docs](https://flutter.dev/docs)
- 🔥 [Firebase Docs](https://firebase.google.com/docs)
- 🎨 [BLoC Pattern](https://bloclibrary.dev)
- 🏗️ [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

---

**Ready to contribute? Start coding! 🚀**

For detailed information, see:
- [README.md](README.md) - Project overview
- [CONTRIBUTING.md](CONTRIBUTING.md) - Contribution guidelines
- [DEVELOPMENT.md](DEVELOPMENT.md) - Development guide
