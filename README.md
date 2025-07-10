# FSDH Redirector Service

A simple static-site toolchain to generate and serve tracked, secure redirects via GitHub Pages.

**Purpose**

* Maintain a centrally managed list of approved destination URLs in `allowed.json`.
* Provide an interactive form (`generate.html`) for users to generate UTM‑tagged redirect links.
* Enforce domain/URL whitelisting in the redirect logic (`index.html`).
* Track every redirect in Google Analytics before handing off users to the final destination.

---

## 📁 Repository Structure

```
├── allowed.json          # Whitelist of fully-qualified URLs
├── generate.html         # Interactive redirect‑link generator UI
├── index.html            # Secure redirect page with GA tracking
├── README.md             # This documentation
├── .github/              # CI/CD, linting, security workflows
└── renovate.json         # Dependency update config
```

---

## 🚀 Quick Start

1. **Web Editor**: Navigate to this repository on GitHub and press the `.` key to open the cloud IDE.
2. **Add URL**: In the web editor, open `allowed.json` and add your destination URL to the `allowed_urls` array.
3. **Commit & PR**: Commit your changes (directly or via a branch) and open a Pull Request against `main` to approve new URLs.
4. **Deploy**: Once merged, GitHub Pages will automatically deploy your updates.
5. **Generate**: Open `generate.html` to build UTM-tagged redirect links.
6. **Track & Redirect**: Visitors clicking those links will hit `index.html`, fire a GA event, then be forwarded to the allowed URL.

---

## ✏️ Adding a New Allowed URL

1. Open `allowed.json` in the repository root.
2. Add your new, fully URL‑encoded destination to the `allowed_urls` array:

   ```json
   {
     "allowed_urls": [
       "https://example.com/page?utm_source=...",
       "https://another.allowed.site/path"
     ]
   }
   ```
3. Create a Pull Request targeting `main`:

   * Title: \*\*Add allowed URL: \*\***`<your URL>`**
   * Body: short description and reason for the redirect.
4. After review and merge, your URL is live and can be used in `generate.html`.

---

## 🛠 Generating Redirect Links

1. Open **generate.html** in your browser (e.g. via GitHub Pages).
2. Enter:

   * **Destination URL** (must match an entry in `allowed.json`).
   * **UTM parameters** (source, medium, campaign, etc.).
3. Click **Generate Link**.
4. The full redirect URL (pointing to `index.html?…`) is produced and auto‑copied to your clipboard.
5. Share that link in your newsletter, email, or other channels.

---

## 🔒 Secure Redirect Logic

* `index.html` fetches `allowed.json` at runtime.
* It rejects any `redirect-url` not exactly listed in `allowed_urls`.
* Fires the GA `gtag('config',…)` call with campaign data.
* Redirects only valid, whitelisted URLs after a short delay.

---

## 📦 Deployment

* Written as a fully static site.
* GitHub Actions workflow (`.github/workflows/deploy-static.yml`) auto‑deploys on every `main` push.
* SSL and custom domain support via GitHub Pages settings.
