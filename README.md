# Flutter CI/CD Templates

Thư viện GitHub Actions cung cấp Reusable Workflow để chuẩn hóa quy trình build Flutter cho Android và iOS, giảm thiểu sự lặp lại code trong các dự án.

## 🚀 Tính Năng

- ✅ Build Android APK và App Bundle
- ✅ Build iOS IPA
- ✅ Tự động setup certificates và keystore
- ✅ Chạy tests trước khi build
- ✅ Upload artifacts với retention tùy chỉnh
- ✅ Support multiple entry points (main_dev.dart, main_prod.dart)

## 📁 Cấu Trúc Project

```
├── .github/workflows/
│   └── build-flutter-app.yml    # Reusable workflow chính
├── examples/
│   ├── flutter-ci-example.yml  # Ví dụ sử dụng
│   └── import-guide.md         # Hướng dẫn chi tiết
└── README.md
```

## 🛠️ Cách Sử Dụng

### Bước 1: Tạo File CI/CD trong Project Flutter

Tạo file `.github/workflows/ci.yml`:

```yaml
name: Flutter App CI/CD Pipeline

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main" ]

jobs:
  # Build Android Release
  build_android:
    name: Build Android App
    uses: nitrox-tech/ci-templates/.github/workflows/build-flutter-app.yml@main
    with:
      os: ubuntu-latest
      platform: android
      build_target: lib/main_prod.dart
      artifact_retention_days: 14
    secrets:
      KEYSTORE_BASE64: ${{ secrets.KEYSTORE_BASE64 }}
      KEY_PROPERTIES: ${{ secrets.KEY_PROPERTIES }}

  # Build iOS Release
  build_ios:
    name: Build iOS App
    uses: nitrox-tech/ci-templates/.github/workflows/build-flutter-app.yml@main
    with:
      os: macos-latest
      platform: ios
      build_target: lib/main_prod.dart
      artifact_retention_days: 14
    secrets:
      P12_BASE64: ${{ secrets.P12_BASE64 }}
      PROVISIONING_PROFILE: ${{ secrets.PROVISIONING_PROFILE }}
      P12_PASSWORD: ${{ secrets.P12_PASSWORD }}
```

### Bước 2: Setup GitHub Secrets

#### Cho Android:
| Secret Name | Mô tả | Cách tạo |
|-------------|-------|----------|
| `KEYSTORE_BASE64` | File keystore đã encode base64 | `base64 -i your-keystore.jks` |
| `KEY_PROPERTIES` | Nội dung file key.properties | Copy nội dung file |

#### Cho iOS:
| Secret Name | Mô tả | Cách tạo |
|-------------|-------|----------|
| `P12_BASE64` | File certificate .p12 đã encode base64 | `base64 -i certificate.p12` |
| `PROVISIONING_PROFILE` | File provisioning profile đã encode base64 | `base64 -i profile.mobileprovision` |
| `P12_PASSWORD` | Mật khẩu file .p12 | Nhập mật khẩu |

### Bước 3: Tạo File key.properties (Android)

Tạo file `android/key.properties`:

```properties
storePassword=your_store_password
keyPassword=your_key_password
keyAlias=your_key_alias
storeFile=../app/keystore.jks
```

## 📖 Hướng Dẫn Chi Tiết

Xem file [import-guide.md](examples/import-guide.md) để có hướng dẫn đầy đủ về:
- Cách setup Android keystore
- Cách setup iOS certificates
- Troubleshooting các lỗi thường gặp
- Cấu hình build.gradle

## 🔧 Parameters

| Parameter | Mô tả | Mặc định |
|-----------|-------|----------|
| `os` | Operating system (ubuntu-latest/macos-latest) | ubuntu-latest |
| `platform` | Platform to build (android/ios) | - |
| `build_target` | Main entry point file | lib/main.dart |
| `artifact_retention_days` | Số ngày giữ artifacts | 7 |
| `build_apk` | Build APK file (Android only) | true |
| `build_aab` | Build App Bundle file (Android only) | true |

## 📝 Ví Dụ Sử Dụng

Xem file [flutter-ci-example.yml](examples/flutter-ci-example.yml) để có ví dụ đầy đủ về cách sử dụng workflow.

## 🤝 Contributing

1. Fork repository
2. Tạo feature branch
3. Commit changes
4. Push và tạo Pull Request

## 📄 License

MIT License - xem file LICENSE để biết thêm chi tiết.