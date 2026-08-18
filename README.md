# MDR Law & Associates — website

Production-ready static site, split into HTML / CSS / JS, ready to upload to
any standard web host (Apache, Nginx, Netlify, Vercel, cPanel, GitHub Pages,
etc.). No build step is required — this is plain HTML/CSS/JS.

## Folder structure

```
mdrlaw-website/
├── index.html                        ← Home page
├── about.html
├── practice-areas.html
├── civil-commercial-litigation.html
├── corporate-nclt.html
├── contracts-arbitration.html
├── property-law.html
├── constitutional-human-rights.html
├── criminal-law.html
├── matrimonial-family-law.html
├── ip-media-law.html
├── international-arbitration.html
├── our-lawyers.html
├── insights.html
├── judgments.html
├── contact.html
├── privacy-policy.html
├── disclaimer.html
├── css/
│   └── styles.css                    ← All site styling (extracted from inline <style>)
├── js/
│   └── main.js                       ← Mobile nav, footer year, scroll-reveal (extracted from inline <script>)
└── assets/
    ├── README.md                     ← What images you still need to add, and their expected names/sizes
    ├── logo-black.png                ← NOT INCLUDED — see assets/README.md
    ├── logo-white.png                ← NOT INCLUDED — see assets/README.md
    ├── icon-black.png                ← NOT INCLUDED — see assets/README.md
    └── og-image.jpg                  ← NOT INCLUDED — see assets/README.md
```

## What changed from the original single file

The original `index.html` had ~500 lines of CSS in a `<style>` block and
~40 lines of JS in a `<script>` block. These are now separate files:

- **`css/styles.css`** — every rule, unchanged, referenced via
  `<link rel="stylesheet" href="css/styles.css">` in `<head>`.
- **`js/main.js`** — the mobile-menu toggle, footer copyright year, and
  scroll-reveal animation logic, unchanged, loaded via
  `<script src="js/main.js" defer></script>` just before `</body>`
  (`defer` keeps it non-blocking and ensures the DOM exists before it runs).
- The page's structured data (`<script type="application/ld+json">`) was
  **kept inline** in `index.html` — search engines expect JSON-LD on the
  page itself, not in an external file.

Every other line of markup, copy, and inline attribute (styles used for
one-off overrides, `onsubmit` on the enquiry form, etc.) is untouched.

## About the extra pages

Your uploaded file only contained the home page, but its header/footer
navigation links to 17 other pages (About, Practice Areas, the nine
individual practice-area pages, Our Lawyers, Insights, Judgments, Contact,
Privacy Policy, Disclaimer). To make sure **no link on the live site 404s**,
each of those pages has been generated using the same header, footer,
floating WhatsApp/call buttons, fonts, and stylesheet — with a placeholder
content section flagged with a dashed border reading "PLACEHOLDER."

These are safe to deploy as-is (they won't break anything), but you'll want
to replace the placeholder section in each with real content before or
shortly after launch. The home page (`index.html`) is fully finished and
untouched.

## Before you go live

1. **Add the four missing images** into `assets/` — see `assets/README.md`
   for exact filenames and sizes (`logo-black.png`, `logo-white.png`,
   `icon-black.png`, `og-image.jpg`).
2. **Wire up the contact form** — it currently just shows a placeholder
   alert (`contact.html` doesn't have the form; it's on `index.html`'s
   Contact section). Point the `<form>` at your email service, a form
   backend (Formspree, Netlify Forms, etc.), or your CRM.
3. **Add the Google Maps embed** — there's a labelled placeholder box in
   the Contact section (`.map-embed`) for your Armenian Street office.
4. **Fill in the 17 placeholder pages** with real content, or remove the
   ones you don't need (and their nav links) if you'd rather ship fewer
   pages at launch.
5. **Double-check the schema.org JSON-LD** in `index.html`'s `<head>` — it
   still has two placeholder `sameAs` entries for LinkedIn/Instagram/
   Twitter URLs if you have social profiles to add.

## Deploying

Any static host works — upload the whole `mdrlaw-website/` folder
(contents, not the folder itself) to your web root:

- **Shared hosting / cPanel**: upload everything into `public_html/`.
- **Netlify / Vercel**: drag-and-drop the folder, or connect a Git repo —
  no build command needed, publish directory is the project root.
- **GitHub Pages**: push this folder to a repo and enable Pages on the
  `main` branch root.

All internal links use root-relative paths (e.g. `/about.html`), so the
site must be deployed at your domain root (`https://www.mdrlaw.in/`) for
navigation and the canonical URLs in `<head>` to match. If you ever deploy
to a subfolder, those links and canonical URLs will need updating.
