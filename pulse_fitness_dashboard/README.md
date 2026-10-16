# Pulse Fitness Dashboard

A responsive, static fitness dashboard intended for GitHub Pages. It includes daily steps, active calories, distance, heart-rate summaries, sleep duration, workout logging, goal editing, historical charts, JSON/CSV import and JSON export.

## Important: what this version does and does not do

- The dashboard initially displays **sample/demo data**, clearly labelled as such.
- Imported data is stored in the current browser's local storage. This static version does not upload health records to a server.
- It does **not** yet connect automatically to Apple Health, Health Connect, or Mi Fitness. A normal website cannot directly read the iPhone HealthKit database. Automatic integration needs native iOS/Android companion apps using the official permission APIs, and an additional secure sync design if data must reach the web dashboard.
- Redmi/Mi Fitness export and third-party sync capabilities depend on watch model, app version, phone, and region.
- Do not commit private health records, API keys, passwords, or OAuth secrets to a public repository.

## Deploy on GitHub Pages

1. Sign in to GitHub and create a new repository, e.g. `pulse-fitness-dashboard`.
2. Upload `index.html` and `README.md` to the repository's root.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Choose branch `main` and folder `/ (root)`, then save.
6. Wait for GitHub Pages to publish the site. Open the URL shown in the Pages settings.

GitHub Pages serves static files. It is suitable for this dashboard UI, but not by itself a private authenticated backend or a secure place for API secrets.

## Import data

Use **Import data**. JSON or CSV records need a date in `YYYY-MM-DD` format. Recognized field names include:

- `date` (required)
- `steps`
- `activeCalories` (or `active_calories`, `calories`)
- `distanceKm` (or `distance_km`, `distance`)
- `heartRate` (or `heart_rate`)
- `sleepHours` (or `sleep_hours`, `sleep`)
- `workouts` (JSON only; an array of objects with `type`, `durationMin`, and `calories`)

### JSON example

```json
{
  "records": [
    {
      "date": "2026-10-16",
      "steps": 7420,
      "activeCalories": 310,
      "distanceKm": 5.4,
      "heartRate": 72,
      "sleepHours": 7.2,
      "workouts": [
        {"type": "Walk", "durationMin": 30, "calories": 120}
      ]
    }
  ]
}
```

### CSV example

```csv
date,steps,activeCalories,distanceKm,heartRate,sleepHours
2026-10-16,7420,310,5.4,72,7.2
2026-10-15,6100,255,4.4,70,6.8
```

## Automatic sync roadmap

For a real automatic-sync product:

1. **iOS companion:** build a native iOS app with HealthKit capability and explicit per-category read permission. It can read permitted steps, active energy, walking/running distance, heart rate, sleep, and workouts where available.
2. **Android companion:** build a native Android app with Health Connect permissions for the available record types. The user must approve access.
3. **Mi Fitness / Redmi Watch:** check the exact model and app version for supported sync/export. Do not assume all watch fields flow into Apple Health or Health Connect.
4. **Secure sync:** if syncing across devices, use authenticated HTTPS endpoints, user-scoped access control, minimal retention, and a managed secret store. Never put a backend secret in `index.html`.
5. **Privacy:** provide a privacy policy, clear permission explanations, disconnect/delete controls, and data export.

This repository intentionally does not fake a connected state or request passwords for health accounts.
