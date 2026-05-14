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
