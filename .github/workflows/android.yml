name: Build Android APK

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '11'

      - name: Setup Android SDK
        uses: android-actions/setup-android@v2
        with:
          api-level: 33
          build-tools: 33.0.2

      - name: Unzip uploaded project
        run: unzip -q invoice.zip -d appsrc

      - name: Make gradlew executable
        run: chmod +x appsrc/InvoiceApp/gradlew

      - name: Build debug APK
        run: cd appsrc/InvoiceApp && ./gradlew assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: android-apk
          path: appsrc/InvoiceApp/app/build/outputs/apk/debug/*.apk
