# QHXD Hà Nội - Deep Link Domain

This repository hosts the deep link redirect page for the QHXD Hà Nội mobile application.

## What's This?

When users share planning information from the app, they'll get a link like:
```
https://ngochuy2002.github.io/qhxh_hanoi_domain/planning?objectid=4742
```

This link:
- ✅ Is clickable in all messaging apps (WhatsApp, Messenger, SMS, etc.)
- ✅ Opens the QHXD Hà Nội app if installed
- ✅ Shows a download page if the app is not installed
- ✅ Works on both Android and iOS

## Files

- `index.html` - The redirect/fallback page
- `.well-known/assetlinks.json` - Android App Links configuration
- `.well-known/apple-app-site-association` - iOS Universal Links configuration

## Setup Instructions

### 1. Enable GitHub Pages

1. Go to repository Settings
2. Navigate to Pages (left sidebar)
3. Under "Source", select:
   - Branch: **main**
   - Folder: **/ (root)**
4. Click Save
5. Wait ~1 minute for deployment

### 2. Update Package Name (if needed)

If your app's package name is different from `com.example.qhxd_hanoi`, update:

**File: `.well-known/assetlinks.json`**
```json
{
  "package_name": "YOUR_ACTUAL_PACKAGE_NAME"
}
```

**File: `.well-known/apple-app-site-association`**
```json
{
  "appID": "YOUR_TEAM_ID.YOUR_BUNDLE_ID"
}
```

### 3. Verify Setup

After GitHub Pages is enabled, verify these URLs work:

1. **Main page:** https://ngochuy2002.github.io/qhxh_hanoi_domain/
2. **Android config:** https://ngochuy2002.github.io/qhxh_hanoi_domain/.well-known/assetlinks.json
3. **iOS config:** https://ngochuy2002.github.io/qhxh_hanoi_domain/.well-known/apple-app-site-association

All should load without 404 errors.

## Testing

### Android
```bash
# Test the deep link
adb shell am start -W -a android.intent.action.VIEW \
  -d "https://ngochuy2002.github.io/qhxh_hanoi_domain/planning?objectid=123"

# Verify App Links
adb shell pm get-app-links com.example.qhxd_hanoi
# Should show: "ngochuy2002.github.io: verified"
```

### iOS
Open Safari on device and navigate to:
```
https://ngochuy2002.github.io/qhxh_hanoi_domain/planning?objectid=123
```

Should automatically open the app.

### Real-world Test
1. Share a planning info from the app
2. Send to yourself via WhatsApp/Messenger
3. Click the link
4. Should open the app directly!

## App Configuration

The Flutter app is already configured to handle these links. No additional changes needed in the app code.

## SHA-256 Fingerprint

The current SHA-256 fingerprint in `assetlinks.json` is:
```
E9:31:E6:22:B3:F3:4C:38:E3:99:3A:2E:21:DD:CF:F0:91:7D:9C:11:55:67:FF:D4:7F:A3:A0:14:49:77:52:21
```

This is from your debug keystore. For production, you'll need to add your release keystore's SHA-256.

## Troubleshooting

**Links don't open the app:**
- Wait 24 hours for Google to verify App Links
- Check that assetlinks.json is accessible
- Verify package name matches exactly
- Try clearing app data and reinstalling

**iOS not working:**
- Verify Team ID is correct in apple-app-site-association
- Check bundle identifier matches
- Enable Associated Domains in Xcode

## Support

For issues, contact the QHXD Hà Nội development team.
