# Hamza — Frontend & React Developer Portfolio

A complete, GitHub-ready **Next.js + React + TypeScript** portfolio, recreated from the requirements of the Hamza portfolio project. Includes a responsive, animated design, project listing, official live TARZO embed, and a WhatsApp icon contact screen backed by server-side redirect routes.

> **Source note:** This is a newly prepared, editable portfolio codebase matching the confirmed functionality. It is **not a byte-for-byte export of the original hosted Site repository**. The three projects other than TARZO are clearly labeled editable sample slots because their original titles and URLs were not available. TARZO is embedded from the real public website; its source code is **not** part of this repository.

## What is included

- Homepage: hero, about, services, skills, featured TARZO work and animated CTAs.
- `/projects`: filterable project cards; TARZO shows its **live** website in an `iframe` (not a static fashion photo).
- `/contact`: animated **WhatsApp-icon-only** contact button. The phone/email are not printed in the public UI.
- `/api/contact/whatsapp`: server-side redirect to the configured WhatsApp number.
- `/api/contact/email`: server-side email `mailto:` redirect (kept available, but not visibly linked on the contact page).
- Mobile navigation, accessibility-friendly markup, SEO metadata, 404 page, `robots.txt` and sitemap.
- Plain CSS animations (no animation dependency needed).

## Requirements

- Node.js **20.9+** (prefer Node.js 22)
- npm

## Run locally

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open `http://localhost:3000`.

To check production compilation:

```bash
npm run typecheck
npm run build
npm run start
```

The server contact routes already have fallback contact values for local testing. In production, set the two env vars below for easy management.

## Environment variables (backend contact settings)

Add these values to `.env.local` locally and to **Vercel → Project → Settings → Environment Variables** in production:

```dotenv
CONTACT_WHATSAPP_NUMBER=923198220874
CONTACT_EMAIL=humzarypto@gmail.com
```

The `03198220874` Pakistani mobile number is converted to international WhatsApp format `923198220874` (country code `92`, without leading `0`).

**Important:** A WhatsApp number is not a secret when users click a WhatsApp link, because the destination URL includes it. Using a server-side redirect keeps the number out of the page's rendered text/config; it does not hide the number from the browser's destination URL.

## Upload this portfolio to GitHub

Create an empty repo on GitHub (for example `hamza-portfolio`). Then run these commands from inside this folder:

```bash
git init
git add .
git commit -m "Initial Hamza portfolio"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/hamza-portfolio.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your real GitHub username. Do not upload `node_modules`, `.next` or `.env.local` (already excluded by `.gitignore`).

## Deploy from GitHub (recommended: Vercel)

1. Go to <https://vercel.com/new> and choose **Import Git Repository**.
2. Select your GitHub `hamza-portfolio` repo.
3. Framework should auto-detect **Next.js**.
4. Add `CONTACT_WHATSAPP_NUMBER` and `CONTACT_EMAIL` to the environment variables.
5. Click **Deploy**. Future GitHub pushes will trigger new portfolio deployments.

**GitHub Pages note:** This project has Next.js server route handlers, so GitHub Pages alone cannot run the contact backend. GitHub is the code host; Vercel (or another Next.js server-compatible host) runs the website.

## Editing project cards

Open `data/projects.ts`:

- The **TARZO** card links to `https://wear-tarzo.papanotify.chatgpt.site`.
- The other three cards are explicitly marked as sample slots. Replace their names/descriptions, assign real `url` values, and change `status` to `"live"` when your real projects are ready.
- Add additional cards to the array as needed (adjust displayed ordinal if you change the number of projects).

### Does TARZO update automatically?

The card uses the **live TARZO site URL directly** as the `iframe` source. New published changes to the original TARZO site appear in the portfolio **when visitors load or refresh the page**, subject to the original website's caching and iframe permission. Unlike a screenshot, this does not require updating the portfolio's source each time. It is not real-time synchronization of TARZO's source files or database.

If the original site ever adds a restrictive `X-Frame-Options` or Content-Security-Policy frame-ancestor rule, browsers may stop displaying the embed; its **Visit site** link will still open TARZO directly.

## Structure

```text
hamza-portfolio-github/
├── app/
│   ├── api/contact/email/route.ts
│   ├── api/contact/whatsapp/route.ts
│   ├── contact/page.tsx
│   ├── projects/page.tsx
│   ├── globals.css
│   ├── layout.tsx
│   ├── not-found.tsx
│   ├── page.tsx
│   ├── robots.ts
│   └── sitemap.ts
├── components/
│   ├── ProjectCard.tsx
│   ├── ProjectGrid.tsx
│   ├── Reveal.tsx
│   ├── SiteFooter.tsx
│   └── SiteHeader.tsx
├── data/
│   ├── projects.ts
│   └── site.ts
├── public/favicon.svg
├── .env.example
├── .gitignore
├── .gitattributes
├── next.config.ts
├── package.json
├── tsconfig.json
└── README.md
```

## Customization

- Main name, text, skills and live TARZO URL: `data/site.ts`.
- Project items: `data/projects.ts`.
- Colors, layout, animations: `app/globals.css`.
- Homepage sections: `app/page.tsx`.
- Navigation: `components/SiteHeader.tsx`.
- Contact icon and its layout: `app/contact/page.tsx`.
- Backend contact details: environment variables above.

The starter metadata uses the original portfolio's URL (`data/site.ts`), but when you deploy to a new public domain, update `siteUrl` to your new domain so canonical links and sitemap use the correct host.

## License

The source is yours to edit and publish for your own portfolio. Third-party websites embedded via iframe remain owned/managed by their respective owners.
