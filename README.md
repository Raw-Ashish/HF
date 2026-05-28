# Hacking Freaks Digital Agency — Business Website

A full-featured luxury dark-gold business website for **Hacking Freaks Digital Agency**, built with React, Vite, TypeScript, and Firebase. All content is managed through a built-in admin panel and persisted globally via Firebase Realtime Database — changes made in the admin panel are instantly visible to all visitors on any device.

---

## [Live Demo](https://hackingfreaks.vercel.app))

> Deploy to Vercel, Netlify, or any static host. Firebase handles all data and authentication.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Pages & Routes](#pages--routes)
- [Admin Panel](#admin-panel)
- [Content Sections System](#content-sections-system)
- [Firebase Setup](#firebase-setup)
- [SEO & Open Graph](#seo--open-graph)
- [Lightbox Gallery](#lightbox-gallery)
- [Getting Started](#getting-started)
- [Environment & Configuration](#environment--configuration)
- [Deployment](#deployment)
- [Data Architecture](#data-architecture)

---

## Features

### Public Site
- **Luxury dark-gold theme** — fully custom CSS with gold gradients, glass cards, and premium typography
- **Animated hero section** with live dashboard widget showing real-time business stats
- **Animated counters** that trigger on scroll into view
- **Full pages** — Home, Services, Projects, Shop, Team, About, Hire Us, 404
- **Detail pages** for every service, project, and shop product at their own slug URL
- **Fullscreen lightbox gallery** with keyboard navigation, swipe gestures, pinch-to-zoom, and thumbnail strip
- **Responsive design** — fully optimised for desktop, tablet, and mobile
- **Scroll-to-top** on every page navigation (instant, no animation flash)
- **Dynamic SEO** — page title, meta description, Open Graph (Telegram/Facebook/LinkedIn), and Twitter Card tags update per page

### Admin Panel (`/admin`)
- **Firebase Authentication** — secure login with email and password
- **13 content editors** — Hero, Stats, Services, Projects, Products, Team, Testimonials, Contact, Navigation, Footer, Branding, SEO, Categories
- **Dynamic content blocks** (Sections Builder) for Services, Projects, and Products — add, remove, and reorder unlimited content sections without touching code
- **Live image previews** in gallery and product editors
- **Save to Firebase** — all changes are globally persistent immediately
- **Reset per section** or reset all content to defaults

### Firebase Backend
- **Realtime Database** — all CMS content synced globally in real time
- **Firebase Authentication** — admin login secured via Firebase Auth
- **Loading gate** — site waits for Firebase data before rendering; visitors never see a flash of default content

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 18 + TypeScript |
| Build Tool | Vite 7 |
| Routing | Wouter |
| Styling | Tailwind CSS + custom CSS variables |
| Animations | Framer Motion |
| Database | Firebase Realtime Database |
| Authentication | Firebase Authentication |
| Icons | Lucide React |
| State | React Context API |
| Package Manager | pnpm (workspace monorepo) |
| UI Primitives | Radix UI / shadcn-ui |

---

## Project Structure

```
HackingFreaks/
├── index.html                          # HTML entry — OG tags, fonts, favicon
├── src/
│   ├── App.tsx                         # Router, ScrollToTop, SeoUpdater, FirebaseGate
│   ├── main.tsx                        # React root
│   ├── index.css                       # Global styles, CSS variables, luxury theme
│   ├── admin.css                       # Admin panel specific styles
│   │
│   ├── lib/
│   │   ├── firebase.ts                 # Firebase app init, db and auth exports
│   │   └── utils.ts                    # Utility helpers
│   │
│   ├── context/
│   │   └── DataContext.tsx             # Firebase Realtime DB reads/writes, global state
│   │
│   ├── data/                           # JSON default values (seed data + TypeScript types)
│   │   ├── hero.json
│   │   ├── stats.json
│   │   ├── services.json               # Includes slug and sections arrays
│   │   ├── products.json               # Includes slug and sections arrays
│   │   ├── projects.json               # Includes slug and sections arrays
│   │   ├── team.json
│   │   ├── testimonials.json
│   │   ├── contact.json
│   │   ├── branding.json
│   │   ├── navigation.json
│   │   ├── footer.json
│   │   ├── seo.json                    # Per-page title, description, keywords
│   │   └── categories.json
│   │
│   ├── components/
│   │   ├── Header.tsx                  # Sticky nav with mobile menu
│   │   ├── Footer.tsx                  # Footer with links and branding
│   │   ├── Lightbox.tsx                # Fullscreen image viewer (keyboard + swipe + pinch-zoom)
│   │   ├── ContentSections.tsx         # Renders dynamic content blocks on detail pages
│   │   ├── ServiceCard.tsx             # Service card with "More Details" link
│   │   ├── ProductCard.tsx             # Product card with buy button and gallery
│   │   ├── ProjectCard.tsx             # Project card with gallery and "View Details" link
│   │   ├── TeamCard.tsx                # Team member card
│   │   ├── AnimatedCounter.tsx         # Scroll-triggered number counter
│   │   └── ui/                         # shadcn-ui primitives (button, dialog, toast, etc.)
│   │
│   ├── pages/
│   │   ├── Home.tsx                    # Landing page — hero, stats, services preview, projects, shop, testimonials, team
│   │   ├── Services.tsx                # Full services listing
│   │   ├── ServiceDetail.tsx           # /service/:slug — full detail page
│   │   ├── Projects.tsx                # Project portfolio grid
│   │   ├── ProjectDetail.tsx           # /project/:slug — full detail page
│   │   ├── Shop.tsx                    # Product shop with category filter
│   │   ├── ProductDetail.tsx           # /shop/:slug — full detail page
│   │   ├── Team.tsx                    # Team members page
│   │   ├── About.tsx                   # About page with stats and quote
│   │   ├── Hire.tsx                    # Contact / hire page with all channels
│   │   ├── not-found.tsx               # 404 page
│   │   │
│   │   └── admin/
│   │       ├── AdminPage.tsx           # Auth gate — shows login or dashboard
│   │       ├── AdminLogin.tsx          # Firebase Auth email/password login form
│   │       ├── AdminDashboard.tsx      # Sidebar nav + section editor shell
│   │       └── sections/
│   │           ├── HeroEditor.tsx
│   │           ├── StatsEditor.tsx
│   │           ├── ServicesEditor.tsx  # + SectionsBuilder integration
│   │           ├── ProjectsEditor.tsx  # + SectionsBuilder integration
│   │           ├── ProductsEditor.tsx  # + SectionsBuilder integration
│   │           ├── TeamEditor.tsx
│   │           ├── TestimonialsEditor.tsx
│   │           ├── ContactEditor.tsx
│   │           ├── NavigationEditor.tsx
│   │           ├── FooterEditor.tsx
│   │           ├── BrandingEditor.tsx
│   │           ├── SeoEditor.tsx
│   │           ├── CategoriesEditor.tsx
│   │           └── SectionsBuilder.tsx # Dynamic content block builder (8 block types)
│   │
│   └── hooks/
│       ├── use-mobile.tsx
│       └── use-toast.ts
```

---

## Pages & Routes

| Route | Page | Description |
|---|---|---|
| `/` | Home | Hero, live dashboard, stats, services preview, featured projects, shop preview, testimonials, team |
| `/services` | Services | Full listing of all services with feature lists and pricing |
| `/service/:slug` | Service Detail | Full detail page with unlimited content sections and gallery |
| `/projects` | Projects | Portfolio grid with image cards and tags |
| `/project/:slug` | Project Detail | Full case study with sections, gallery, and buttons |
| `/shop` | Shop | Product grid with category filter tabs |
| `/shop/:slug` | Product Detail | Full product page with price, stock, gallery, buy button, and sections |
| `/team` | Team | Team member cards |
| `/about` | About | Agency story, stats, and quote |
| `/hire` | Hire Us | Contact methods, form, and communication channels |
| `/admin` | Admin Panel | Protected CMS — requires Firebase Auth login |

All routes are directly accessible by URL — deep linking works without any server configuration.

---

## Admin Panel

### Login

Navigate to `/admin`. The login form uses **Firebase Authentication**.

- **Email:** `admin@supplywalah.com`
- **Password:** Set in your Firebase Console under Authentication → Users

The session persists across page refreshes. Firebase Auth handles session management automatically.

### Editors

Once logged in, the sidebar gives access to 13 section editors:

| Editor | What You Can Edit |
|---|---|
| **Hero** | Headline, subheadline, CTA buttons, badge text, dashboard widget stats |
| **Stats** | Counter numbers, labels, suffixes (e.g. 150+, 50+) |
| **Services** | Title, slug, description, features, pricing lines, gallery images, CTA button, content sections |
| **Projects** | Title, slug, overview, year, category, status, tags, images, card buttons, content sections |
| **Products** | Name, slug, price, currency, stock, stock status, offer/discount, rating, description, features, delivery, buy link, gallery images, content sections |
| **Team** | Name, role, bio, avatar, social links |
| **Testimonials** | Quote, author name, role, company, rating |
| **Contact** | Phone, WhatsApp, Telegram, email, social links, address |
| **Navigation** | Nav links (label + href) |
| **Footer** | Footer description, link columns, bottom text |
| **Branding** | Agency name, tagline, logo URL, primary color, meta description |
| **SEO** | Per-page title, description, and keywords |
| **Categories** | Product category list for shop filter |

Every editor has a **Save** button (writes instantly to Firebase, visible to all users) and a **Reset** button (restores that section to the JSON defaults).

---

## Content Sections System

Services, Projects, and Products each support a **Sections Builder** — a drag-and-drop-style editor for building rich detail pages with unlimited content blocks. Each block has its own editor UI.

### Available Block Types

| Type | Description |
|---|---|
| **Paragraph** | Heading + body text for narrative sections |
| **Features List** | Bullet list of features with gold checkmark icons |
| **Feature Boxes** | Grid of titled cards with descriptions (e.g. key results, highlights) |
| **Specs / Tech Details** | Label–value rows in a grid (e.g. Language: Python, Timeline: 3 days) |
| **Image Gallery** | Grid of images with fullscreen lightbox on click |
| **Buttons** | One or more CTA buttons (Gold or Outline style, internal or external links) |
| **Pricing** | Highlighted pricing lines in a gold-bordered box |
| **FAQ** | Accordion of questions and answers |

Blocks can be reordered with the up/down arrows, expanded to edit, and deleted. Any combination of blocks can be used in any order.

### How Slugs Work

Every service, project, and product has a `slug` field — this becomes the URL path:

```
/service/telegram-bot-recovery
/project/whatsapp-lead-gen
/shop/whatsapp-bulk-message
```

If a slug doesn't match any item, the page shows a 404. Slugs are editable in the admin panel.

---

## Firebase Setup

### 1. Create a Firebase Project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Create a new project (or use an existing one)
3. Enable **Realtime Database** — start in test mode, then apply security rules (see below)
4. Enable **Authentication** → Sign-in method → **Email/Password**
5. Create an admin user under Authentication → Users

### 2. Configure the App

Update `src/lib/firebase.ts` with your project's config:

```ts
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.firebasestorage.app",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID",
};
```

> **Note:** Firebase web config keys are safe to include in frontend code. Security is enforced by Firebase Security Rules, not by hiding the config.

### 3. Firebase Security Rules

Apply these rules in Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    "cms": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

This allows:
- **Anyone** to read all CMS content (required for the public site)
- **Only authenticated users** to write (admin only)

### 4. Database Structure

All content lives under the `/cms` key in the Realtime Database:

```
/cms
  /hero        → { headline, subheadline, badge, ... }
  /stats       → { stats: [...] }
  /services    → { services: [...] }
  /products    → { products: [...] }
  /projects    → { projects: [...] }
  /team        → { members: [...] }
  /testimonials → { testimonials: [...] }
  /contact     → { phone, whatsapp, telegram, email, ... }
  /branding    → { name, tagline, logo, primaryColor, ... }
  /navigation  → { links: [...] }
  /footer      → { description, columns: [...] }
  /seo         → { pages: { "/": {...}, "/services": {...}, ... } }
  /categories  → { categories: [...] }
```

On the very first load, if `/cms` is empty, the app seeds Firebase with the default values from the JSON files in `src/data/`. After that, the JSON files are only used as TypeScript type references.

---

## SEO & Open Graph

### Static Fallback (`index.html`)

The `index.html` file contains complete OG and Twitter Card tags for the homepage. These are read by bots (Telegram, Facebook, Twitter, LinkedIn) that crawl raw HTML before JavaScript runs:

```html
<meta property="og:title" content="Hacking Freaks — Elite Automation & Bot Services" />
<meta property="og:description" content="..." />
<meta property="og:image" content="https://..." />
<meta name="twitter:card" content="summary_large_image" />
```

### Dynamic Per-Page SEO

The `SeoUpdater` component in `App.tsx` updates all meta tags on every route change:

- `document.title`
- `meta[name="description"]`
- `meta[name="keywords"]`
- `meta[property="og:title"]`
- `meta[property="og:description"]`
- `meta[name="twitter:title"]`
- `meta[name="twitter:description"]`

Per-page SEO data is managed from the admin panel → SEO editor, stored in Firebase under `/cms/seo`.

### Telegram Cache

Telegram aggressively caches link previews. After updating your site, force a refresh by sending your URL to **@WebpageBot** on Telegram.

---

## Lightbox Gallery

The `Lightbox` component (`src/components/Lightbox.tsx`) provides a fullscreen image viewer used across project cards, product cards, and detail pages.

**Features:**
- Keyboard navigation — `←` / `→` to navigate, `Esc` to close, `+` / `-` to zoom
- Swipe gestures on mobile (left/right)
- Pinch-to-zoom on touchscreens
- Thumbnail strip at the bottom
- Image counter (e.g. `2 / 5`)
- Lazy loading with spinner while image loads
- Smooth transitions between images

Clicking any project image, product image, or gallery block on a detail page opens the lightbox.

---

## Getting Started

### Prerequisites

- Node.js 18+
- pnpm (`npm install -g pnpm`)

### Install

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO

# Install all workspace dependencies
pnpm install
```

### Run in Development

```bash
pnpm --filter @workspace/business-site run dev
```

The site runs at `http://localhost:21868` (or the port configured in the workflow).

### Typecheck

```bash
pnpm run typecheck
```

### Build

```bash
pnpm --filter @workspace/business-site run build
```

---

## Environment & Configuration

There are no required environment variables for the frontend — the Firebase config is embedded directly in `src/lib/firebase.ts` (this is normal and safe for Firebase web apps; security is enforced by Firebase Rules).

If you want to use environment variables instead:

1. Create `.env.local` in `artifacts/business-site/`:

```env
VITE_FIREBASE_API_KEY=your_key
VITE_FIREBASE_DATABASE_URL=https://your-project-default-rtdb.firebaseio.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_APP_ID=your_app_id
```

2. Update `src/lib/firebase.ts` to use `import.meta.env.VITE_FIREBASE_*`.

---

## Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy from the business-site directory
cd artifacts/business-site
vercel
```

Add a `vercel.json` for SPA routing (all paths redirect to `index.html`):

```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```

### Netlify

Add a `_redirects` file to `artifacts/business-site/public/`:

```
/*  /index.html  200
```

### Any Static Host

Run `pnpm --filter @workspace/business-site run build` and upload the contents of `artifacts/business-site/dist/` to your host.

> **Important:** All hosts need to be configured to serve `index.html` for all routes (SPA fallback). Without this, direct URL access to `/services`, `/project/slug`, etc. will return a 404.

---

## Data Architecture

### How Data Flows

```
JSON files (src/data/)
      │
      ▼  (first run — if Firebase /cms is empty)
Firebase Realtime Database (/cms)
      │
      ▼  (onValue listener — real time)
DataContext (React Context)
      │
      ▼
All pages and components
```

1. On app load, a Firebase `onValue` listener connects to `/cms`
2. A `FirebaseGate` component blocks rendering until Firebase responds (prevents JSON flash)
3. If `/cms` is empty, default JSON data is used directly
4. Admin panel writes via `set()` to the relevant `/cms/<section>` path
5. All connected clients receive the update in real time via the `onValue` listener

### Adding a New Section

1. Add default data to a new JSON file in `src/data/`
2. Import it in `DataContext.tsx` and add to `defaultData`
3. Create an editor component in `src/pages/admin/sections/`
4. Register the editor in `AdminDashboard.tsx`
5. Use `useSiteData().data.yourSection` in any page or component

---

## Key Files Reference

| File | Purpose |
|---|---|
| `src/lib/firebase.ts` | Firebase initialization — db and auth exports |
| `src/context/DataContext.tsx` | Global CMS state — Firebase reads/writes |
| `src/App.tsx` | Router, ScrollToTop, SeoUpdater, FirebaseGate |
| `src/components/ContentSections.tsx` | Renders all 8 content block types on detail pages |
| `src/pages/admin/sections/SectionsBuilder.tsx` | Admin UI for building content block arrays |
| `index.html` | Static OG/Twitter tags for bot crawlers |
| `src/data/seo.json` | Per-page SEO defaults |

---

## License

MIT — free to use, modify, and deploy.

---

## Credits

Built with [React](https://react.dev), [Vite](https://vite.dev), [Firebase](https://firebase.google.com), [Tailwind CSS](https://tailwindcss.com), [Framer Motion](https://www.framer.com/motion/), and [Lucide Icons](https://lucide.dev).
