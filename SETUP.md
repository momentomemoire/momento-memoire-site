# Getting your site live with an admin panel

This is a one-time setup (about 15 minutes, all done by clicking — no code).
After this, your website manager will log in at **yoursite.netlify.app/admin**
and upload videos, photos, and captions themselves, forever.

## What you're setting up

- **Netlify** — free hosting for the website itself
- **GitHub** — free storage for the website's files (this is what powers the "Undo/history" of every edit)
- **Netlify Identity + Git Gateway** — turns GitHub into a simple login-and-upload panel your manager never has to understand

---

## Step 1 — Put the files on GitHub

1. Go to [github.com](https://github.com) and create a free account if you don't have one.
2. Click the **+** in the top right → **New repository**. Name it something like `momento-memoire-site`. Keep it **Public** or **Private**, either works. Click **Create repository**.
3. On the new repo page, click **uploading an existing file**.
4. Drag in *all* the files and folders from this project (`index.html`, `admin/`, `content/`, `netlify.toml`) keeping the folder structure intact, then click **Commit changes**.

## Step 2 — Deploy on Netlify

1. Go to [netlify.com](https://netlify.com) and sign up free — choose **"Sign up with GitHub"** to link the two automatically.
2. Click **Add new site → Import an existing project**.
3. Choose **GitHub**, then pick the `momento-memoire-site` repository.
4. Leave the build settings as they are (no build command needed) and click **Deploy site**.
5. Netlify gives you a free web address like `random-name-123.netlify.app`. You can rename it: **Site settings → Change site name**.

## Step 3 — Turn on the login system (Identity)

1. In your site's Netlify dashboard, go to **Site configuration → Identity** and click **Enable Identity**.
2. Under **Registration**, set it to **Invite only** (so random people can't sign up).
3. Scroll to **Services → Git Gateway** and click **Enable Git Gateway**. This is what lets the admin panel save changes without your manager ever touching GitHub.

## Step 4 — Fix one setting in the CMS config

1. On GitHub, open `admin/config.yml` and click the pencil (edit) icon.
2. Replace both lines that say `https://your-site-name.netlify.app` with your real Netlify address from Step 2.
3. Commit the change. Netlify will redeploy automatically (takes ~1 minute).

## Step 5 — Invite your website manager

1. In Netlify: **Site configuration → Identity → Invite users**.
2. Enter their email address. They'll get an email with a link to set a password.
3. That's it — they now log in at `yoursite.netlify.app/admin`.

---

## What your manager will see

A simple dashboard with two sections:

- **🎬 Reels (Videos)** — add/remove video blocks, paste a YouTube/Vimeo/Facebook/Instagram link, set the category, duration, and short description.
- **🖼️ Albums (Category / Event)** — add/remove albums, set category and date, upload photos with captions.
- **👥 Team** — add/remove team members, upload a photo, and set their hierarchy level (Leadership / Core Crew / Associates) from a dropdown — this controls how prominently they appear on the site automatically.

Every change they publish updates the live site automatically within about a minute — no code, no developer needed.

## Notes

- **Videos are links, not uploads:** in the Reels editor, paste the video's page link — from YouTube, Vimeo, Facebook, or Instagram — into the "Video link" field. The site detects which platform it's from and embeds the player automatically. Nothing to upload, no file size limits.
  - YouTube / Vimeo / Facebook: plays inline in the popup with sound and controls.
  - Instagram: opens as an embedded post card (Instagram doesn't allow a plain video-only embed); there's also an "Open on Instagram" link underneath in case the embed doesn't load.
  - Make sure the post/video is set to **Public** on that platform, or visitors won't be able to view it.
- **Previewing locally:** because the site loads `content/reels.json` and `content/albums.json` dynamically, double-clicking `index.html` on your computer will show placeholder demo content instead of live data (browsers block that kind of file loading offline). Once deployed on Netlify this isn't an issue.
