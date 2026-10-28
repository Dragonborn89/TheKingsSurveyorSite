# Publishing thekingssurveyor.com (one-time setup)

Alex does every step here himself; nothing in this folder is live until it is pushed.

## 1. Create the repo and push (10 minutes)

On GitHub: New repository, name `TheKingsSurveyorSite`, public, no README (this folder has one). Then from this folder:

```
cd D:\Devgit\TheKingsSurveyorSite
git init
git add .
git commit -m "The King's Surveyor one-page site"
git branch -M main
git remote add origin https://github.com/Dragonborn89/TheKingsSurveyorSite.git
git push -u origin main
```

## 2. Turn on GitHub Pages (2 minutes)

Repo Settings, Pages. Source: Deploy from a branch. Branch: main, folder: / (root). Save.
Under Custom domain it should already read `thekingssurveyor.com` because of the CNAME file; if not, type it and Save.
Leave "Enforce HTTPS" unticked until DNS has propagated (step 3), then come back and tick it.

## 3. DNS at IONOS (5 minutes, then wait up to an hour)

Domains, thekingssurveyor.com, DNS. First REMOVE the existing forward to Steam (Forwarding section) and any A or CNAME record IONOS created for it. Then add:

| Type  | Host | Value                   |
|-------|------|-------------------------|
| A     | @    | 185.199.108.153         |
| A     | @    | 185.199.109.153         |
| A     | @    | 185.199.110.153         |
| A     | @    | 185.199.111.153         |
| CNAME | www  | dragonborn89.github.io  |

Check with `nslookup thekingssurveyor.com` from a terminal: it should return the four 185.199.x.153 addresses. Then back in GitHub Pages, tick Enforce HTTPS (the certificate takes a few minutes after DNS is right).

## 4. Google Search Console (5 minutes)

search.google.com/search-console, Add property, Domain: `thekingssurveyor.com`. It gives you a TXT record to add at IONOS (same DNS screen). Once verified: Sitemaps, submit `https://thekingssurveyor.com/sitemap.xml`. Then URL Inspection, paste `https://thekingssurveyor.com/`, Request Indexing.

## 5. After it is live

- Replace the Steam link in the X bio with the site? No. Keep the Steam link in the bio for launch week; the site links to Steam anyway.
- Add the site URL to the Steam page (Steamworks, Store Page Admin, Basic Info, Website) so Steam links back to it.
- Add it to the YouTube channel links and the Substack About page.
- Fact sheet: add `Website: https://thekingssurveyor.com` under the Steam page line.

## Updating the page later

Edit `index.html`, commit, push. Pages redeploys in about a minute. Images come from the press kit; rebuild them there, do not edit the copies in `assets/`.
