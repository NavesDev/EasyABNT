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
