# Contributing to ai-context-generator

Thank you for your interest in contributing. This project is a collection of meta-prompts, so contributions are straightforward — no code to compile, no tests to run. The quality bar is about clarity, accuracy, and usefulness.

---

## Ways to Contribute

### 🌍 New language translation
The most impactful contribution. If you can produce a high-quality, natural translation of the prompt in your language, it will immediately be useful to developers worldwide.

### 🛠️ Stack-specific improvements
If you work with a stack not well covered (Ruby/Rails, Java/Quarkus, .NET, Elixir/Phoenix, etc.), you can improve the detection logic and output templates for that stack.

### 🐛 Bug reports
If the prompt produces incorrect, misleading, or incomplete documentation for a specific project type, open an issue describing the case.

### ✏️ Clarity and wording improvements
If any instruction is ambiguous or could be expressed more precisely, a PR is welcome.

---

## Adding a New Language

1. Fork the repository and create a branch:
   ```bash
   git checkout -b feat/add-language-xx
   ```

2. Copy the English version as your base:
   ```bash
   cp AI-DOCS-GENERATOR.md AI-DOCS-GENERATOR-xx.md
   ```
   Replace `xx` with the [ISO 639-1 language code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) (e.g., `fr`, `de`, `ja`, `zh`).

3. Translate the file. Keep in mind:
   - Translate instructions and explanations, not code blocks or file paths
   - Adapt regional formats where relevant (date formats, currency, legal references like GDPR/LGPD/PIPL)
   - Use natural, professional language — avoid literal translations that sound awkward
   - Technical terms like `AGENT.md`, `JsonQ`, `PHPUnit`, `ADR` stay as-is

4. Add your language to the table in `README.md`:
   ```markdown
   | 🇫🇷 French / Français | [AI-DOCS-GENERATOR-fr.md](./AI-DOCS-GENERATOR-fr.md) |
   ```

5. Open a pull request with a clear title: `feat: add French translation`

---

## Improving Stack Coverage

If you want to improve detection or output quality for a specific stack:

1. Identify which phase needs improvement:
   - **Phase 1** — detection indicators (file names, dependencies, extensions)
   - **Phase 2** — architectural pattern mapping
   - **Phase 3** — convention detection from config files
   - **Output templates** — the generated `.ai/*.md` content

2. Make your changes in all language files to keep them in sync. If you only speak one language, note it in the PR and a maintainer or other contributor can help with the other versions.

3. Where possible, base your additions on real project structures. Invented examples are less useful than patterns observed in actual codebases.

---

## Pull Request Guidelines

- Keep PRs focused: one language or one improvement per PR
- Write a clear description of what changed and why
- If your PR touches all language files, mention it explicitly
- PRs that add content without a real use case may be declined — always explain the motivation

---

## Reporting Issues

When opening a bug report or improvement request, include:

- Which version of the prompt you used (language file + approximate date)
- Which AI assistant you used it with
- What type of project you ran it on (stack, rough size)
- What the prompt produced vs. what you expected

The more specific the report, the easier it is to address.

---

## What We Won't Accept

- Auto-generated translations without human review
- Stack additions based purely on speculation with no real-world validation
- Changes that make the prompt more verbose without improving its output
- Modifications that break backward compatibility with the generated file structure

---

## License

By contributing, you agree that your contributions will be licensed under the same [MIT License](./LICENSE) that covers this project.
