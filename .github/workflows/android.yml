name: Build Android APK

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Set up JDK
      uses: actions/setup-java@v3
      with:
        distribution: 'zulu'
        java-version: '17'

    - name: Unzip Android project
      run: unzip invoice.zip -d appsrc

    - name: Build APK
      run: |
        cd appsrc/InvoiceApp
        ./gradlew assembleDebug

    - name: Upload APK Artifact
      uses: actions/upload-artifact@v3
      with:
        name: BabyFoodsInvoice-APK
        path: appsrc/InvoiceApp/app/build/outputs/apk/debug/*.apk
