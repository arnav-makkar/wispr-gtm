# Wispr India GTM — pitch site

One static page. No build step, no dependencies.

    public/index.html     the site
    public/preview.png    link preview card
    public/robots.txt     search engines told to stay out
    vercel.json           output directory + noindex headers

Everything Vercel serves lives in `public/`. Files at the repo root
(this README, vercel.json, .gitignore) are not deployed.

## Deploy

The repo is already initialised, committed, on `main`, and pointed at
`https://github.com/arnav-makkar/wispr-gtm.git`. One command:

    git push -u origin main

If GitHub rejects the push because the repo already has a commit
(you ticked "Add a README" when creating it):

    git pull --rebase origin main
    git push -u origin main

**Make the repo private** if it is not already. Settings > General >
Danger Zone > Change visibility. A public repo publishes the page
source on github.com whatever headers this config sets.

Then on vercel.com: Add New > Project > import `wispr-gtm`.
Framework Preset **Other**, build command empty. Output Directory is
already `public` via vercel.json. Deploy.

Commits are authored as `arnav-makkar <arnavm@edmo.education>`. If that
email is not on your GitHub account, the commit will show the name
without linking to your profile. To point it at the right address:

    git config user.email "<the email on your GitHub account>"
    git commit --amend --reset-author --no-edit

## The page is set to noindex

`robots.txt`, the `X-Robots-Tag` header in vercel.json, and a meta tag
in index.html all say the same thing. It will not appear in search.
Anyone with the link can open it, so treat the URL as the password.

To make it public later, remove all three and redeploy.

## One edit worth making after the first deploy

In `public/index.html`, `og:image` and `twitter:image` point at
`/preview.png`. Most link previewers resolve that, but WhatsApp and a
few others want an absolute URL. Once you know the domain, change both
to the full address:

    <meta property="og:image" content="https://your-domain.vercel.app/preview.png">
    <meta name="twitter:image" content="https://your-domain.vercel.app/preview.png">

## Updating the page

Replace `public/index.html`, commit, push. Vercel redeploys on every
push to `main` and keeps every previous deployment, so you can roll
back from the dashboard.
