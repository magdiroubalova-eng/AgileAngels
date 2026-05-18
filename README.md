# Agile Angels — QA Team Showcase 🪽

[![HTML Validator](https://github.com/magdiroubalova-eng/AgileAngels/actions/workflows/html-validator.yml/badge.svg)](https://github.com/magdiroubalova-eng/AgileAngels/actions/workflows/html-validator.yml)
[![Deploy to GitHub Pages](https://github.com/magdiroubalova-eng/AgileAngels/actions/workflows/static.yml/badge.svg)](https://github.com/magdiroubalova-eng/AgileAngels/actions/workflows/static.yml)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-live-success?logo=github)](https://magdiroubalova-eng.github.io/AgileAngels/)
[![Accessibility](https://img.shields.io/badge/WCAG%202.1-SC%202.4.6-blueviolet)](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)

> A QA-team-themed website built by women in tech — with a full automated QA infrastructure to back it up. Because we test our own code, too.

🌐 **Live demo:** [magdiroubalova-eng.github.io/AgileAngels](https://magdiroubalova-eng.github.io/AgileAngels/)

---

## 🎯 About

**Agile Angels** is a five-woman QA team project from the [Czechitas Digital Academy — Testing Track](https://www.czechitas.cz/) (2026 cohort). The website celebrates our team identity, our individual roles, and the QA mindset that connects us — featuring a Sprint Board, a "QA Dictionary" of inside jokes, a Bug Hunt leaderboard, and individual member profiles.

But the website is just one half of the story. The **other half is the automated QA infrastructure** that ensures this static site stays high-quality on every commit. This README documents both.

---

## 🛠️ Tech Stack

| Layer | Tech |
|---|---|
| Frontend | Vanilla HTML5 + CSS3 |
| Icons | [Lucide](https://lucide.dev/) (via CDN) |
| Fonts | Google Fonts (Bangers, Inter, Montserrat, Sora, Space Mono) |
| CI/CD | GitHub Actions |
| Hosting | GitHub Pages (auto-deployed from `main`) |
| Dev tools | VS Code, GitHub Copilot, Claude Code |

No frameworks, no build step. Just clean web fundamentals — the way QA likes it: deterministic and testable.

---

## ✅ QA Infrastructure

### Implemented

#### 🔍 HTML Validator
**File:** `.github/workflows/html-validator.yml`

Automated HTML validation using the [Nu Html Checker](https://validator.w3.org/nu/) — the same engine behind the official W3C validator — via [`Cyb3r-Jak3/html5validator-action`](https://github.com/Cyb3r-Jak3/html5validator-action).

**Triggers:**
- `push` to `main`
- `pull_request` to `main`
- `workflow_dispatch` (manual trigger from Actions tab)
- `schedule` — weekdays at 06:00 UTC (`cron: '0 6 * * 1-5'`)

**What it catches:** unclosed tags, invalid element nesting, missing required attributes, duplicate `<head>` tags, and accessibility issues such as sections without headings.

### Planned

- 🔗 **Link Checker** — using `lycheeverse/lychee-action` to catch dead internal and external links
- 💡 **Lighthouse Audit** — measuring performance, accessibility, SEO, and best practices
- 🎭 **Playwright E2E** — interactive flow testing (click-through navigation, button behavior, user journeys)
- 🐰 **CodeRabbit** — AI-powered automated code review on every pull request

---

## ♿ Accessibility Highlights

The site implements **WCAG 2.1 Success Criterion 2.4.6 — [Headings and Labels](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)**.

Every `<section>` element contains a heading (`h1`–`h6`). For sections where a visible heading would conflict with the visual design (hero banner, footer navigation), we use the industry-standard **`.sr-only` utility class** defined in `src/style.css`:

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

This pattern (used in Bootstrap, Tailwind, and most major design systems) keeps headings in the DOM for assistive technologies — screen readers, voice navigation — while hiding them visually.

**Why this matters:** previously, a screen-reader user landing on the hero would only hear `"Image: Agile Angels"`. Now they hear `"Agile Angels — QA testing team"` and know exactly where they are.

**Files with accessibility improvements:**
- `src/index.html` — 1 `sr-only` heading (hero section)
- `src/bug-hunt.html` — 3 `sr-only` headings (image, footer, bottom bar)
- `src/member-detail.html` — 1 `sr-only` heading (footer)

---

## 📁 Project Structure

```
AgileAngels/
├── .github/
│   └── workflows/
│       ├── html-validator.yml    # HTML validation CI
│       └── static.yml            # GitHub Pages deployment
├── guide/                        # Course materials (lecturer-provided)
├── src/                          # Website source
│   ├── index.html                # Main page — Meet the Team
│   ├── member-detail.html        # Individual member profile
│   ├── bug-hunt.html             # Bug Hunt leaderboard
│   ├── style.css                 # All styles (incl. .sr-only utility)
│   ├── done.js                   # Page interactions
│   └── images/                   # Image assets
├── .gitignore
└── README.md                     # This file
```

---

## 🌿 Development Workflow

This project follows a **branch-and-PR workflow** with code review:

1. **Feature branch** — named with conventional prefix: `feature/<topic>`, `fix/<issue>`, `refactor/<scope>`, `ci/<scope>`
2. **Pull request** to `main` — opened with a structured description (*What / Why / Test*)
3. **Code review** — performed by team members and optionally AI reviewers (GitHub Copilot, Claude Code, CodeRabbit)
4. **Automated checks** — HTML Validator runs on every PR; PR cannot be merged if checks fail ❌
5. **Merge** — using a merge commit to preserve commit history

**Commit messages** follow the [Conventional Commits](https://www.conventionalcommits.org/) format:

| Prefix | Use case |
|---|---|
| `feat:` | New feature or capability |
| `fix:` | Bug fix |
| `refactor:` | Code restructuring without behavior change |
| `ci:` | CI/CD configuration changes |
| `docs:` | Documentation updates |

---

## 💻 Local Setup

```bash
# Clone the repo
git clone https://github.com/magdiroubalova-eng/AgileAngels.git
cd AgileAngels

# Serve the static site locally
# Option 1: VS Code Live Server extension (right-click index.html → "Open with Live Server")
# Option 2: Python's built-in HTTP server
python -m http.server 8080 --directory src

# Then open http://localhost:8080 in your browser
```

No build step required.

---

## 👥 The Team

| Codename | Role | Tagline |
|---|---|---|
| **Kamila** | Explorer | *Finding bugs before they find you* |
| **Majda** | Visionary | *Bright ideas, brighter solutions* |
| **Jana** | Organizer | *Checklists are her love language* |
| **Lucia** | Automator | *Spinning gears, shipping quality* |
| **Oli** | Storyteller | *User stories are her superpower* |

---

## 📚 Behind the Scenes — What I Learned

For me personally (Magda), building the QA infrastructure side of this project was an exercise in:

- **Setting up CI/CD from scratch** — writing YAML workflow files, debugging exit codes, configuring schedule triggers and event filters
- **HTML accessibility** — implementing WCAG patterns, learning the difference between `display: none` and the `sr-only` technique
- **Git workflows** — feature branches, structured PR descriptions, conventional commit messages, atomic commits
- **Architecture decisions** — knowing when to fix vs. when to exclude vs. when to refactor (e.g., removing a vendor reference file once upstream sync was no longer relevant, and re-enabling full validation as a result)
- **Working with AI tools as a QA engineer** — using Claude and GitHub Copilot to accelerate code generation, while applying the QA mindset of *trust but verify*

---

## 📄 License

Czechitas Digital Academy — Testing Track 2026.  
Educational project. *All bugs will be found.* 🐛
