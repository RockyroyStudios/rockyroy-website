# Rockyroy Studios website

A static site with no build step: plain HTML and CSS, hosted on GitHub Pages.

| Page | Path | Used for |
|---|---|---|
| Studio home | `/` | Organization website for Google Play account verification |
| Pesky Pest | `/pesky-pest/` | Game page and store-listing "website" field |
| Privacy Policy | `/privacy/` | Play Console privacy-policy URL and the in-game Privacy link |
| Terms of Use | `/terms/` | In-game Terms link |
| Support | `/support/` | In-game Support link and store-listing support details |

## Preview locally

Open `index.html` in a browser, or serve the folder:

```
python3 -m http.server 8000
```

## Publish on GitHub Pages

1. Create a new **public** GitHub repository, e.g. `rockyroy-website`. Keep it separate from the game repo.
2. Push the contents of this folder to its `main` branch.
3. In the repo, go to **Settings → Pages → Build and deployment**, choose *Deploy from a branch*, then `main` and `/ (root)`.
4. The site appears at `https://<github-user>.github.io/rockyroy-website/`. All pages use relative links, so they work there. Only `404.html` assumes the site is at the domain root, so it shows unstyled until the custom domain is set.

## When the domain is bought

1. In **Settings → Pages → Custom domain**, enter the domain (e.g. `rockyroystudios.com`). GitHub creates a `CNAME` file.
2. At the domain registrar, add GitHub's DNS records (four `A` records for the apex plus a `www` CNAME). See GitHub's "Managing a custom domain" docs.
3. Tick **Enforce HTTPS** once the certificate is issued.
4. Verify the domain in **Google Search Console**. Google's organization-account check needs a website you can prove you own.
5. Optional: set up an email address on the domain (e.g. `support@`) and swap it for the Gmail address across the pages (`grep -rl rockyroy.studios@gmail.com .`).

## Legal pages — current review status

The Privacy Policy and Terms pages are working drafts, not approved legal advice. Do not publish them as final or use them to make store declarations until the named legal operator, deployed SDKs, consent flow, retention terms and children’s handling have been verified. The Android test build currently uses GameAnalytics, Firebase Crashlytics and LevelPlay; the planned AdMob/UMP and Firebase Analytics changes are not yet implemented. Update these pages before enabling any new data flow.

## Before release

- [ ] **Legal name.** Once the business structure is chosen, name the legal owner in the Privacy Policy and Terms, e.g. "Rockyroy Studios, a sole proprietorship of [full legal name], [city], India". Use the exact name and address registered with Google Play.
- [ ] **Counsel review.** Have the Privacy Policy and Terms reviewed, especially the children's section. India's DPDP Act treats everyone under 18 as a child and requires verifiable parental consent. COPPA and the EU GDPR also apply if the game is offered in those regions. The game currently has no in-game consent or opt-out for adults; that decision is still open in the release checklist.
- [ ] **Re-check against the shipped build.** The Privacy Policy describes the 2 Oct 2026 code: age gate, GameAnalytics and Crashlytics for adults only, LevelPlay child-directed for under-18s, Firebase Analytics deactivated. Update it whenever SDKs, ad networks or data flows change, and keep Play Console Data Safety consistent with it.
- [ ] **app-ads.txt.** Once the domain is live, add the `app-ads.txt` lines from the LevelPlay dashboard at the site root, and enter the same domain as the developer website in Play Console.
- [ ] **Store link.** Replace "Coming soon to Google Play" on `/pesky-pest/` with the real Play Store link. Use Google's official badge artwork, following its brand guidelines.
- [ ] **Screenshots.** The current ones are from August 2026 and the gameplay shot shows pause-menu labels. Swap in the final store screenshots.
- [ ] **Game links.** Put the final URLs into `Assets/SlapTheFly/Scripts/UI/Settings/SettingsLinks.cs` (Privacy, Terms, Support, Rate).
