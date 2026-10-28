# TNPSC Group IV — Exam Assets (Blogger-Ready)

A dedicated repository for **TNPSC Group IV** study material that is loaded into
**Blogger** through a front-end script. Every file here is fetched over HTTPS
(raw GitHub / jsDelivr CDN) so that fonts, JSON and media render correctly
inside Blogger without CORS or font-rendering issues.

## 📢 Commercial Use Policy

This project is released under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license.  
**Commercial use is strictly prohibited without prior written permission.**

We actively monitor for unauthorized commercial exploitation. If you are a coaching academy, publishing house, ed-tech platform, or any other entity wishing to use, reproduce, or distribute this material for commercial purposes, you **must** obtain a separate commercial license.

**Contact for commercial licensing:**

> **Raj – The YOUTH for TRUTH and Health**  
> 📧 **tnyouthfoundation@gmail.com**

We welcome collaborations that respect the non-commercial spirit of this project.  
For all other permissions, please reach out to the same email address.

> ⚠️ Scope: **Group IV only.** Unrelated blog assets stay in the main repository.

---

## 📌 Purpose

- Store all Group IV **tests, guides, index pages, info pages, web pages and media**.
- Keep the Group IV content **isolated** from other blog assets.
- Provide a **stable, versioned, CDN-served** source that the Blogger front-end
  can `fetch()` reliably.
- Avoid Tamil font rendering problems by serving fonts + UTF-8 files from here.

---

## 📂 Folder Structure

```
group4/
├── index/                     # Index / manifest JSON files used by Blogger
│   ├── tests-index.json
│   ├── guides-index.json
│   └── info-index.json
│
├── tests/                     # Practice test data
│   ├── 2024/
│   │   ├── test-2024-01.json
│   │   └── test-2024-02.json
│   └── 2025/
│       └── test-2025-01.json
│
├── guides/                    # Study guides by subject
│   ├── polity/
│   ├── history/
│   ├── geography/
│   ├── science/
│   ├── tamil/
│   ├── aptitude/
│   └── current-affairs/
│
├── info/                      # Info pages (eligibility, syllabus, pattern…)
│   └── *.html / *.json
│
├── pages/                     # Full web pages loaded in Blogger
│   └── *.html
│
├── media/
│   ├── images/
│   ├── pdf/
│   ├── audio/
│   └── fonts/                 # Tamil / English web fonts
│
└── README.md
```

---

## 🗂️ File Types & Conventions

| Type        | Format        | Location              | Example                          |
|-------------|---------------|-----------------------|----------------------------------|
| Tests       | `.json`       | `tests/YYYY/`         | `tests/2024/test-2024-01.json`   |
| Guides      | `.html` `.md` | `guides/<subject>/`   | `guides/polity/polity-01.html`   |
| Index files | `.json`       | `index/`              | `index/tests-index.json`         |
| Info pages  | `.html` `.txt`| `info/`               | `info/eligibility.html`          |
| Web pages   | `.html`       | `pages/`              | `pages/group4-syllabus.html`     |
| Media       | `.pdf` `.png` `.mp3` `.woff2` | `media/` | `media/pdf/syllabus.pdf`     |

**Naming rules**

- All lowercase, **hyphens only** (no spaces, no underscores).
- Tests: `test-<year>-<serial>.json`
- Guides: `<subject>-<part>.html`
- Every new file **must** be added to its `index/*.json` manifest.

---

## 🔗 Access URLs

Replace `<user>` and `<repo>` with your GitHub username and this repo name.

**Raw GitHub**
```
https://raw.githubusercontent.com/<user>/<repo>/main/<path>
```

**jsDelivr (recommended — faster + cache-friendly)**
```
https://cdn.jsdelivr.net/gh/<user>/<repo>@main/<path>
```

Example:
```
https://cdn.jsdelivr.net/gh/<user>/group4@main/index/tests-index.json
https://cdn.jsdelivr.net/gh/<user>/group4@main/tests/2024/test-2024-01.json
```

> 💡 Pin to a tag (e.g. `@v1.0.0`) instead of `@main` for a frozen release,
> and use `@main` only during active editing.

---

## ⚙️ How Blogger Uses These Files

The Blogger front-end script only needs to fetch the **index manifest**, then
lazy-load individual tests / guides:

```js
const BASE = "https://cdn.jsdelivr.net/gh/<user>/group4@main/";

fetch(BASE + "index/tests-index.json")
  .then(r => r.json())
  .then(list => {
    // list = [{ id, title, year, path }, ...]
    list.forEach(item => loadTest(BASE + item.path));
  });

async function loadTest(url) {
  const res  = await fetch(url);
  const data = await res.json();      // questions, options, answers…
  renderTest(data);
}
```

- Add `charset="utf-8"` to any injected `<link>` / `<style>` / `<font>` tag.
- Load Tamil fonts from `media/fonts/` via `@font-face` with `font-display: swap;`
  to prevent FOIT / tofu boxes.

---

## ✅ Adding New Content — Checklist

1. Upload the file into the correct folder.
2. Update the matching `index/*.json` manifest.
3. Commit with a clear message: `add: test-2025-01 (Group IV)`
4. Verify the jsDelivr URL loads (CDN refreshes within ~12–24 h; use
   `https://purge.jsdelivr.net/gh/<user>/<repo>@main/<path>` to force it).
5. Confirm the Blogger page renders the new item.
6. (Optional) Tag a release `vX.Y.Z` for a stable snapshot.

---

## 🧾 License & Disclaimer

- Material is compiled **for personal / educational use** by TNPSC Group IV aspirants.
- **Not affiliated with** TNPSC or the Government of Tamil Nadu.
- Questions / notes are prepared or adapted by the author; please credit
  original sources where applicable.
- Do not redistribute paid or copyrighted coaching material.

---

**Maintainer:** *your-name / your-blog*
**Last updated:** *YYYY-MM-DD*
