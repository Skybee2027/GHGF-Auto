# GHGF Ebook Robot

Repo: https://github.com/Skybee2027/GHGF-Auto
Timezone for all times: America/New_York (EST/EDT).

Folders:
- `blogs/` – topic source. If empty, use topics from https://greathealthgreatfitness.com (no medical topics).
- `ebooks/` – output. Each book lives in `ebooks/<YYYY-MM-DD>/<slug>/` with:
  - `book.md` – full manuscript
  - `cover.html` – designed cover (colored gradient, title, subtitle)
  - `book.pdf` – final PDF (cover page first, then chapters)
  - `meta.json` – `{ "title", "subtitle", "slug", "source_topic", "price_usd": 9.99, "status", "verification_log": [] }`
- `ebooks/REPORT-<YYYY-MM-DD>.md` – daily report of created, verified, saved, failed.

## Content rules (all stages)
- Engaging, well-structured, and colorful headings and cover. Target 6,000–10,000 words, 8–12 chapters.
- NO medical advice: no diagnoses, symptoms, treatments, medications, supplements, dosing, or "cure" claims. General wellness, fitness habits, and lifestyle education only, with a line suggesting readers consult a qualified professional.
- Do not invent statistics, studies, or quotes. Use general, verifiable knowledge; avoid specific numbers unless they are common knowledge.
- Do not use placeholder text (TODO, lorem ipsum, [insert], XXX).
- Never write secrets or API keys into the repo.

## Stage 1 — Create (06:00 ET)
1. Pull the repo. Read topics from `blogs/`. Skip any topic already used (check `source_topic` in existing `meta.json` files).
2. Create exactly 2 ebooks for today. Write `book.md`.
3. Build `cover.html` (gradient background, large title, subtitle, "GHGF" brand line) and render it as the first page of `book.pdf`. Install tooling if missing (`pip install --break-system-packages weasyprint` or a headless browser).
4. Set `status: "draft"` in `meta.json`. Commit and push.

## Stage 2 — Verify (11:00 to 13:00 ET)
Verify every draft from today and reverify after each fix:
- Manuscript is complete, chapters match the outline, no placeholder text, no broken markdown.
- No medical advice language (run a keyword check for: diagnose, treat, cure, medication, dosage, symptom, supplement, prescription).
- PDF exists, opens, cover is page 1, page count is sane, text is not cut off.
- Title, subtitle, price (9.99) are set in `meta.json`.
- Log each check in `verification_log`. Fix errors, re-render, and recheck.
- Set `status: "verified"` on pass, or `"failed"` with the reason on failure. Commit and push.

## Stage 3 — Save (15:00 ET)
1. Pull the repo. Only `status: "verified"` books are final.
2. Set `status: "final"`, write `ebooks/REPORT-<date>.md` listing created, verified, final, and failed books with reasons.
3. Commit and push with a clear message. Do not force-push.
4. Failed drafts stay in their folder with their reason in the report.
