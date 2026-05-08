# Deployment

The site deploys automatically to GitHub Pages on every push to `main` via `.github/workflows/deploy.yml`.

## How it works

1. GitHub Actions runs `npm ci && npm run build`
2. The `dist/` folder is uploaded as a Pages artifact
3. GitHub Pages serves it at `peterbacalso.com`

`public/CNAME` contains the custom domain and is copied into `dist/` at build time.

## One-time GitHub setup

1. **Repo Settings → Pages → Source**: set to **GitHub Actions**
2. **Repo Settings → Pages → Custom domain**: enter `peterbacalso.com`

## DNS setup (at your registrar)

For an apex domain (`peterbacalso.com`, no `www`), add these A records pointing to GitHub Pages:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Or add a `CNAME` record for `www` → `peterbacalso.github.io` and redirect the apex to `www`.

GitHub's canonical reference: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## Manual deploy

To trigger a deploy without a commit, go to **Actions → Deploy to GitHub Pages → Run workflow**.

## Local preview of production build

```bash
npm run build && npm run preview   # http://localhost:4321
```
