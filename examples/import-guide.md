# Hướng Dẫn Import Flutter CI Template

## Bước 1: Copy File Workflow

Copy file `.github/workflows/build-flutter-app.yml` từ repository này vào project Flutter của bạn.

## Bước 2: Tạo File CI/CD trong Project

Tạo file `.github/workflows/ci.yml` trong project Flutter của bạn với nội dung:

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

## Bước 3: Setup GitHub Secrets

### Cho Android:
1. Vào Settings > Secrets and variables > Actions
2. Thêm các secrets sau:

| Secret Name | Mô tả | Cách tạo |
|-------------|-------|----------|
| `KEYSTORE_BASE64` | File keystore đã encode base64 | `base64 -i your-keystore.jks` |
| `KEY_PROPERTIES` | Nội dung file key.properties | Copy nội dung file key.properties |

### Cho iOS:
1. Thêm các secrets sau:

| Secret Name | Mô tả | Cách tạo |
|-------------|-------|----------|
| `P12_BASE64` | File certificate .p12 đã encode base64 | `base64 -i certificate.p12` |
| `PROVISIONING_PROFILE` | File provisioning profile đã encode base64 | `base64 -i profile.mobileprovision` |
| `P12_PASSWORD` | Mật khẩu file .p12 | Nhập mật khẩu |

## Bước 4: Tạo File key.properties (Android)

Tạo file `android/key.properties` trong project Flutter:

```properties
storePassword=your_store_password
keyPassword=your_key_password
keyAlias=your_key_alias
storeFile=../app/keystore.jks
```

## Bước 5: Cập nhật build.gradle (Android)

Thêm vào `android/app/build.gradle`:

```gradle
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android {
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
            storePassword keystoreProperties['storePassword']
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```

## Bước 6: Test Workflow

1. Push code lên branch `main` hoặc `develop`
2. Kiểm tra tab Actions trong GitHub
3. Download artifacts từ build thành công

## Troubleshooting

### Lỗi thường gặp:

1. **Android build fail**: Kiểm tra file key.properties và keystore
2. **iOS build fail**: Kiểm tra certificate và provisioning profile
3. **Flutter version**: Đảm bảo Flutter version trong project tương thích

### Debug:

- Xem logs trong GitHub Actions
- Kiểm tra secrets đã được set đúng chưa
- Test build local trước khi push
