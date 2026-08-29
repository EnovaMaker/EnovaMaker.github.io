# EnovaMaker.github.io

The page at <https://enovamaker.github.io>, and later at `enovamaker.com`.

One static file. No build step, no framework, no JavaScript, no external fonts, no analytics —
the wordmark is drawn in inline SVG and the type is the system stack. A page about running your
own infrastructure should not be pulling resources from four other companies to render itself.

## Editing

Change `index.html`, commit, push. GitHub Pages serves `main` directly; it is live within a
minute or two.

## Pointing `enovamaker.com` here

Once the domain is registered, at the registrar's DNS:

```
A     @    185.199.108.153
A     @    185.199.109.153
A     @    185.199.110.153
A     @    185.199.111.153
AAAA  @    2606:50c0:8000::153
AAAA  @    2606:50c0:8001::153
AAAA  @    2606:50c0:8002::153
AAAA  @    2606:50c0:8003::153
CNAME www  enovamaker.github.io.
```

Then Settings → Pages → Custom domain → `enovamaker.com`, and tick **Enforce HTTPS** once the
certificate has issued (it takes a few minutes, and the tickbox stays greyed out until then).

⚠️ Do not point the Tor bridge's domain here, or any subdomain of this one at the bridge. The
bridge's domain is expected to be blocked, blocking often lands at the level of the whole DNS
zone, and the cover site has to be served by the bridge host itself.

## Checking a change before pushing

```sh
python3 -m http.server -d . 8000    # then open http://localhost:8000
```
