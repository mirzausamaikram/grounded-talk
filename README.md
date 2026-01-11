# Peer Listening Site — Deploy to Vercel & Push to GitHub

This repo is a single-page static site (HTML/CSS/JS). It includes a `vercel.json` that adds security/privacy headers on Vercel.

## Prepare Git locally

```powershell
cd C:\Users\mirza\Desktop\Working
git init
git add .
git commit -m "Initial site + security headers"
```

## Create a GitHub repo and push

1. Create a new GitHub repository (public or private).
2. Add it as a remote and push:

```powershell
git remote add origin https://github.com/<your-user>/<your-repo>.git
git branch -M main
git push -u origin main
```

## Deploy on Vercel

Option A — Import from GitHub (recommended)
- Go to https://vercel.com/new and import your repo.
- Vercel auto-detects a static site and deploys it.
- `vercel.json` will apply security headers globally.

Option B — CLI deploy (direct)
```powershell
npm i -g vercel
vercel login
vercel --prod
```

## Verify security headers

Once deployed, check headers:

```powershell
# Replace with your deployed URL
iwr https://<your-vercel-app>.vercel.app -Headers
```
Expect to see:
- `Strict-Transport-Security`
- `Content-Security-Policy`
- `Referrer-Policy`
- `X-Frame-Options`, `X-Content-Type-Options`
- `Permissions-Policy`

## Notes on Content Security Policy (CSP)
Current CSP allows inline CSS/JS (`'unsafe-inline'`) because the page uses inline styles/scripts. For a stricter CSP:
- Move inline styles into CSS files, and inline scripts into JS files.
- Update CSP to remove `'unsafe-inline'`.

## Custom domain
- Add your domain in Vercel project settings and set DNS to Vercel.
- Enable HSTS preload if desired (already enabled via headers).

## Next steps
- Replace placeholder links (Calendly, Instagram/TikTok/WhatsApp, Feedback form).
- Add a simple privacy policy page/section if you plan to collect data.
