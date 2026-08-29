# EnovaMaker.github.io

The page at <https://enovamaker.github.io>, and later at `www.enovamaker.com`.

One static file. No build step, no framework, no JavaScript, no external fonts, no analytics. A
page about running your own infrastructure should not pull resources from four other companies to
render itself, so the only things it loads are its own images.

---

## Editing

Change `index.html`, commit, push. GitHub Pages serves `main` directly and it is live in a minute
or two.

To check a change before pushing:

```sh
python3 -m http.server -d . 8000     # then open http://localhost:8000
```

### ⚠️ When you change an image, bump the version

The page loads images as `logo.png?v=2`, not `logo.png`. Browsers cache images aggressively, and
the file name does not change when the contents do — so anyone who has opened the page before
keeps seeing the old picture, with no way to know. Raising the number forces a refetch.

```html
src="logo.png?v=2"   →   src="logo.png?v=3"
```

This has already caught us once.

---

## The images

| File | Background | Use it for |
|---|---|---|
| `logo.png` | transparent | The web, anywhere you control the background |
| `mark.png` | transparent | The same, symbol only |
| `logo-white.png` | white, with margin | Word, PDF, slides, grant applications |
| `mark-white.png` | white, with margin | The same, symbol only |
| `avatar.png` | white, 500×500 | GitHub profile picture |
| `Logo1.JPG`, `Logo1b.jpg` | — | The originals. Untouched, keep them |

**Rule of thumb:** transparent where you choose the background, `-white` where you do not. A
transparent PNG in a viewer set to a dark theme is drawn on black, which is why the logo looks
wrong on disk and right on the page.

`avatar.png` is centred on the mark's own bounding box rather than the image's — the mark was
cropped off-centre from a larger picture — and scaled so its corner sits 237px from the middle,
inside the 250 that GitHub's circular crop leaves. Upload it at
**Settings → Profile → Edit → Upload a photo**.

### How the cut-outs were made

Both sources are photographs of signage on a grey wall. Two signals separate the logo from it:
the orange is **saturated** and the navy is **dark**, while the wall is light and desaturated and
its drop shadow is mid-grey — so the shadow falls outside both tests and disappears for free.

Only a 3px median filter after that. An earlier attempt used a 7px morphological close to fill
holes, which merged and then ate the tagline: `INNOVATION · FABRICATION · CREATION` is navy type
three or four pixels wide. Whatever you do to the mask, keep it smaller than the thinnest stroke.

A faint light fringe remains along the letters. It is invisible on white, and it is the reason
the logo sits on a white card in dark mode rather than floating on the dark ground.

---

## Pointing the domains here

**`enovamaker.com` is the primary.** The funders are international and it is the address that goes
in the repositories and on the sponsorship page.

**The `.pt` cannot also be a custom domain.** A repository's `CNAME` file holds exactly one, so
`enovamaker.pt` gets a redirect at the registrar instead. That costs nothing and needs no hosting.

### 1. DNS for `enovamaker.com`

```
CNAME   www    enovamaker.github.io.          ← trailing dot

A       @      185.199.108.153
A       @      185.199.109.153
A       @      185.199.110.153
A       @      185.199.111.153
AAAA    @      2606:50c0:8000::153
AAAA    @      2606:50c0:8001::153
AAAA    @      2606:50c0:8002::153
AAAA    @      2606:50c0:8003::153
```

### 2. Verify the domain first — Settings → Pages → Verify domain

Add the `TXT` record GitHub gives you. This stops anyone else claiming the domain on their own
repository if this site is ever disabled. GitHub's own documentation asks for it "to improve
security and avoid takeover attacks", and almost nobody does it.

### 3. Settings → Pages → Custom domain → `www.enovamaker.com`

Set **only** the `www`. With the apex A/AAAA records in place, GitHub creates the
`enovamaker.com` → `www.enovamaker.com` redirect itself. Upstream recommends the `www` form
because "www subdomains are not affected by changes to the IP addresses of GitHub's servers" —
the four addresses above can change one day; the CNAME will not.

### 4. Tick **Enforce HTTPS**

The box stays greyed out for a few minutes while the certificate is issued. That is normal.

### 5. Redirect the `.pt` at its registrar

```
enovamaker.pt  →  https://www.enovamaker.com     301, permanent
```

Look for "URL forwarding" or "Web forwarding". Most registrars include it.

---

## ⚠️ Keep this away from the Tor bridge

Do not point the bridge's domain here, and do not put the bridge on a subdomain of this one.

The bridge's domain is **expected** to be blocked — that is what happens to a bridge that works —
and blocking is often applied to the whole DNS zone. A subdomain would take the company's site and
mail down with it. The bridge's cover site also has to be served by the bridge host itself, or the
bridge does not work at all.

Two names, two machines, no link between them.

---

## Things this page deliberately does not say

**It does not call EnovaMaker a company.** It is not incorporated yet, and the grant applications
are made by an individual. A page claiming otherwise contradicts them, and funders check.

**It does not claim a professional title.** *Engenheiro* is protected in Portugal. The page says
what the work is, not what the person is called.

**Each module says `working` or `design`.** Two ship code; six are published designs. A visitor who
clones one and finds an empty flake should have been told so here first.
