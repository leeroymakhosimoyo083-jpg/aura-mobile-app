name: Build Android APK

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 🏗 Checkout repo
        uses: actions/checkout@v3

      - name: 🟢 Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: 📦 Install Expo CLI & Dependencies
        run: |
          npm install -g eas-cli
          npm install

      - name: 🚀 Build APK via EAS
        env:
          EXPO_TOKEN: ${{ secrets.EXPO_TOKEN }}
        run: |
          eas build --platform android --profile preview --non-interactive
