# Municipal Budget Intelligence & Outcome Recommendation System

The existing dashboard has been extended with a local, browser-based Random Forest Regression workflow, analytical recommendations, scenario simulation, anomaly detection, CSV import, PWA support and mobile/desktop wrapper configuration.

## Run locally

Open `DASHBOARD/index.html` through a local static server (for example `npm run serve` after `npm install`). A server is required for service-worker installation; core dashboard analysis still works without an internet connection once cached.

## Data and methodology

The dashboard keeps `DASHBOARD/data.js` unchanged as its source dataset. The model trains only on rows with complete required features and a real outcome-improvement target. Missing values are not treated as zero. It uses an 80/20 reproducible split, reports R²/MAE/RMSE where enough records are available, and runs K-fold CV when feasible. Feature importance comes from impurity reduction across randomized decision trees and is explicitly non-causal.

Recommendations are separate, transparent analytical rules that combine utilization, ML prediction, per-capita spending, historical sector context and over-budget status. Isolation Forest results identify statistical anomalies, never fraud.

## CSV import

CSV processing is entirely local. The importer validates required high-level fields, reports missing fields, and offers either adding records for retraining or using the first valid row as a scenario. It does not overwrite the supplied source data.

## Builds

- Android: `npm install`, `npx cap add android`, `npm run android:sync`, then build APK/AAB in Android Studio.
- Windows: install Rust and Tauri system prerequisites, then `npm install` and `npm run windows:build`; this generates the NSIS `.exe` installer.

The shared dashboard files, data and ML code are used by browser/PWA, Capacitor and Tauri targets.
