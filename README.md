# GitGud Translation Guide

You don’t need to know anything about the game’s code to help. If you can read English and translate into another language, you’re ready. This page shows you how to add a brand‑new language or improve an existing one using only the GitHub website.

---
## 1. What You Actually Translate
All texts you see in the menus (welcome messages, buttons, prompts, warnings, etc.) live in simple text files inside the folder: `Data/i18n/`

Each file is a list of "key": "text" pairs. Example (English):
```json
{
	"ui.title.welcome": "Welcome to Git Gud - Master Git through 100 progressive challenges!",
	"ui.general.start": "Start"
}
```

You only change the right‑hand side (the text). Never change the left side (the key). Keys are how the game knows which line to show.

---
## 2. File Names
| Type | Example | When to use |
|------|---------|------------|
| Base English (always there) | `en.json` | Source text. Use this as your reference. |
| A new language | `fr.json`, `es.json`, `de.json` | 2‑letter lowercase language code (ISO 639‑1). |
| Regional variant (optional) | `pt-BR.json`, `en-GB.json` | Only if a region spelling/word differs. Include ONLY changed lines. |

If a line is missing in your language file, the game temporarily falls back to English—so partial translations are fine.

---
## 3. Basic Workflow (All on GitHub Web)
1. Open the GitGud repository on GitHub.
2. Click the Fork button (top-right) to create your own copy.
3. In your fork, browse to `Data/i18n/`.
4. Adding a new language? Click “Add file” → “Create new file” → name it like `it.json` (for Italian). Improving one? Open e.g. `fr.json` and click the pencil ✏️.
5. Paste or edit content (see next section for how to start).
6. Scroll down, write a short description (example: `Add Italian translation (menu + intro messages)`), then press “Commit changes”.
7. Click “Contribute” → “Open pull request”. Describe what you translated and (optionally) what’s still missing.

That’s it. A maintainer will review and merge or request tweaks.

---
## 4. Starting a New Translation Quickly
Option A (minimal): Create your `<lang>.json` and only include the lines you translate now. Example Spanish start:
```json
{
	"ui.title.welcome": "Bienvenido a Git Gud - Domina Git con 100 desafíos progresivos!",
	"ui.general.start": "Comenzar"
}
```

Option B (full template): Copy the whole `en.json`, paste it, then translate line by line. This is more work initially but makes it easy to see what’s left.

Both are acceptable.

---
## 5. How to Edit Safely
Do:
* Only translate the text after the colon.
* Keep punctuation if it makes sense in your language.

Don’t:
* Don’t rename or delete keys on the left.
* Don’t add random new keys (ask first if you think one is needed).
* Don’t add translator credits inside the text—Git remembers you.

---
## 6. Style & Tone
* Keep sentences friendly, clear, and concise.
* Avoid overly technical slang if a simpler word exists.
* Prefer neutral gender unless your language requires a form—pick the most widely understood variant.
* Be consistent: if you choose “Quitter” vs “Sortir” for a button, use it everywhere that context applies.

---
## 7. Handling Long Text
If a phrase becomes too long and might wrap awkwardly, consider:
* Shortening synonyms (e.g., “Configuration” → “Paramètres” already fine in FR, etc.)
* Removing duplicate meaning (e.g., “Please select” → “Select”).

If you are unsure, leave a note in the Pull Request.

---
## 8. Checking Your Work (Simple)
You can skip technical checks if unsure; maintainers can help. But if you’d like:

Quick self-check:
1. Make sure the file starts with `{` and ends with `}`.
2. Every line except the last ends with a comma.
3. Quotes always come in pairs `"text"`.
4. Search for `"ui.` occurrences—did you accidentally alter any key names on the left side?

Optional (if you have Windows PowerShell and feel comfortable):
```powershell
# List missing keys vs English (replace fr with your language code)
$en = (Get-Content Data/i18n/en.json | ConvertFrom-Json).psobject.Properties.Name
$tr = (Get-Content Data/i18n/fr.json | ConvertFrom-Json).psobject.Properties.Name
$en | Where-Object { $_ -notin $tr }
```
This simply shows which English keys you haven’t translated yet. No need to reach 100% before opening a PR.

---
## 9. Regional Differences (Optional)
If your language has regional differences (example: Portuguese in Portugal vs Brazil):
1. Translate a shared base file first (e.g. `pt.json`).
2. Create a second file (e.g. `pt-BR.json`) containing only lines that differ:
```json
{
	"ui.general.start": "Iniciar"
}
```
Everything else will reuse `pt.json` (and then English if still missing).

If you’re unsure whether a regional file is justified, just ask in an issue.

---
## 10. Common Mistakes & Fixes
| Problem | What Happens | Fix |
|---------|--------------|-----|
| Changed a key name | Game can’t find the text | Revert key name; only translate value |
| Removed a comma mid‑file | File stops working | Add comma after every line except the last |
| Added translator credit in text | Shows to players | Remove it (Git logs credit you) |
| Wrong filename (e.g. `FR.json`) | File ignored | Use lowercase: `fr.json` |

---
## 11. Pull Request Template (You Can Copy This)
Title: `i18n(es): initial Spanish translation (menus + core)`

Description:
```
Language: Spanish (es)
Coverage: ~40% (menus & intro basics). Will continue in a later PR.
Questions: None.
Notes: Kept 'Git' and technical terms in English when standard.
```

---
## 12. If English Changes
Sometimes new English lines are added or wording changes. It’s okay if your language file doesn’t have those yet—English will show until someone translates them. You can open very small PRs that translate just a handful of new lines.

---
## 13. License & Credit
By submitting translations you agree they are included under the project’s license. Your GitHub username becomes part of the contributor history, no need to sign the text itself.

---
## 14. Need Help or Unsure About a Phrase?
Open a GitHub Issue or Discussion with a title starting `[i18n]` and explain the question (include the key name). Someone will clarify.

---
## 15. Quick TL;DR
1. Fork project
2. Add or edit `<lang>.json`
3. Only translate the right side
4. Commit & open Pull Request (can be partial)

Thank you for helping more people learn Git with GitGud!
