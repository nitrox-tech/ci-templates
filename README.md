# CI Templates

This repository contains CI/CD templates for building Android and iOS applications.

## Overview

This project provides reusable CI/CD pipeline templates that can be used across different mobile application projects to automate the build, test, and deployment processes.

## Features

- **Android Build Templates**: Automated Android app building and testing
- **iOS Build Templates**: Automated iOS app building and testing
- **Cross-platform Support**: Templates for React Native, Flutter, and native projects
- **Multiple CI Platforms**: Support for GitHub Actions, GitLab CI, and other CI/CD platforms

## Supported Platforms

- Android (Java/Kotlin)
- iOS (Swift/Objective-C)
- React Native
- Flutter
- Xamarin

## CI/CD Platforms

- GitHub Actions
- GitLab CI/CD
- Jenkins
- Bitrise
- CircleCI

## Getting Started

1. Clone this repository
2. Choose the appropriate template for your project
3. Copy the template files to your project
4. Customize the configuration according to your project needs
5. Set up the required environment variables and secrets

## Templates Structure

```
├── android/
│   ├── github-actions/
│   ├── gitlab-ci/
│   └── jenkins/
├── ios/
│   ├── github-actions/
│   ├── gitlab-ci/
│   └── jenkins/
├── react-native/
│   ├── github-actions/
│   └── gitlab-ci/
├── flutter/
│   ├── github-actions/
│   └── gitlab-ci/
└── shared/
    ├── scripts/
    └── configs/
```

## Usage

### Android Projects

For Android projects, use the templates in the `android/` directory:

```bash
# Copy GitHub Actions template
cp android/github-actions/.github/workflows/android-ci.yml .github/workflows/
```

### iOS Projects

For iOS projects, use the templates in the `ios/` directory:

```bash
# Copy GitHub Actions template
cp ios/github-actions/.github/workflows/ios-ci.yml .github/workflows/
```

### React Native Projects

For React Native projects, use the templates in the `react-native/` directory:

```bash
# Copy GitHub Actions template
cp react-native/github-actions/.github/workflows/react-native-ci.yml .github/workflows/
```

### Flutter Projects

For Flutter projects, use the templates in the `flutter/` directory:

```bash
# Copy GitHub Actions template
cp flutter/github-actions/.github/workflows/flutter-ci.yml .github/workflows/
```

## Configuration

Each template includes configuration files that need to be customized:

- Environment variables
- Build configurations
- Test configurations
- Deployment settings

## Requirements

- Node.js (for React Native projects)
- Flutter SDK (for Flutter projects)
- Android SDK (for Android projects)
- Xcode (for iOS projects)
- Appropriate CI/CD platform access

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the templates
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For questions and support, please open an issue in this repository or contact the development team.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes and updates.
