# AGENTS.md — Repository Instructions for AI Agents

- **Context:** Obsidian vault + academic/developer study notes and code projects (Duoc UC, software engineering, security, cloud).
- **Core Paradigm:** Hybrid structure (notes + code). Minimal boilerplate. Documentation-as-code.

---

## 1. Directory Structure & Conventions

- `2026/`: Active academic semester notes, lectures, labs.
- `Proyectos/`: Code implementations, sandboxes, scripts (e.g., Ticketti).
- `Recursos/`: Cheat sheets, manuals, reference materials, profiles.
- `MOCs/`: Maps of Content (Obsidian index notes).
- **Ignored Paths:** `.obsidian/`, `.makemd/`, `.space/`, `.trash/`, OS temp files (`.DS_Store`, `Thumbs.db`, `desktop.ini`).

---

## 2. Tech Stack & Environment

- **Languages:** Python, JavaScript/TypeScript, SQL, Markdown.
- **Runtime/Tools:** Node.js, Python 3.x, Git, PowerShell (Windows/Cross-platform).
- **Documentation:** Markdown (Obsidian flavored, standard `[[WikiLink]]` syntax).

---

## 3. Build, Test & Validation Commands

- **Check Git Status:** `git status`
- **Run Tests / Scripts:** `pytest` or `python -m unittest` in respective project subdirectories.

---

## 4. Coding & Writing Standards

- **Notes & Documentation:** Concise, technical, bullet-driven. Spanish for academic reflections/notes.
- **Code Projects:** Ponytail/YAGNI principle (minimum code solving the problem). Reuse existing utils before writing new ones. Strict input validation at trust boundaries.

---

## 5. Git & Commit Rules (Strict Spanish)

- **Commit Messages:** MUST be in Spanish following Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`).
- **Format:** `<tipo>(<alcance>): <descripción en español>` (e.g., `docs(cloud): añadir resumen semana 1 cloud native`).
- **Staging:** Stage only intended files. Never commit secrets, API keys, or Obsidian workspace states.

---

## 6. Gotchas & Operational Pitfalls

- **Pathing:** Windows OS environment (`win32`, PowerShell). Always quote paths containing spaces.
- **Vault Integrity:** Do not break Obsidian relative links or frontmatter metadata (`tags:`, `aliases:`).
- **Scope Creep:** Do not auto-generate speculative notes or unrequested refactoring in adjacent directories.

---

## 7. AI Workflow & Safety Rules

- **Surgical Edits:** Touch only requested files. Preserve adjacent formatting.
- **Verification:** Non-trivial logic requires an assertion or test check.
- **Token Efficiency:** Keep context lean. Use grep/glob before reading large files.
