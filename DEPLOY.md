# Publish Akilivo as a preview

This is a static preview of the app. It can be shared by URL after publishing. It currently has no student accounts, shared database, secure admin sign-in, or cross-device history, so do not treat it as the finished production learning service.

## Recommended launch path

Use a private GitHub repository connected to Cloudflare Pages. Cloudflare can deploy the static site from Git and automatically publish future changes pushed to the production branch. The Pages project must be created with Git integration from the start; Cloudflare does not allow converting a Direct Upload project into a Git-integrated project later. See [Cloudflare's static HTML deployment guide](https://developers.cloudflare.com/pages/framework-guides/deploy-anything/) and [Git integration guide](https://developers.cloudflare.com/pages/get-started/git-integration/).

## First publish

1. Sign in to or create your own GitHub account, then create a **private** repository named `akilivo-mathematics` (or another name you prefer). Do not include passwords, API keys, student records or other private information in the repository.
2. In Cloudflare, open **Workers & Pages → Create application → Pages → Connect to Git**. Sign in to GitHub, authorize Cloudflare for the new repository, and select it.
3. Set the production branch to `main`. Leave the framework preset unselected and leave the build command blank. Use the repository root as the build output (or use `.` if the screen requires a value). The root contains `index.html`.
4. Deploy. Cloudflare will provide a `*.pages.dev` preview URL. A custom domain is optional and requires a domain you own.
5. Open that URL on a phone and computer. Check practice and the content studio before sharing it with students; the studio is not protected by sign-in yet.

The GitHub and Cloudflare accounts must belong to you. Never send account passwords or API tokens in chat. I can continue the setup after you have created the private repository and connected the provider, or guide you through each screen.

## Ongoing updates

Keep the code in the GitHub repository. Each reviewed update pushed to `main` will trigger a new Pages deployment; Cloudflare also provides preview deployments for pull requests. Keep a copy of the current project before accepting a major change. Update `app.js` social links when you are ready to share your channel URLs.

For a public production launch later, first add server-enforced admin/student authentication, a shared database, backups, reviewed curriculum content and privacy/retention information. The current browser-local question studio is available to anyone who opens the preview; it does not update a shared question bank.
