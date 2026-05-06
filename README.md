# Reels for Estates — Tiers Landing Page

Static HTML landing page that pitches the listing-video service across 5 tiers (Stages 1-5).
Built for GitHub Pages — zero build step, just static files.

## Live URL

After enabling Pages: `https://<your-github-username>.github.io/realestate-tiers-landing/`

## Setup (60 seconds — one-time)

### 1. Get your form access key

The booking form uses [Web3Forms](https://web3forms.com) (free, unlimited submissions, no signup beyond email verification).

1. Go to **https://web3forms.com/create-access-key**
2. Enter the email address you want bookings sent to (your Gmail works)
3. Click **"Create Access Key"** — you'll get an access key emailed in seconds
4. Open `index.html`, find the line:
   ```html
   <input type="hidden" name="access_key" value="REPLACE_WITH_WEB3FORMS_ACCESS_KEY" />
   ```
5. Replace `REPLACE_WITH_WEB3FORMS_ACCESS_KEY` with the key you got
6. Commit and push — done. Bookings now land in your inbox.

### 2. Update the contact email in the footer

Find `rob@yourdomain.co.uk` in the JS error fallback near the bottom of `index.html` and swap it for your real email.

## Adding new tiers (Stages 3, 4, 5)

When you lock in a new tier:

1. **Add the demo videos** to `videos/` (web-optimised — see "Re-encoding videos" below)
2. **Replace the placeholder card** in the "Coming soon" section with a full `<section class="stage">` block — copy the structure from Stage 1 or Stage 2
3. **Update the tier strip** at the top — change `class="tier-card-mini ghost"` to `class="tier-card-mini"` and fill in the price + tagline
4. Commit and push

## Re-encoding videos for web

All demo videos in `videos/` are pre-optimised. If you add new ones, run:

```bash
ffmpeg -i source.mp4 -vcodec libx264 -crf 24 -preset fast -movflags +faststart -acodec aac -b:a 96k web-optimised.mp4
```

Targets: ~5-15 MB per 30-60s vertical reel. Anything bigger will slow page load.

## Local preview

```bash
cd realestate-tiers-landing
python -m http.server 8000
# open http://localhost:8000
```

Or just double-click `index.html` — works without a server.

## Deploy to GitHub Pages

```bash
gh repo create realestate-tiers-landing --public --source . --push
gh api repos/:owner/realestate-tiers-landing/pages -f source[branch]=main -f source[path]=/ -X POST
```

Pages takes ~1 minute to publish. URL printed on first push.

## File map

```
index.html            ← the landing page
videos/
  stage1-hook.mp4     ← Stage 1 V1 demo (28s, ~10 MB)
  stage1-tour.mp4     ← Stage 1 V2 demo (43s, ~13 MB)
  stage1-pick.mp4     ← Stage 1 V3 demo (40s, ~9 MB)
  stage2-hook.mp4     ← Stage 2 V1 demo HD (28s, ~6 MB)
  stage2-tour.mp4     ← Stage 2 V2 demo HD with morphs (54s, ~10 MB)
  stage2-pick.mp4     ← Stage 2 V3 demo HD (40s, ~4 MB)
img/                  ← (placeholder for og:image, brand logos)
```

## Design tokens

- **Cream palette** (matches Stage 2 video backgrounds): `#f8f5f0` → `#efeadd`
- **Navy** (text + CTAs): `#1a2b4a`
- **Sand gold** (accents, prices): `#c9a86a`
- **Sage** (success ticks, subtle highlights): `#9eab91`
- **Headings:** Playfair Display 700
- **Body:** Inter 400

These mirror the Wilton Road demo videos so the whole pitch feels cohesive.
