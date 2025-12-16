# Contributing to Spotify Clone

Thank you for your interest in contributing to our Spotify Clone project! This guide will help you get started with contributing to this Flutter application.

## Table of Contents

- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Architecture](#project-architecture)
- [Coding Guidelines](#coding-guidelines)
- [Making Changes](#making-changes)
- [Testing](#testing)
- [Submitting Changes](#submitting-changes)

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

1. **Flutter SDK** (version 3.4.3 or higher)
   - Download from: https://flutter.dev/docs/get-started/install
   - Verify installation: `flutter --version`

2. **Dart SDK** (comes with Flutter)

3. **Firebase Account**
   - Create a project at: https://console.firebase.google.com
   - Enable Authentication and Cloud Firestore

4. **IDE** (choose one):
   - Android Studio with Flutter plugin
   - VS Code with Flutter extension
   - IntelliJ IDEA with Flutter plugin

5. **Git**
   - For version control

### Development Setup

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
   - Install FlutterFire CLI:
     ```bash
     dart pub global activate flutterfire_cli
     ```
   - Configure Firebase for your project:
     ```bash
     flutterfire configure
     ```
   - This will create/update `firebase_options.dart` with your Firebase configuration

4. **Run the app**
   ```bash
   flutter run
   ```

## Project Architecture

This project follows **Clean Architecture** principles with a clear separation of concerns:

```
lib/
├── auth/                  # Authentication gate
├── common/                # Shared components
│   ├── bloc/             # Shared BLoC states
│   ├── helpers/          # Helper functions
│   └── widgets/          # Reusable widgets
├── core/                  # Core configurations
│   ├── configs/          # Theme, assets, constants
│   └── usecase/          # Base use case classes
├── data/                  # Data layer
│   ├── models/           # Data models
│   ├── repositoryimpl/   # Repository implementations
│   └── sources/          # Data sources (Firebase)
├── domain/                # Domain layer
│   ├── entities/         # Business entities
│   ├── repository/       # Repository interfaces
│   └── usecases/         # Business logic use cases
└── presentation/          # Presentation layer
    ├── choose_mode/      # Theme selection
    ├── pages/            # App pages/screens
    └── song_player/      # Music player feature
```

### Architecture Principles

- **Separation of Concerns**: Each layer has a specific responsibility
- **Dependency Rule**: Dependencies point inward (presentation → domain ← data)
- **Clean Code**: Readable, maintainable, and testable code
- **State Management**: Uses BLoC pattern with hydrated_bloc for persistence

## Coding Guidelines

### General Guidelines

1. **Follow Dart conventions**
   - Use `lowerCamelCase` for variables and methods
   - Use `UpperCamelCase` for classes
   - Use `lowercase_with_underscores` for file names

2. **Code Style**
   - Run `flutter analyze` before committing
   - Follow the lint rules defined in `analysis_options.yaml`
   - Format code: `flutter format .`

3. **Naming Conventions**
   - Use descriptive names for variables and functions
   - Suffix BLoC classes with `Cubit` or `Bloc`
   - Suffix state classes with `State`
   - Suffix use cases with `UseCase`

### Widget Guidelines

1. **Prefer StatelessWidget** over StatefulWidget when state management is handled by BLoC
2. **Extract reusable widgets** to `common/widgets/`
3. **Use const constructors** when possible for performance
4. **Keep widgets small** - break down complex widgets into smaller components

### State Management

1. **Use BLoC/Cubit** for state management
2. **Use HydratedBloc** for persistent state
3. **Keep business logic in use cases**, not in BLoC
4. **Emit immutable states** using Equatable

### Firebase Integration

1. **Use repositories** to abstract Firebase operations
2. **Handle errors properly** with try-catch and Either from dartz
3. **Don't expose Firebase directly** to presentation layer

## Making Changes

### Before You Start

1. **Check existing issues** - avoid duplicate work
2. **Create an issue** if one doesn't exist
3. **Discuss major changes** before implementing

### Development Workflow

1. **Create a new branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**
   - Write clean, documented code
   - Follow the coding guidelines
   - Test your changes

3. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add your feature description"
   ```

   Commit message format:
   - `feat:` for new features
   - `fix:` for bug fixes
   - `docs:` for documentation
   - `style:` for formatting changes
   - `refactor:` for code refactoring
   - `test:` for adding tests
   - `chore:` for maintenance tasks

4. **Keep your branch updated**
   ```bash
   git fetch origin
   git rebase origin/main
   ```

## Testing

### Running Tests

```bash
# Run all tests
flutter test

# Run tests with coverage
flutter test --coverage
```

### Writing Tests

1. **Unit tests** for use cases and business logic
2. **Widget tests** for UI components
3. **Integration tests** for complete user flows

Place tests in the `test/` directory mirroring the `lib/` structure.

## Submitting Changes

### Pull Request Process

1. **Ensure your code**:
   - Passes all tests: `flutter test`
   - Has no analysis issues: `flutter analyze`
   - Is properly formatted: `flutter format .`

2. **Push your branch**
   ```bash
   git push origin feature/your-feature-name
   ```

3. **Create a Pull Request**
   - Provide a clear title and description
   - Reference any related issues
   - Include screenshots for UI changes
   - Wait for code review

4. **Address feedback**
   - Respond to review comments
   - Make requested changes
   - Push updates to the same branch

### PR Guidelines

- Keep PRs focused and small
- Write clear commit messages
- Update documentation if needed
- Add tests for new features
- Ensure backward compatibility

## Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Help others learn and grow
- Keep discussions professional

## Need Help?

- Open an issue for questions
- Check existing documentation
- Review closed PRs for examples

Thank you for contributing to Spotify Clone! 🎵
