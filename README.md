# Co-Create Studios — Website

This is the website for Co-Create Studios (29 West Capitol Drive, Kapitolyo, Pasig).

It's a **single static page** — no server, no database, no install step. Everything
(markup, styling, and the scroll animation) lives in one file: `index.html`. That
makes it simple to host almost anywhere, and simple to break if you're not careful
editing it — so read the "Editing content" section before changing anything.

---

## 1. What's in this folder

```
index.html                 The entire site — HTML, CSS and JavaScript in one file
1.png                       The wing-mark logo shown top-left in the header
cocreate-reel.mp4           The looping hero video (used instead of the Instagram embed)
testimonials/                Client testimonial video clips
testimonials/thumbs/         Thumbnail images for those videos (shown before you click play)
```

`index.html` is a large file (a couple of MB) because a few fallback images are
embedded directly inside it as text. That's intentional — don't be alarmed when
you open it and see a huge wall of text partway through; just use your editor's
search (Ctrl/Cmd+F) to jump to what you need instead of scrolling.

---

## 2. Viewing it on your own computer

You technically *can* double-click `index.html` and it'll open in a browser, but
some browsers restrict video playback for files opened this way. It's more
reliable to serve the folder with a tiny local web server:

**Option A — Python (already installed on most Macs):**
```bash
cd "cocreate-site 2"
python3 -m http.server 8000
```
Then open `http://localhost:8000` in your browser.

**Option B — VS Code:**
Install the "Live Server" extension, right-click `index.html`, choose
"Open with Live Server."

**Option C — Node:**
```bash
npx serve .
```

Any of these let you preview exactly what visitors will see.

---

## 3. Putting it on your own domain

Because this is a plain static site, it will run on **any** web host — you are
not locked into a particular provider. Broadly, there are two kinds of hosting,
and either works fine:

### Option A: A modern static host (easiest, usually free)
Services like **Netlify**, **Vercel**, **Cloudflare Pages**, or **GitHub Pages**
let you drag-and-drop this folder and get a live URL in under a minute.

General steps (Netlify as an example — the others are nearly identical):

1. Create a free account at the host of your choice.
2. Drag this whole folder onto their "deploy" page (or connect a GitHub repo if
   you prefer version control).
3. You'll get a temporary URL like `yoursite.netlify.app` — confirm the site
   works there first.
4. In the host's dashboard, find **"Add custom domain"** and enter your domain
   (e.g. `cocreatestudios.ph`).
5. The host will show you one or two DNS records to add — usually either an
   **A record** (pointing to an IP address) or a **CNAME record** (pointing to
   something like `yoursite.netlify.app`).
6. Log into wherever you bought the domain (GoDaddy, Namecheap, Google Domains,
   etc.), open its DNS settings, and add exactly the records the host gave you.
7. Wait — DNS changes can take anywhere from a few minutes to ~48 hours to fully
   propagate. The host will usually show a green checkmark once it sees your
   domain pointing correctly, and will auto-issue a free HTTPS certificate.

### Option B: Traditional web hosting (cPanel / shared hosting)
If you already pay for hosting (common with providers aimed at the Philippines
market, e.g. Hostinger, Hostgator):

1. Log into your hosting control panel (often cPanel).
2. Open **File Manager**, navigate to `public_html` (the folder that serves your
   domain's root).
3. Upload every file and folder from this project into `public_html`
   (`index.html`, `1.png`, `cocreate-reel.mp4`, and the `testimonials/` folder)
   — or upload a zip and use "Extract."
4. If your domain is already registered with that same host, it usually works
   immediately. If the domain lives elsewhere, point its nameservers or DNS A
   record to your host — your hosting provider's support page will have the
   exact values.
5. Visit your domain to confirm it loads.

**Either way, make sure the `testimonials/` folder (with its `thumbs/`
subfolder) and `1.png` and `cocreate-reel.mp4` go up alongside `index.html` —
if those are missing, the videos/logo on the live site will be broken even
though the page itself still loads.**

---

## 4. Editing the content

Everything is inside `index.html`. Open it in a text editor and use
**search (Ctrl/Cmd+F)** for these landmarks rather than scrolling — the file is
long because of embedded fallback images.

| What you want to change | Search for this text |
|---|---|
| Logo in the top-left header | Replace the file `1.png` with a new image of the same name. Size is controlled by the `.brand-mark` CSS rule near the top of the file. |
| Hero headline / subheading | `A playground` |
| Address / about blurb | `29 West Capitol Drive` |
| Instagram link | `cocreatestudios.mnl` |
| Pricing (rates shown in the Booking section) | `Shoots, 6 hours` |
| Booking button link (currently Setmore) | `cocreatestudiosmnl.setmore.com` |
| Written reviews (the star-rating quotes) | `var REVIEWS` |
| Video testimonials (the carousel) | `var TESTIMONIALS` — see below |
| Hero looping video | The file `cocreate-reel.mp4` — replace it with a new clip of the same filename, or change the `EXTERNAL_MP4` variable to point at a different filename |

### Adding / changing a video testimonial
Find `var TESTIMONIALS` in `index.html`. Each entry looks like this:
```js
{ src:'testimonials/ADS 01 - SHEENA.mp4', poster:'testimonials/thumbs/sheena.jpg',
  name:'Sheena Gutierrez', role:'Coach for Designers, The Six Figure Designer Academy' },
```

- `src` — path to the video file inside the `testimonials/` folder
- `poster` — path to a thumbnail image inside `testimonials/thumbs/` (shown before
  the clip plays; without one it will try to use a video frame instead)
- `name` / `role` — the caption shown under the player

To add a new testimonial: drop the video file into `testimonials/`, generate a
thumbnail for it (any frame grab works — even a phone screenshot of the video
paused), drop that into `testimonials/thumbs/`, then add a new line to the
`TESTIMONIALS` array following the pattern above. To remove one, delete its line.

---

## 5. A couple of things worth knowing

- **No install step, no npm, no build.** Everything the page needs (fonts, the
  3D library used for the animated logo) loads from the internet automatically
  when someone visits — you don't need to install anything to deploy it.
- **The testimonial videos are large** (20–35MB each). That's fine for most
  hosts, but it does mean the testimonials section can be slow to load on weak
  mobile connections. If that becomes a problem, consider compressing the clips
  (e.g. with [HandBrake](https://handbrake.fr/) or `ffmpeg`) or hosting them on
  a video platform (YouTube/Vimeo unlisted, or a CDN) instead of serving the raw
  files yourself.
- **No WebGL fallback is automatic.** On very old browsers or devices that can't
  run the animated 3D logo, the site automatically switches to a simpler static
  layout — no action needed on your part.
# CoCreate
