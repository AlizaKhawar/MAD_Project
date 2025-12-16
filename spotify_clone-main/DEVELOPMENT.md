# Development Guide

This guide provides detailed information for developers working on the Spotify Clone project.

## Table of Contents

- [Environment Setup](#environment-setup)
- [Project Configuration](#project-configuration)
- [Development Workflow](#development-workflow)
- [Working with Features](#working-with-features)
- [Firebase Configuration](#firebase-configuration)
- [State Management](#state-management)
- [Common Tasks](#common-tasks)
- [Debugging](#debugging)
- [Performance](#performance)

## Environment Setup

### Required Tools

1. **Flutter SDK 3.4.3+**
   ```bash
   # Check version
   flutter --version
   
   # Update Flutter
   flutter upgrade
   ```

2. **Dart SDK** (comes with Flutter)

3. **IDE Setup**
   
   **For VS Code:**
   - Install Flutter extension
   - Install Dart extension
   - Configure settings.json:
     ```json
     {
       "dart.flutterSdkPath": "/path/to/flutter",
       "editor.formatOnSave": true,
       "editor.codeActionsOnSave": {
         "source.fixAll": true
       }
     }
     ```
   
   **For Android Studio:**
   - Install Flutter plugin
   - Install Dart plugin
   - Configure Flutter SDK path in settings

4. **Platform-Specific Requirements**
   
   **Android:**
   - Android Studio or Android SDK
   - JDK 11 or higher
   - Android SDK 33 or higher
   
   **iOS (macOS only):**
   - Xcode 14+
   - CocoaPods
   - iOS Simulator or physical device

### Initial Setup

```bash
# Clone repository
git clone https://github.com/AlizaKhawar/MAD_Project.git
cd MAD_Project/spotify_clone-main

# Get dependencies
flutter pub get

# Check for issues
flutter doctor -v

# Run code generation (if needed)
flutter pub run build_runner build --delete-conflicting-outputs
```

## Project Configuration

### Firebase Setup

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com)
   - Create a new project or select existing
   - Enable Authentication and Firestore

2. **Configure FlutterFire**
   ```bash
   # Install FlutterFire CLI
   dart pub global activate flutterfire_cli
   
   # Add to PATH if needed
   export PATH="$PATH":"$HOME/.pub-cache/bin"
   
   # Configure project
   flutterfire configure
   ```

3. **Firestore Rules** (for development)
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       // Songs collection
       match /Songs/{songId} {
         allow read: if true;
         allow write: if request.auth != null;
       }
       
       // Users collection
       match /Users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```

4. **Authentication Setup**
   - Enable Email/Password authentication in Firebase Console
   - Configure password requirements if needed

## Development Workflow

### Code Standards

1. **Formatting**
   ```bash
   # Format all files
   flutter format .
   
   # Format specific file
   flutter format lib/main.dart
   ```

2. **Linting**
   ```bash
   # Analyze code
   flutter analyze
   
   # Fix auto-fixable issues
   dart fix --apply
   ```

3. **Type Safety**
   - Use explicit types when not obvious
   - Avoid `dynamic` when possible
   - Use `const` constructors when possible

### Git Workflow

```bash
# Create feature branch
git checkout -b feature/new-feature

# Make changes and commit
git add .
git commit -m "feat: add new feature"

# Keep branch updated
git fetch origin
git rebase origin/main

# Push changes
git push origin feature/new-feature
```

### Commit Message Convention

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(auth): add password reset functionality
fix(player): resolve audio playback issue on iOS
docs(readme): update installation instructions
refactor(data): simplify repository pattern
```

## Working with Features

### Adding a New Feature

1. **Create Use Case** (domain layer)
   ```dart
   // lib/domain/usecases/feature/feature_usecase.dart
   import 'package:dartz/dartz.dart';
   import 'package:spotify/core/usecase/usecase.dart';
   
   class FeatureUseCase implements UseCase<ReturnType, Params> {
     @override
     Future<Either<Failure, ReturnType>> call({Params? params}) async {
       // Implementation
     }
   }
   ```

2. **Create Repository Interface** (domain layer)
   ```dart
   // lib/domain/repository/feature/feature_repository.dart
   import 'package:dartz/dartz.dart';
   
   abstract class FeatureRepository {
     Future<Either<Failure, ReturnType>> method();
   }
   ```

3. **Implement Repository** (data layer)
   ```dart
   // lib/data/repositoryimpl/feature/feature_repository_impl.dart
   class FeatureRepositoryImpl implements FeatureRepository {
     @override
     Future<Either<Failure, ReturnType>> method() async {
       // Implementation using data sources
     }
   }
   ```

4. **Create Data Source** (data layer)
   ```dart
   // lib/data/sources/feature/feature_service.dart
   abstract class FeatureService {
     Future<ReturnType> method();
   }
   
   class FeatureServiceImpl implements FeatureService {
     @override
     Future<ReturnType> method() async {
       // Firebase or API implementation
     }
   }
   ```

5. **Create BLoC/Cubit** (presentation layer)
   ```dart
   // lib/presentation/feature/bloc/feature_cubit.dart
   class FeatureCubit extends Cubit<FeatureState> {
     final FeatureUseCase useCase;
     
     FeatureCubit({required this.useCase}) : super(FeatureInitial());
     
     Future<void> loadData() async {
       emit(FeatureLoading());
       final result = await useCase.call();
       result.fold(
         (failure) => emit(FeatureError(message: failure.message)),
         (data) => emit(FeatureLoaded(data: data)),
       );
     }
   }
   ```

6. **Register Dependencies** (service locator)
   ```dart
   // lib/service_locater.dart
   sl.registerSingleton<FeatureService>(FeatureServiceImpl());
   sl.registerSingleton<FeatureRepository>(FeatureRepositoryImpl());
   sl.registerSingleton<FeatureUseCase>(FeatureUseCase());
   ```

7. **Create UI** (presentation layer)
   ```dart
   // lib/presentation/feature/pages/feature_page.dart
   class FeaturePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return BlocProvider(
         create: (_) => FeatureCubit(useCase: sl<FeatureUseCase>())..loadData(),
         child: BlocBuilder<FeatureCubit, FeatureState>(
           builder: (context, state) {
             // UI implementation
           },
         ),
       );
     }
   }
   ```

## Firebase Configuration

### Firestore Structure

```
firestore/
├── Songs/
│   └── {songId}
│       ├── title: string
│       ├── artist: string
│       ├── duration: string
│       ├── releaseDate: timestamp
│       └── ...
└── Users/
    └── {userId}
        ├── email: string
        ├── favoritesSongs: array
        └── ...
```

### Adding Firestore Collections

```dart
// Example: Add new collection
class NewCollectionService {
  final FirebaseFirestore _firestore = FirebaseFirestore.instance;
  
  Future<void> addDocument(Map<String, dynamic> data) async {
    await _firestore.collection('NewCollection').add(data);
  }
  
  Future<List<Model>> getDocuments() async {
    final snapshot = await _firestore.collection('NewCollection').get();
    return snapshot.docs.map((doc) => Model.fromJson(doc.data())).toList();
  }
}
```

## State Management

### BLoC Pattern

**When to use Cubit vs Bloc:**
- Use **Cubit** for simple state management
- Use **Bloc** when you need to track events

**State Classes:**
```dart
// Define states
abstract class FeatureState extends Equatable {
  @override
  List<Object?> get props => [];
}

class FeatureInitial extends FeatureState {}
class FeatureLoading extends FeatureState {}
class FeatureLoaded extends FeatureState {
  final Data data;
  FeatureLoaded({required this.data});
  
  @override
  List<Object?> get props => [data];
}
class FeatureError extends FeatureState {
  final String message;
  FeatureError({required this.message});
  
  @override
  List<Object?> get props => [message];
}
```

### Hydrated BLoC (Persistent State)

```dart
import 'package:hydrated_bloc/hydrated_bloc.dart';

class ThemeCubit extends HydratedCubit<ThemeMode> {
  ThemeCubit() : super(ThemeMode.system);
  
  void changeTheme(ThemeMode mode) => emit(mode);
  
  @override
  ThemeMode? fromJson(Map<String, dynamic> json) {
    return ThemeMode.values[json['theme'] as int];
  }
  
  @override
  Map<String, dynamic>? toJson(ThemeMode state) {
    return {'theme': state.index};
  }
}
```

## Common Tasks

### Adding a New Screen

1. Create page file in `lib/presentation/pages/`
2. Define route in navigation
3. Add necessary BLoC providers
4. Implement UI

### Adding Assets

1. Add files to `assets/` directory
2. Update `pubspec.yaml`:
   ```yaml
   flutter:
     assets:
       - assets/images/new_image.png
       - assets/vectors/new_icon.svg
   ```
3. Run `flutter pub get`
4. Access in code:
   ```dart
   Image.asset('assets/images/new_image.png')
   ```

### Updating Dependencies

```bash
# Check outdated packages
flutter pub outdated

# Update all packages
flutter pub upgrade

# Update specific package
flutter pub upgrade package_name
```

## Debugging

### Flutter DevTools

```bash
# Run app in debug mode
flutter run

# Open DevTools
flutter pub global activate devtools
flutter pub global run devtools
```

### Common Debug Commands

```bash
# Hot reload
# Press 'r' in terminal or use IDE shortcut

# Hot restart
# Press 'R' in terminal

# Clear build cache
flutter clean

# Rebuild
flutter pub get
flutter run
```

### Logging

```dart
import 'dart:developer' as developer;

// Simple logging
print('Debug message');

// Better logging
developer.log('Message', name: 'FeatureName');

// With error
developer.log(
  'Error occurred',
  name: 'FeatureName',
  error: error,
  stackTrace: stackTrace,
);
```

## Performance

### Best Practices

1. **Use const constructors**
   ```dart
   const Text('Hello')  // Better
   Text('Hello')        // Rebuilds unnecessarily
   ```

2. **Avoid rebuilding entire widget tree**
   ```dart
   // Good: Only rebuild what changed
   BlocBuilder<FeatureCubit, FeatureState>(
     builder: (context, state) => Text(state.data)
   )
   ```

3. **Lazy load images**
   ```dart
   FadeInImage.assetNetwork(
     placeholder: 'assets/loading.gif',
     image: imageUrl,
   )
   ```

4. **Cache network images**
   - Consider using `cached_network_image` package

5. **Profile performance**
   ```bash
   flutter run --profile
   ```

### Memory Management

- Dispose controllers and streams
- Cancel subscriptions in dispose()
- Use weak references when appropriate

```dart
@override
void dispose() {
  _controller.dispose();
  _subscription.cancel();
  super.dispose();
}
```

## Additional Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [BLoC Library](https://bloclibrary.dev)
- [Firebase for Flutter](https://firebase.flutter.dev)
- [Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

---

Happy coding! If you have questions, open an issue or reach out to the maintainers.
