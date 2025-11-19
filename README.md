name: Build Android APK

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '11'

      - name: Install Android SDK
        uses: android-actions/setup-android@v2

      - name: Unzip project
        run: unzip invoice.zip -d appsrc

      - name: Make gradlew executable
        run: chmod +x appsrc/InvoiceApp/gradlew || true

      - name: Build APK
        run: |
          cd appsrc/InvoiceApp
          ./gradlew assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: Invoice-APK
          path: appsrc/InvoiceApp/app/build/outputs/apk/debug/*.apk
