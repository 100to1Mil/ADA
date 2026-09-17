# The Auto Detailing Academy — Website

Plain HTML/CSS, no build step, no dependencies. Ready to host on GitHub Pages.

## Files
- `index.html` — homepage
- `about.html` — about page
- `downloads/quick-start-playbook.pdf` — the lead magnet PDF

## How to put this on GitHub Pages

1. Go to github.com and create a new repository (e.g. `auto-detailing-academy`). Public repo, no README/license needed — you already have these files.
2. Upload all three items in this folder (`index.html`, `about.html`, `downloads/`) to the repo — either drag-and-drop on the GitHub website ("Add file" → "Upload files") or via git if you're comfortable with it.
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set Source to **Deploy from a branch**, Branch to **main**, folder to **/(root)**. Save.
5. GitHub gives you a live URL, usually `https://yourusername.github.io/auto-detailing-academy/` — it takes a minute or two to go live after the first deploy.
6. (Optional) If you want your own domain (e.g. theautodetailingacademy.com) instead of the github.io link, add a `CNAME` file with your domain name in it, and point your domain's DNS at GitHub's servers — happy to walk through this when you're ready.

## The email forms don't send anywhere yet

GitHub Pages only hosts static files — it can't receive form submissions on its own. The simplest fix without any backend code is a free service like **Formspree**: you sign up, get a form endpoint URL, and I just swap the form's `action` attribute to point at it. Emails start landing in your inbox (or a spreadsheet) same day. Say the word and I'll wire it up.

## Making the Playbook actually send automatically

Right now, submitting the form does two things: notifies you (via Formspree) and takes the visitor to `thank-you.html`, which has a direct download button for the Playbook — so nobody's left empty-handed.

To make Formspree **email the Playbook to them automatically**, turn on the Autoresponse plugin:

1. In your Formspree dashboard, open the "ADA Playbook Signup" form.
2. Go to the **Workflow** tab → **Actions** → **+ Add New** → **Auto Response**.
3. Set the subject (e.g. "Your Quick-Start Playbook") and write a short message with a link to the PDF.
4. Once your site has a live URL (GitHub Pages link or your custom domain), the download link in that email needs to be the *full* address — e.g. `https://theautodetailingacademy.com/downloads/quick-start-playbook.pdf` — not a relative path, since it's going out in an email, not loading on your site.

Formspree's autoresponder sends a text email with a link, not an attached file — which is actually fine (and standard) here, since it means the file's easy to update later without needing to change what's been "sent."

## Using ada.thepreproom.academy as the domain

This repo includes a `CNAME` file (already set to `ada.thepreproom.academy`) — GitHub Pages reads that file automatically once you upload it, so you don't need to type the domain into the Pages settings UI yourself, though it'll also show up there once DNS is confirmed.

Two things need to happen:

1. **Upload the `CNAME` file along with everything else** to the repo (root level, no file extension).
2. **Add a DNS record for the `ada` subdomain**, wherever `thepreproom.academy`'s DNS is managed (check your domain registrar first — if DNS wasn't specifically pointed at Netlify, it's likely still at your registrar):
   - Type: **CNAME**
   - Host/Name: **ada**
   - Value/Target: **yourusername.github.io** (your actual GitHub username, not the repo name)
   - TTL: default is fine

DNS changes can take anywhere from a few minutes to a few hours to propagate. Once it does, `ada.thepreproom.academy` will point straight at this site — and `thepreproom.academy` itself (and The Preproom app on Netlify) stays completely untouched, since subdomains route independently.
