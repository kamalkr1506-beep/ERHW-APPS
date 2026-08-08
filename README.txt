═══════════════════════════════════════════════════════════════
  ERHW PWA → APK Package v2 (Fixed for PWA Builder)
═══════════════════════════════════════════════════════════════

📁 CONTENTS:
  • index.html       - Main app
  • manifest.json    - PWA manifest (fixed paths)
  • sw.js            - Service Worker
  • icon-*.png       - Icons in ROOT (required by PWA Builder)
  • icons/           - Duplicate icons folder
  • screenshots/     - Placeholder screenshots
  • .well-known/     - assetlinks.json

═══════════════════════════════════════════════════════════════
🚀 BUILD APK WITH PWA BUILDER
═══════════════════════════════════════════════════════════════

1. UPLOAD ALL FILES to Netlify first:
   https://app.netlify.com/sites/beautiful-crisp-fa8aed/deploys

2. Go to: https://www.pwabuilder.com

3. Enter URL: https://beautiful-crisp-fa8aed.netlify.app

4. Click "Start" → wait for checks

5. Go to "Android" tab → "Generate Package"

6. Download APK or AAB

═══════════════════════════════════════════════════════════════
🔧 FIXES IN THIS VERSION
═══════════════════════════════════════════════════════════════

✅ Icons: 8 sizes (72-512) in ROOT directory
✅ Icons: purpose="any maskable" for 192px and 512px
✅ Manifest: relative paths (no leading /)
✅ Screenshots: placeholder 1080x1920
✅ No broken links

═══════════════════════════════════════════════════════════════
