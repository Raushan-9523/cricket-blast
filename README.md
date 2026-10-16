# CRICKET BLAST – "Har Ball Ki Baat!" 🏏

> India's premier high-impact sports digital media portal for Indian cricket fans. Featuring live scores, ball-by-ball scorecards, IPL 2026 coverage, match tactical analysis, YouTube shorts, breaking news ticker, and an authorized editorial dashboard.

---

## 🌟 Key Features

1. **Brand Identity & Multilingual Architecture**:
   - Tagline: *"Har Ball Ki Baat!"* (हर बॉल की बात!).
   - Hindi-first editorial format with seamless bilingual switching between **हिंदी (Hindi)**, **Hinglish**, and **English**.
   - Custom athletic sports typography featuring Teko, Plus Jakarta Sans, and Yantramanav.
   - Circular sports emblem with floodlights, wooden stumps, crossed bats, and red leather seam ball matching official Cricket Blast branding.

2. **Match Centre & Scorecard Simulation**:
   - Live, upcoming, and completed match cards with realistic simulation status, target, and run rates.
   - Full scorecard with detailed Batting statistics (Dismissal, Runs, Balls, 4s, 6s, SR), Bowling analysis (O, M, R, W, Econ), Fall of Wickets, and live ball-by-ball commentary feed.
   - Cleanly marked as verified simulation data without scraping or deceiving readers.

3. **14 Homepage Editorial Sections**:
   - Breaking News Ticker with live alert flash and pause/play controls.
   - Lead Featured Story with high-resolution visuals and Key Takeaways.
   - Latest Cricket News with interactive tabs (Team India, IPL 2026, Analysis, Stats).
   - Match Schedule and Fixtures in IST.
   - Points Table for IPL 2026 and ICC World Test Championship (WTC).
   - YouTube Shorts & Video Reel player modal.
   - Columnist Opinion & Top 5 Trending Reads.
   - Daily Newsletter subscription form.
   - Comprehensive footer with trust policies.

4. **Staff Admin Dashboard (`/admin`)**:
   - Secure staff authentication (`/admin/login`).
   - Create, edit, toggle published/draft, and delete articles with rich preview.
   - Manage real-time breaking news ticker alerts.
   - Manage video clips and YouTube reels.
   - Monetization & Google AdSense placement toggles (Header Banner, In-Article, Sidebar, Homepage Interstitial, Footer).
   - Site settings, editorial contacts, and data reset tool.

5. **Monetization & Google AdSense Ready**:
   - Fully compliant ad placement slots with discreet "ADVERTISEMENT / विज्ञापन" labels.
   - Configurable AdSense Publisher Client ID (placeholder: `ca-pub-XXXXXXXXXXXXXX`) and ad slot IDs.
   - Zero misleading clicks or forced interactions.

6. **SEO & Structured Data**:
   - Schema.org JSON-LD `NewsArticle` and `BreadcrumbList` structured data.
   - Dedicated slug routing for articles: `/article/:slug`.
   - `sitemap.xml` and `robots.txt` generated for search engines.
   - Open Graph and Twitter Card tags in `index.html`.

7. **Legal & Trust Pages**:
   - `/about`: Mission, editorial principles, and publisher info.
   - `/contact`: Interactive contact and correction form.
   - `/editorial-policy`: Sourcing, fact-checking, and correction policy.
   - `/privacy-policy`: Cookie and subscriber protection.
   - `/disclaimer`: Fair-use editorial sports data attribution.
   - `/terms`: Terms of service.

---

## 🛠️ Local Development & Setup

### Prerequisites
- Node.js (v18 or higher)
- npm or bun

### Installation
```bash
# Install dependencies
npm install

# Start development server
npm run dev
```
The application will run locally at `http://localhost:3000`.

---

## 🔑 Environment Variables (`.env`)

Refer to `.env.example`:
```env
# GEMINI_API_KEY: Optional for future automated summary features
GEMINI_API_KEY="MY_GEMINI_API_KEY"

# APP_URL: Current hosting origin
APP_URL="https://cricketblast.in"
```

---

## 🛡️ Admin Access Credentials

To test the editorial workflow:
1. Navigate to `/admin/login` or click **"एडमिन लॉगिन"** in the top navigation bar.
2. Enter staff passkey:
   - **Passkey**: `cricketblast2026` (or `admin123`)
   - **Email**: `editor@cricketblast.in`
3. You will be redirected to the full admin workspace with real-time editing.

---

## 🔥 Cloud Firestore & Firebase Setup (Optional)

When deploying with Firebase:
1. Initialize Firebase in the root directory.
2. Configure `firestore.rules`:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function isAdmin() {
      return request.auth != null && request.auth.token.admin == true;
    }

    match /articles/{articleId} {
      allow read: if resource.data.status == 'published' || isAdmin();
      allow write: if isAdmin();
    }

    match /breaking_alerts/{alertId} {
      allow read: if true;
      allow write: if isAdmin();
    }

    match /matches/{matchId} {
      allow read: if true;
      allow write: if isAdmin();
    }

    match /settings/{docId} {
      allow read: if true;
      allow write: if isAdmin();
    }

    match /newsletter_subscribers/{subscriberId} {
      allow create: if request.resource.data.email is string;
      allow read, update, delete: if isAdmin();
    }
  }
}
```

---

## 🚀 Deployment

Build production static assets:
```bash
npm run build
```
Preview production build:
```bash
npm run preview
```
