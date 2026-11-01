# Akilivo Mathematics

**Working name:** Akilivo (availability checks are pending)  
**Tagline:** Learn smarter. Rise higher.

A responsive, Mathematics-first learning app prototype. The current version runs entirely in a browser and stores its question bank, practice history and settings in that browser's local storage.

## Run it on Windows 11

1. Download or copy this `akilivo` folder to your computer.
2. Open the folder in Visual Studio Code.
3. Open `index.html` in a browser. For a smoother development workflow, install the free **Live Server** extension in VS Code, right-click `index.html`, and choose **Open with Live Server**.
4. Try a Mathematics session from **Practice**. Open **Question studio** to create a draft, review its answer and worked solution, then publish it into the local practice bank.

No build step, paid service, API key, account, or install is needed for this local preview. Google Fonts are optional; the app falls back to system fonts if unavailable.

## What works now

- Responsive student overview, topic selection, timed practice, automatic marking, answer review with worked steps, and practice history.
- A local question studio to create, edit, and publish or unpublish questions. New questions begin as drafts.
- A prompt helper that prepares an AI question-generation prompt for copying into an AI tool you choose. It does not call an AI API or publish generated content.
- A social links panel for YouTube, Facebook, TikTok and a WhatsApp Channel. The cards remain marked “Link coming soon” until the public URLs are set in `socialLinks` near the top of `app.js`.
- Example Mathematics questions are included as starter content. Review and replace them with curriculum-checked content before real classroom use.
- Browser-local persistence. Clearing browser data or switching browsers/devices will remove or leave behind this local data; it does not sync.

## Not connected yet

There is no cloud database, shared question bank, secure admin login, student account, cross-device progress sync, payment system, or AI API integration in this prototype. The studio is visible to anyone who can open this local app; it is **not** a secure private dashboard. Do not put confidential student data or credentials into it.

### Social links and WhatsApp privacy

Add your public YouTube channel, Facebook page, and TikTok profile URLs to the `socialLinks` object in `app.js`. For WhatsApp, create a **Channel** and use its invite URL (`https://whatsapp.com/channel/...`); do not use a `wa.me` or click-to-chat URL, since those are phone-number chat links. WhatsApp says Channel followers will not see the admin's phone number, though admins may see profile details for followers who are already their contacts. Channels are one-way updates, so students cannot message you directly there. See [WhatsApp's Channel privacy details](https://faq.whatsapp.com/1318001139066835) and [how to create and share a Channel](https://faq.whatsapp.com/794229125227200/).

## Suggested low-cost path to a shared web and Android app

The prototype is intentionally plain HTML, CSS and JavaScript so it can be opened and understood without a toolchain. For a production version, move the UI into a maintained web framework (for example, React with Vite) and wrap the same responsive web client with **Capacitor** for Android. Both clients should use one HTTPS API and shared PostgreSQL database rather than maintaining separate question banks. A managed Postgres service such as Supabase can be evaluated for a free-friendly initial tier; check current limits and terms before committing.

Suggested backend boundaries:

- `profiles`: authenticated user id, display name, role, and school/grade fields as appropriate. Roles must be enforced by server-side authorization, not by a browser flag.
- `questions`: topic, grade, difficulty, prompt, answer, worked steps, status (`draft`, `in_review`, `published`, `archived`), author/reviewer ids, timestamps, and a version number.
- `attempts` and `attempt_answers`: student id, question/version ids, submitted answer, correctness, duration, and session timestamp. Restrict each student to their own records.
- `question_reviews`: reviewer, decision, notes and timestamp. Keep an audit trail for edits and publication.
- Private admin APIs for question creation/review/publication; student APIs return published questions only. Apply row-level access controls and validate input on the server.

Keep answers and marking rules on a protected API for high-stakes exams; in a practice app, decide deliberately whether downloaded questions can expose answers. Add backups, rate limits, privacy/retention rules and account recovery before onboarding real students. Do not collect sensitive learner data until those choices are implemented and explained.

### AI workflow when the backend exists

An authenticated admin requests a draft from a server-side function. Store the model, prompt/version and generated output as `draft`; never expose the provider key in the app or browser. A human reviewer checks curriculum fit, mathematical correctness, clarity, difficulty and solution steps, then explicitly approves publication. Retain the generated draft and review history. The local prompt helper in this prototype only copies text and is not connected to a provider.

### Android packaging path

After the web app has a production build and API configuration, install Node.js LTS, then in the project run `npm create vite@latest` (choose React if moving to React), add Capacitor (`npm install @capacitor/core @capacitor/cli`, then `npx cap init`), build the web client, add Android (`npm install @capacitor/android`, `npx cap add android`) and sync (`npx cap sync android`). Open the generated Android project in Android Studio to build and sign an APK/AAB. These steps are a future migration path; this static prototype does not yet contain a Capacitor project. Keep Android and web pointed at the same API.

## Next implementation steps

1. Agree on the curriculum/content source and review workflow; replace starter questions with verified content.
2. Choose hosting and configure the shared database, migrations, backups and access policies.
3. Add real student and admin authentication, server-enforced roles, and cloud persistence; migrate local progress only with a user-controlled import/export flow.
4. Add the server-side AI draft provider, secret management, review queue and audit history.
5. Add accessibility and device checks, then package the web client for Android with Capacitor.
6. Complete Akilivo name, domain and trademark checks before public launch.

For publishing the current static preview and setting up automatic updates, follow [DEPLOY.md](DEPLOY.md).

## Project files

- `index.html` — app structure and screens
- `styles.css` — responsive visual design
- `app.js` — question data, local practice flow and local studio
