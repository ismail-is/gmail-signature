# Xeenx — Gmail Email Signature Package

## What's included
```
signature.html
assets/
  banner.jpg
  email.png
  website.png
  location.png
  linkedin.png
  x.png
  youtube.png
  facebook.png
  instagram.png
```

## Why the images use URLs, not local file paths
Gmail, Outlook, Apple Mail, and Yahoo Mail do **not** load images from your
local computer or from `assets/` folder paths — signature images must be
hosted on a **public web server** (your own domain, a CDN, or an image host)
so every recipient's email client can fetch them. This is standard practice
for every email signature in existence.

## Step 1 — Upload the images
Upload the entire `assets/` folder to a public location, for example:
- Your website server: `https://www.xeenx.de/email-signature/assets/`
- A CDN / S3 bucket / Cloudinary / Imgur (any direct-link image host)

Each image must be reachable as a direct `.jpg` / `.png` URL (open the link
in an incognito browser tab — you should see only the image, nothing else).

## Step 2 — Replace the image URLs in signature.html
The HTML currently uses placeholder URLs in this format:
```
https://www.xeenx.de/email-signature/assets/[filename]
```
Find and replace **every occurrence** of
`https://www.xeenx.de/email-signature/assets/` with the real base URL where
you uploaded your `assets/` folder.

### Exactly where the banner URL is
Search for this line near the bottom of `signature.html` (inside the last
`<tr>`, the full-width banner row):
```html
<img src="https://www.xeenx.de/email-signature/assets/banner.jpg" width="720" ...>
```
Replace `https://www.xeenx.de/email-signature/assets/banner.jpg` with the
live URL of your uploaded `banner.jpg`.

### Exactly where each icon URL is
Each social icon and each contact icon has its own `<img src="...">` tag:

| Icon | Line to find |
|---|---|
| LinkedIn | `src="https://www.xeenx.de/email-signature/assets/linkedin.png"` |
| X | `src="https://www.xeenx.de/email-signature/assets/x.png"` |
| YouTube | `src="https://www.xeenx.de/email-signature/assets/youtube.png"` |
| Facebook | `src="https://www.xeenx.de/email-signature/assets/facebook.png"` |
| Instagram | `src="https://www.xeenx.de/email-signature/assets/instagram.png"` |
| Email icon | `src="https://www.xeenx.de/email-signature/assets/email.png"` |
| Website icon | `src="https://www.xeenx.de/email-signature/assets/website.png"` |
| Location icon | `src="https://www.xeenx.de/email-signature/assets/location.png"` |

Replace each with the real hosted URL of that file.

## About the icon PNGs included
The 8 icon PNGs in `assets/` are clean, blue (#4A4DD6), 24x24px, transparent-
background placeholder icons (envelope, globe, pin, LinkedIn "in", X, YouTube
play button, Facebook "f", Instagram camera) built to match the reference
design's color and sizing exactly. If you have official brand-guideline
social icons you'd prefer instead, simply replace the PNG files in
`assets/` with your own — **keep the same filenames** and no HTML edits are
needed, only re-upload.

## About banner.jpg
`banner.jpg` was cropped and exported directly from your reference design
(the bottom "END-TO-END CREATIVE STUDIO FOR AMBITIOUS BUSINESSES" panel),
sized at 1440px wide (retina-ready for a 720px display width) so it stays
sharp on high-density displays without distortion.

## Step 3 — Install in Gmail
1. Open **Gmail → Settings (gear icon) → See all settings**
2. Go to the **General** tab → scroll to **Signature**
3. Click **Create new**, name it, then:
   - Open `signature.html` in a browser
   - Select all the rendered signature content (not the raw code) → Copy
   - Paste into the Gmail signature box
4. Scroll down → set this signature as default for new emails / replies
5. Click **Save Changes**

> Tip: If pasting from a browser strips styling, you can instead paste the
> rendered HTML through the **Insert HTML** trick using a temporary Google
> Doc, or use a Chrome extension such as "Gmail Signature Uploader" —
> Gmail's compose box itself does not accept raw HTML/code paste.

## Technical notes
- Built entirely with **HTML tables** and **inline CSS** — no Flexbox, Grid,
  position:absolute, external CSS, JavaScript, or SVG.
- All social/contact icons are individually clickable and open in a new tab
  (`target="_blank"`).
- Layout is fixed at **720px max-width**, centered, and degrades gracefully
  on narrow/mobile mail clients (table cells wrap naturally; no broken
  layout).
- Tested structure follows Gmail/Outlook-safe patterns: `role="presentation"`
  tables, `cellpadding`/`cellspacing`/`border="0"`, explicit `width`/`height`
  on every image, and `display:block` on all `<img>` tags to prevent
  unwanted spacing in Outlook/Gmail.
