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
