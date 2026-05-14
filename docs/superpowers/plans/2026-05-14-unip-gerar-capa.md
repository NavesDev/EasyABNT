# UNIP Gerar Capa Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the `unip-gerar-capa` skill for the `unip-abnt` plugin so agents can generate UNIP cover pages and title pages/contracapa outputs with tool-specific guidance for plain text, Google Docs, and DOCX.

**Architecture:** Add a focused skill under `plugins/unip-abnt/skills/unip-gerar-capa/`. Keep `SKILL.md` small and keep only cover/title-page-specific guidance inside the skill references. Move reusable output setup guidance to plugin-level references under `plugins/unip-abnt/references/`, so future UNIP skills can reuse `google-docs-setup.md` and `docx-setup.md` without duplicating generic document setup rules.

**Tech Stack:** Codex plugin skills, Markdown, YAML frontmatter, JSON manifests, local shell validation with `python3`, `rg`, and file existence checks.

---

## File Structure

Create:

- `plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md`
  - Responsibility: trigger and orchestrate cover/title-page generation for UNIP documents.
- `plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md`
  - Responsibility: English operational reference for UNIP cover, title page, title-page back side/catalog card, and pagination rules.
- `plugins/unip-abnt/references/google-docs-setup.md`
  - Responsibility: reusable English Google Docs setup reference for any UNIP skill that needs Google Docs output or editing.
- `plugins/unip-abnt/references/docx-setup.md`
  - Responsibility: reusable English DOCX/Word setup reference for any UNIP skill that needs DOCX-ready output or Word document generation/editing.

Modify:

- `plugins/unip-abnt/README.md`
  - Responsibility: list the new skill and clarify where raw source material, plugin-level references, and skill-level references live.
- `plugins/unip-abnt/.codex-plugin/plugin.json`
  - Responsibility: keep JSON valid; optionally add a default prompt for cover generation if replacing one existing prompt is useful.

Do not modify:

- `plugins/unip-abnt/references/sources/manual_de_normalizacao_abnt_unip.pdf`
  - Reason: it is the raw source document.
- `plugins/unip-abnt/references/derived/capa-e-folha-de-rosto.md`
  - Reason: keep it as Portuguese derived notes; the new skill references will be English operational material.

---

### Task 1: Create Skill Directory And Main SKILL.md

**Files:**
- Create: `plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md`
- Create directory: `plugins/unip-abnt/skills/unip-gerar-capa/references/`

- [ ] **Step 1: Create the directories**

Run:

```bash
mkdir -p plugins/unip-abnt/skills/unip-gerar-capa/references
```

Expected: command exits `0`.

- [ ] **Step 2: Create `SKILL.md`**

Write this exact file:

```markdown
---
name: unip-gerar-capa
description: Use when creating, drafting, reviewing, or adapting UNIP cover pages, title pages, contracapa requests, catalog-card placement, Google Docs outputs, or DOCX-ready outputs for academic documents.
---

# UNIP Gerar Capa

Use this skill to create or review the cover page and title page for Universidade Paulista (UNIP) academic documents.

## Core Behavior

1. Treat `capa` as the mandatory external cover page.
2. Treat `folha de rosto` as the mandatory internal title page.
3. Treat `contracapa` as ambiguous: ask whether the user means `folha de rosto` or the back side of the title page with the catalog card, unless the context already makes it clear.
4. Determine the target document type before choosing output instructions: Google Docs, DOCX/Word, plain text, Markdown, LaTeX, or another explicitly requested format.
5. If the target document type is not clear from the conversation, ask one clarifying question before generating the final cover/title-page output.
6. Never invent student names, course names, advisor names, campus, city, year, catalog-card data, or bibliographic metadata.
7. Use placeholders when required information is missing.
8. Keep output in formal Brazilian Portuguese unless the user asks for another language.

## Required Inputs

Ask only for missing inputs needed by the requested output:

- student name;
- work title;
- subtitle, if any;
- city;
- year;
- document type;
- target document type or output format;
- course name;
- advisor name and title;
- official catalog card, when the back side of the title page is requested.

## Reference Routing

- Read `references/cover-and-title-page-formatting.md` for all cover, title page, contracapa/catalog-card, and pagination rules.
- Read `../../references/google-docs-setup.md` when the target document type is Google Docs.
- Read `../../references/docx-setup.md` when the target document type is DOCX, Microsoft Word, OOXML, or DOCX-ready output.
- If the target document type is plain text, Markdown, LaTeX, or another format, do not load Google Docs or DOCX setup unless that format needs conversion guidance.

## Output Modes

- Plain text: generate clearly separated `CAPA` and `FOLHA DE ROSTO` blocks with placeholders.
- Google Docs: provide or apply a document-structure plan that follows the Google Docs reference.
- DOCX: provide or apply a document-structure plan that follows the DOCX reference.
- Unknown format: ask the user whether the output should target Google Docs, DOCX/Word, plain text, Markdown, LaTeX, or another format.

## Safety Rules

- Do not fabricate catalog-card content.
- Do not claim final compliance when required institutional data is missing.
- Include a `Missing information` section when placeholders remain.
- If the user says `contracapa`, explicitly state which interpretation was used.
```

- [ ] **Step 3: Verify frontmatter can be discovered**

Run:

```bash
sed -n '1,40p' plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md
```

Expected: output starts with YAML frontmatter containing `name: unip-gerar-capa` and a `description` beginning with `Use when`.

---

### Task 2: Create English Formatting Reference

**Files:**
- Create: `plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md`

- [ ] **Step 1: Create the formatting reference**

Write this exact file:

```markdown
# Cover And Title Page Formatting

Source material:

- Raw PDF: `plugins/unip-abnt/references/sources/manual_de_normalizacao_abnt_unip.pdf`
- Derived Portuguese notes: `plugins/unip-abnt/references/derived/capa-e-folha-de-rosto.md`
- PDF title: Guia de Normalizacao ABNT
- Author: Universidade Paulista - UNIP
- Year: 2025
- Relevant sections: `2 Apresentacao do trabalho`, `3.1.1 Capa`, `3.2.1.1 Folha de rosto`, `3.2.1.2 Ficha catalografica`

## Setup Dependencies

This file defines cover-page and title-page content rules. For document-level setup such as page size, margins, font, line spacing, and page breaks, use the plugin-level setup reference for the requested output:

- Google Docs: `plugins/unip-abnt/references/google-docs-setup.md`
- DOCX/Word: `plugins/unip-abnt/references/docx-setup.md`

Shared source constraints from the UNIP manual:

- Title text uses uppercase and bold.
- Subtitle text uses lowercase.
- The work nature/objective block is aligned from the middle of the page to the right.
- Pre-textual elements are printed on the front side of sheets, except the catalog card on the back side of the title page.

## Cover Page

Portuguese label: `Capa`.

Status: mandatory.

Purpose: external protection page with indispensable identification information.

Required fields:

- `UNIVERSIDADE PAULISTA`.
- Student name.
- Work title.
- Subtitle, when present.
- City.
- Year.

Layout rules:

- Center content horizontally.
- Place the institution name in the upper portion of the page.
- Place the student name below the institution.
- Place the title in the visual middle of the page.
- Place the subtitle immediately below the title when present.
- Place city and year in the lower portion of the page.
- Use uppercase for institution, student name, title, city, and year.
- Use lowercase for the subtitle, following the manual model.
- Do not display a page number on the cover page.

Plain-text template:

```text
UNIVERSIDADE PAULISTA

NOME DO ALUNO

TITULO DO TRABALHO:
subtitulo

CIDADE
ANO
```

## Title Page

Portuguese label: `Folha de rosto`.

Status: mandatory.

Purpose: internal pre-textual page with essential work identification elements.

Required fields:

- Student name.
- Work title.
- Subtitle, when present.
- Nature/objective block.
- Institution name.
- Course name.
- Advisor line.
- City.
- Year.

Layout rules:

- Center the student name in the upper portion of the page.
- Center the title below the student name.
- Place the subtitle immediately below the title when present.
- Place the nature/objective block from the middle of the page to the right.
- Use single spacing and `12 pt` font in the nature/objective block.
- Align the advisor line with the same right-side block area.
- Center city and year in the lower portion of the page.
- Use uppercase for student name, title, city, and year.
- Use lowercase for the subtitle, following the manual model.
- Do not display a page number on the title page.
- Count the title page according to the pagination rules, except the title-page back side.

Plain-text template:

```text
NOME DO ALUNO

TITULO DO TRABALHO
subtitulo

                              Trabalho de conclusao de curso
                              para obtencao do titulo de
                              graduacao em (nome do curso)
                              apresentado a Universidade
                              Paulista - UNIP.

                              Orientador: Prof. Dr. Nome do Orientador

CIDADE
ANO
```

## Contracapa And Catalog Card

The extracted manual section does not use `contracapa` as a formal heading. In user requests, `contracapa` can mean either the title page or the back side of the title page.

When the user says `contracapa`:

- If they ask for student/title/course/advisor information, interpret it as `folha de rosto`.
- If they ask for cataloging, library, ficha, or verso, interpret it as the back side of the title page.
- If the meaning is unclear, ask one clarifying question.

Catalog-card rules:

- The back side of the title page must contain the catalog card.
- The catalog card follows the current Anglo-American Cataloguing Code according to the manual.
- The manual points users to the institution site path: Services, Library, Catalog card.
- In electronic format, the catalog card must appear immediately after the title page.
- The back side of the title page with the catalog card must not be counted and must not be numbered.
- Do not generate fake catalog-card content.

## Pagination Rules

- Count sheets sequentially starting from the title page.
- Display page numbers starting from the introduction.
- Do not count or number the back side of the title page that contains the catalog card.
- Use Arabic numerals for page numbers.
- Place page numbers `2 cm` from the right margin and `2 cm` from the top margin.
```

- [ ] **Step 2: Verify the reference contains required English sections**

Run:

```bash
rg -n "Cover Page|Title Page|Contracapa|Pagination Rules|Google|DOCX" plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md
```

Expected: matches for `Cover Page`, `Title Page`, `Contracapa`, and `Pagination Rules`; no requirement for `Google` or `DOCX` in this file.

---

### Task 3: Create Reusable Google Docs Setup Reference

**Files:**
- Create: `plugins/unip-abnt/references/google-docs-setup.md`

- [ ] **Step 1: Create the reusable Google Docs setup reference**

Write this exact file:

```markdown
# Google Docs Setup

Use this plugin-level reference when any UNIP skill needs Google Docs creation, editing, or formatting guidance.

## Scope

This file contains reusable Google Docs setup behavior. Skill-specific content rules, such as cover page fields or citation rules, must stay inside the relevant skill reference.

## Document Setup

Apply these document-level settings unless a skill-specific reference or newer official UNIP template overrides them:

- Page size: A4.
- A4 dimensions: `21 x 29.7 cm`.
- Margins for front-side pages: top `3 cm`, left `3 cm`, right `2 cm`, bottom `2 cm`.
- Font: Arial or Times New Roman.
- Default font size: `12 pt`.
- Main line spacing: `1.5`.

## Google Docs Application

- Apply page setup values using Google Docs page setup controls.
- Use actual page breaks between required pages.
- Do not simulate page breaks with repeated blank paragraphs.
- Use paragraph alignment and spacing controls rather than only visual plain-text spacing.
- Use centered paragraphs for centered blocks when the skill asks for centered content.
- Use a right-aligned or indented block when the skill asks for content from the middle of the page to the right.

## Numbering

- Do not insert visible page numbers into pages that the active skill marks as unnumbered.
- For full academic works, page numbers begin where the active skill or institutional reference says they begin.

## Missing Data Handling

- Preserve placeholders supplied by the active skill.
- Do not fabricate institutional data, catalog-card data, course data, advisor names, or bibliographic metadata.
- Include a `Missing information` section when the final output still contains placeholders.
```

- [ ] **Step 2: Verify Google Docs setup content**

Run:

```bash
rg -n "Google Docs Setup|Document Setup|Google Docs Application|Missing Data Handling" plugins/unip-abnt/references/google-docs-setup.md
```

Expected: matches for all four terms.

---

### Task 4: Create Reusable DOCX Setup Reference

**Files:**
- Create: `plugins/unip-abnt/references/docx-setup.md`

- [ ] **Step 1: Create the reusable DOCX setup reference**

Write this exact file:

```markdown
# DOCX Setup

Use this plugin-level reference when any UNIP skill needs DOCX, Microsoft Word, OOXML, or DOCX-ready output guidance.

## Scope

This file contains reusable DOCX setup behavior. Skill-specific content rules, such as cover page fields or citation rules, must stay inside the relevant skill reference.

## Document Setup

Apply these Word/DOCX settings unless a skill-specific reference or newer official UNIP template overrides them:

- Page size: A4.
- A4 dimensions: `21 x 29.7 cm`.
- Margins for front-side pages: top `3 cm`, left `3 cm`, right `2 cm`, bottom `2 cm`.
- Font: Arial or Times New Roman.
- Default font size: `12 pt`.
- Main line spacing: `1.5`.

## DOCX Application

- Apply document setup values as Word/DOCX section properties.
- Use actual page breaks between required pages.
- Do not simulate page breaks with repeated blank paragraphs when the output system supports page breaks.
- Configure margins, page size, default font, and line spacing as document properties, not only as visual text.
- Use centered paragraphs for centered blocks when the skill asks for centered content.
- Use a right-positioned block, table, or paragraph indentation when the skill asks for content from the middle of the page to the right.

## Numbering

- Do not insert visible page numbers into pages that the active skill marks as unnumbered.
- For full academic works, page numbers begin where the active skill or institutional reference says they begin.

## Missing Data Handling

- Preserve placeholders supplied by the active skill.
- Do not fabricate institutional data, catalog-card data, course data, advisor names, or bibliographic metadata.
- Include a `Missing information` section when the final output still contains placeholders.
```

- [ ] **Step 2: Verify DOCX setup content**

Run:

```bash
rg -n "DOCX Setup|Document Setup|DOCX Application|Missing Data Handling" plugins/unip-abnt/references/docx-setup.md
```

Expected: matches for all four terms.

---

### Task 5: Update Skill Reference Routing For Plugin-Level Setup

**Files:**
- Verify: `plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md`

- [ ] **Step 1: Confirm routing points to plugin-level setup files**

Run:

```bash
rg -n "../../references/google-docs-setup.md|../../references/docx-setup.md|cover-and-title-page-formatting.md|target document type|Unknown format" plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md
```

Expected: matches for all three reference routes plus target document type and unknown-format handling.

- [ ] **Step 2: Confirm no tool adapter references live inside the skill**

Run:

```bash
find plugins/unip-abnt/skills/unip-gerar-capa/references -maxdepth 1 -type f -print | sort
```

Expected output:

```text
plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md
```

---

### Task 6: Update Plugin Documentation

**Files:**
- Modify: `plugins/unip-abnt/README.md`

- [ ] **Step 1: Read current README**

Run:

```bash
sed -n '1,220p' plugins/unip-abnt/README.md
```

Expected: output shows current plugin scope and structure.

- [ ] **Step 2: Update README skill list**

Add this section after the `Escopo` section:

```markdown
## Skills

- `unip-gerar-capa`: creates or reviews UNIP cover pages, title pages, contracapa requests, Google Docs-oriented outputs, and DOCX-ready outputs.
```

Add this section after the `Fontes` section:

```markdown
## Material De Referencia

- `references/sources/`: raw institutional source files, such as PDFs and templates.
- `references/derived/`: developer-facing extracted notes from source files.
- `references/google-docs-setup.md`: reusable Google Docs setup for any UNIP skill.
- `references/docx-setup.md`: reusable DOCX/Word setup for any UNIP skill.
- `skills/<skill-id>/references/`: English operational references loaded by a specific skill.
```

- [ ] **Step 3: Verify README mentions the new skill**

Run:

```bash
rg -n "unip-gerar-capa|Material De Referencia|google-docs-setup.md|docx-setup.md|skills/<skill-id>/references" plugins/unip-abnt/README.md
```

Expected: matches for all five terms.

---

### Task 7: Optional Manifest Prompt Update

**Files:**
- Modify: `plugins/unip-abnt/.codex-plugin/plugin.json`

- [ ] **Step 1: Inspect current prompts**

Run:

```bash
python3 -m json.tool plugins/unip-abnt/.codex-plugin/plugin.json
```

Expected: valid JSON with three `interface.defaultPrompt` strings.

- [ ] **Step 2: Replace one prompt with cover-generation prompt**

If the current prompts still include `"Crie um esqueleto UNIP ABNT."`, replace it with:

```json
"Gere capa e folha de rosto UNIP."
```

Keep the prompt under 128 characters.

- [ ] **Step 3: Validate manifest JSON**

Run:

```bash
python3 -m json.tool plugins/unip-abnt/.codex-plugin/plugin.json
```

Expected: valid formatted JSON output and exit code `0`.

---

### Task 8: Validate Skill And References

**Files:**
- Verify: `plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md`
- Verify: `plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md`
- Verify: `plugins/unip-abnt/references/google-docs-setup.md`
- Verify: `plugins/unip-abnt/references/docx-setup.md`
- Verify: `plugins/unip-abnt/.codex-plugin/plugin.json`
- Verify: `claude-plugin/marketplace.json`

- [ ] **Step 1: Check required files exist**

Run:

```bash
test -f plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md
test -f plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md
test -f plugins/unip-abnt/references/google-docs-setup.md
test -f plugins/unip-abnt/references/docx-setup.md
```

Expected: all commands exit `0`.

- [ ] **Step 2: Check no placeholder markers were introduced**

Run:

```bash
rg --hidden "\\[TODO|TODO|TBD" plugins/unip-abnt/skills/unip-gerar-capa plugins/unip-abnt/README.md plugins/unip-abnt/.codex-plugin/plugin.json -g '!.git/**'
```

Expected: exit code `1` with no matches.

- [ ] **Step 3: Check references are in English**

Run:

```bash
rg -n "Fonte:|Formatacao|Folha De Rosto|Nao |Paginacao|obrigatoria" plugins/unip-abnt/skills/unip-gerar-capa/references plugins/unip-abnt/references/google-docs-setup.md plugins/unip-abnt/references/docx-setup.md
```

Expected: exit code `1` with no matches.

- [ ] **Step 4: Validate JSON files**

Run:

```bash
python3 -m json.tool plugins/unip-abnt/.codex-plugin/plugin.json
python3 -m json.tool claude-plugin/marketplace.json
```

Expected: both commands output formatted JSON and exit `0`.

- [ ] **Step 5: Show final file tree**

Run:

```bash
find plugins/unip-abnt/skills/unip-gerar-capa -maxdepth 4 -type f -print | sort
test -f plugins/unip-abnt/references/google-docs-setup.md
test -f plugins/unip-abnt/references/docx-setup.md
```

Expected `find` output:

```text
plugins/unip-abnt/skills/unip-gerar-capa/SKILL.md
plugins/unip-abnt/skills/unip-gerar-capa/references/cover-and-title-page-formatting.md
```

Expected `test` commands: exit `0`.

---

### Task 9: Review And Commit

**Files:**
- Review all files changed by this plan.

- [ ] **Step 1: Review git diff**

Run:

```bash
git diff -- plugins/unip-abnt/skills/unip-gerar-capa plugins/unip-abnt/references/google-docs-setup.md plugins/unip-abnt/references/docx-setup.md plugins/unip-abnt/README.md plugins/unip-abnt/.codex-plugin/plugin.json
```

Expected: diff only includes the new skill, plugin-level setup references, README documentation, and optional prompt update.

- [ ] **Step 2: Check git status**

Run:

```bash
git status --short
```

Expected: changed files are limited to this feature plus any pre-existing unrelated user changes.

- [ ] **Step 3: Commit if requested by the user**

Only commit if the user explicitly asks for a commit.

Run:

```bash
git add plugins/unip-abnt/skills/unip-gerar-capa plugins/unip-abnt/references/google-docs-setup.md plugins/unip-abnt/references/docx-setup.md plugins/unip-abnt/README.md plugins/unip-abnt/.codex-plugin/plugin.json
git commit -m "feat(unip-abnt): add cover generation skill"
```

Expected: commit succeeds.

---

## Self-Review

Spec coverage:

- Creates `unip-gerar-capa`: covered by Task 1.
- Creates references in English: covered by Tasks 2, 3, 4 and Task 8 Step 3.
- Includes base cover/title-page formatting reference: covered by Task 2.
- Includes reusable Google Docs setup reference: covered by Task 3.
- Includes reusable DOCX setup reference: covered by Task 4.
- References indicate what to do for a specific plugin/skill/document type: covered by Task 1 routing, Task 2 skill reference, and Task 5 routing verification.
- Unknown target document type requires a user question before final output: covered by Task 1 core behavior and Task 5 routing verification.
- Does not implement before planning: this document is only a plan.

Placeholder scan:

- The plan intentionally includes placeholders inside generated templates such as `NOME DO ALUNO`, `CIDADE`, and catalog-card insertion markers because the skill must use placeholders instead of inventing academic data.
- No `TODO` or `TBD` placeholders are used as implementation gaps.

Type and path consistency:

- Skill path is consistently `plugins/unip-abnt/skills/unip-gerar-capa/`.
- Base reference is consistently `references/cover-and-title-page-formatting.md`.
- Plugin-level Google Docs setup is consistently `plugins/unip-abnt/references/google-docs-setup.md`.
- Plugin-level DOCX setup is consistently `plugins/unip-abnt/references/docx-setup.md`.
