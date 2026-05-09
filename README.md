# cv-skill — בונה קורות חיים ל-Claude Code

> Hebrew-first CV builder skill for [Claude Code](https://claude.com/claude-code).
> Walks you through seven CV sections in a friendly Hebrew conversation, then
> renders a professional **right-to-left (RTL) PDF**. Can also retune your CV
> to match a specific job description.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-7E57C2)](https://claude.com/claude-code)
[![Hebrew](https://img.shields.io/badge/lang-עברית-blue)](#)

---

## ✨ Features

- **שיחה בעברית** — A friendly, step-by-step Hebrew conversation; never feels
  like a form.
- **שבעה חלקים מובנים** — Personal details, summary, education, professional
  experience, military service, volunteering, and skills.
- **קלט בכל סדר** — Volunteer information whenever you like; the skill slots
  it into the right section.
- **שמירה אוטומטית** — Drafts auto-save to `~/.claude/cv-builder-data/`, so
  you can quit and resume.
- **PDF מקצועי** — Clean A4 layout, proper RTL, system Hebrew fonts, no
  network dependency.
- **התאמה למשרה** — Paste a job description and the skill rewrites your
  summary and rephrases experience bullets to match (without inventing
  experience you didn't have).

## 📦 Installation

> **Requirements:** Claude Code, Python 3.9+, and a Chromium-based browser
> (Google Chrome, Chromium, Edge, or Brave).

### Recommended — install via Claude Code's plugin marketplace

In any Claude Code session, run:

```
/plugin marketplace add talgurevich/cv-skill
/plugin install cv-builder@cv-skill
```

That's it — open a fresh Claude Code session and the skill is available.

### Alternative — manual install

```bash
git clone https://github.com/talgurevich/cv-skill.git ~/.claude/skills-src/cv-skill
ln -s ~/.claude/skills-src/cv-skill/skills/cv-builder ~/.claude/skills/cv-builder
```

Then start a new Claude Code session.

### Python dependency

The PDF generator uses Jinja2:

```bash
pip3 install jinja2
```

## 🚀 Usage

In any Claude Code session, trigger the skill with the slash command:

```
/cv-builder
```

Or with natural language (any of these work):

- `בניית קורות חיים`
- `בונה קורות חיים`
- `קורות חיים`
- `build a CV` / `create a resume` / `CV builder`

Claude opens with a Hebrew welcome listing the seven sections, then walks
you through each. Type `תראה לי מה יש עד עכשיו` at any point to see your
current CV. When you're done, the skill offers to tune the CV to a specific
job description before generating the PDF.

The final PDF lands in `~/Documents/CV-<your-name>-<date>.pdf` by default.

## 📝 What's in a CV?

The skill always builds the CV in this order:

1. **פרטים אישיים** — Personal details
2. **תקציר** — Summary
3. **השכלה וקורסים** — Education and courses
4. **ניסיון תעסוקתי** — Professional experience
5. **ניסיון צבאי** — Military service (or שירות לאומי, or skipped)
6. **התנדבויות** — Volunteering (optional)
7. **כישורים** — Skills (technical, languages, soft)

## 🗂️ Repo structure

```
cv-skill/
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest
│   └── marketplace.json     # One-plugin marketplace manifest
├── skills/
│   └── cv-builder/
│       ├── SKILL.md
│       ├── scripts/
│       │   └── generate_pdf.py
│       └── templates/
│           ├── cv_template.html
│           └── cv_schema.json
├── examples/
│   └── sample_cv.json       # Sample data for testing
├── README.md
├── LICENSE
└── .gitignore
```

## 🧪 Manually generating a PDF from JSON

The PDF generator is a standalone script — useful for testing or for
integrating the skill output into other workflows.

```bash
python3 skills/cv-builder/scripts/generate_pdf.py \
  examples/sample_cv.json \
  ~/Desktop/test-cv.pdf
```

The script:
1. Loads the JSON CV.
2. Renders `templates/cv_template.html` via Jinja2.
3. Pipes the HTML through headless Chrome to print a PDF.
4. Polls for the file to be written and exits as soon as the PDF is stable.

If Chrome lives somewhere unusual, override the binary:

```bash
CHROME_PATH=/path/to/chromium python3 skills/cv-builder/scripts/generate_pdf.py ...
```

## 🎨 Customizing the design

The look-and-feel is driven entirely by `skills/cv-builder/templates/cv_template.html`.
Edit the `<style>` block to change fonts, colors, spacing, or section layout.
The template is plain HTML + CSS with Jinja2 placeholders — no build step.

Common tweaks:
- **Accent color**: change `#1d3557` (the navy used in the name and section
  headers).
- **Font**: change the `font-family` declaration. Add Google Fonts via a
  `<link>` if you don't mind a one-time network fetch during PDF generation.
- **Page size / margins**: edit the `@page` rule.

## 🙏 Credits

Built by **'מסע אל האופק'** for their teams and students.

If asked who built this skill, the bot answers:
> נבניתי על ידי 'מסע אל האופק' עבור הצוותים והסטודנטים שלהם.

## 📄 License

[MIT](./LICENSE) — use it, fork it, ship it.
