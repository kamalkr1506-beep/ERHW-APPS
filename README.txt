═══════════════════════════════════════════════════════════════
  ERHW PWA → APK Package
  ERHW v4.0 + Supabase | Road Safety Platform
═══════════════════════════════════════════════════════════════

📁 CONTENTS:
  • index.html       - Main app (Supabase integrated)
  • manifest.json    - PWA manifest with icons & shortcuts
  • sw.js            - Service Worker (offline support)
  • icons/           - PWA icons (72, 96, 128, 144, 192, 384, 512)
  • .well-known/     - assetlinks.json for Trusted Web Activity

═══════════════════════════════════════════════════════════════
🚀 METHOD 1: PWA Builder (Easiest - 2 minutes)
═══════════════════════════════════════════════════════════════

1. Go to: https://www.pwabuilder.com
2. Enter your URL: https://beautiful-crisp-fa8aed.netlify.app
3. Click "Start" → Go to "Android" section
4. Click "Generate" → Download APK/AAB
5. Install on your phone!

═══════════════════════════════════════════════════════════════
🛠️ METHOD 2: Bubblewrap CLI (For Google Play Store)
═══════════════════════════════════════════════════════════════

Requirements: Node.js + Java JDK + Android SDK

  npm install -g @bubblewrap/cli

  bubblewrap init --manifest https://beautiful-crisp-fa8aed.netlify.app/manifest.json
  bubblewrap build

Output: app-release-signed.apk + app-release-bundle.aab

═══════════════════════════════════════════════════════════════
🔧 FIXES INCLUDED FOR APK:
═══════════════════════════════════════════════════════════════

✅ Icons: All sizes generated (72px to 512px)
✅ Manifest: Standalone display, portrait orientation
✅ GPS: Browser handles location permissions via JS
   → In APK, Android auto-requests location permission
✅ TTS: Uses Web Speech API (works in WebView/APK)
   → For better TTS in APK, consider native TTS plugin
✅ Offline: Service Worker caches app for offline use
✅ Background Sync: Queues reports when offline

═══════════════════════════════════════════════════════════════
⚠️ IMPORTANT: Upload to Netlify FIRST
═══════════════════════════════════════════════════════════════

Upload ALL files in this folder to your Netlify site root:
  - index.html
  - manifest.json
  - sw.js
  - icons/ (folder)
  - .well-known/ (folder)

Then update SUPABASE_URL in index.html if needed:
  const SUPABASE_URL = 'https://pxloolvcpvedrtfvotpo.supabase.co';

═══════════════════════════════════════════════════════════════
📱 ANDROID PERMISSIONS (Auto-handled by Bubblewrap/PWA Builder)
═══════════════════════════════════════════════════════════════

Required permissions for full functionality:
  • INTERNET          - Supabase sync
  • ACCESS_FINE_LOCATION - GPS tracking
  • RECORD_AUDIO      - Voice alerts (TTS)
  • VIBRATE           - Alert notifications

═══════════════════════════════════════════════════════════════
🌐 SUPABASE TABLES REQUIRED
═══════════════════════════════════════════════════════════════

Run this SQL in Supabase SQL Editor:

-- Table: reports
CREATE TABLE reports (
  id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  type text NOT NULL,
  user_name text,
  user_id uuid REFERENCES auth.users,
  is_guest boolean DEFAULT true,
  lat double precision NOT NULL,
  lng double precision NOT NULL,
  status text DEFAULT 'pending',
  created_at timestamptz DEFAULT now(),
  confirmed_at timestamptz,
  closed_at timestamptz
);

ALTER TABLE reports ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Allow public read" ON reports FOR SELECT USING (true);
CREATE POLICY "Allow authenticated insert" ON reports FOR INSERT TO authenticated WITH CHECK (true);
ALTER PUBLICATION supabase_realtime ADD TABLE reports;

-- Table: profiles
CREATE TABLE profiles (
  id uuid REFERENCES auth.users ON DELETE CASCADE PRIMARY KEY,
  name text,
  phone text UNIQUE,
  reports_count int DEFAULT 0,
  points int DEFAULT 0,
  level int DEFAULT 1,
  updated_at timestamptz DEFAULT now()
);

ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Allow public read profiles" ON profiles FOR SELECT USING (true);
CREATE POLICY "Allow users update own profile" ON profiles FOR UPDATE TO authenticated USING (auth.uid() = id);
CREATE POLICY "Allow insert own profile" ON profiles FOR INSERT TO authenticated WITH CHECK (auth.uid() = id);

═══════════════════════════════════════════════════════════════
📞 NEED HELP?
═══════════════════════════════════════════════════════════════

• Supabase Docs: https://supabase.com/docs
• PWA Builder: https://docs.pwabuilder.com
• Bubblewrap: https://github.com/GoogleChromeLabs/bubblewrap

═══════════════════════════════════════════════════════════════
