# UNIP ABNT

Plugin institucional do EasyABNT para apoiar escrita, estruturacao e revisao de documentos academicos da Universidade Paulista (UNIP).

## Escopo

Este plugin deve concentrar regras especificas da UNIP, mantendo o plugin `easy-abnt` como base generica para ABNT.

Use este plugin para:

- estruturar trabalhos academicos conforme modelo institucional da UNIP;
- revisar textos, citacoes e referencias com foco em exigencias locais;
- registrar pendencias quando uma regra depender de manual, template ou orientacao da instituicao;
- evitar invencao de dados bibliograficos, fontes ou normas.

## Skills

- `unip-gerar-capa`: creates or reviews UNIP cover pages, title pages, contracapa requests, Google Docs-oriented outputs, and DOCX-ready outputs.

## Fontes

As regras especificas da UNIP ainda precisam ser preenchidas com fontes oficiais.

Fontes esperadas:

- manual de trabalhos academicos da UNIP;
- template oficial de TCC, artigo ou projeto;
- orientacoes da biblioteca;
- normas do curso, edital, disciplina ou professor orientador.

## Material De Referencia

- `references/sources/`: raw institutional source files, such as PDFs and templates.
- `references/derived/`: developer-facing extracted notes from source files.
- `references/google-docs-setup.md`: reusable Google Docs setup for any UNIP skill.
- `references/docx-setup.md`: reusable DOCX/Word setup for any UNIP skill.
- `skills/<skill-id>/references/`: English operational references loaded by a specific skill.

## Estrutura

```text
plugins/unip-abnt/
├── .codex-plugin/plugin.json
├── .mcp.json
├── .app.json
├── README.md
├── assets/
├── hooks/
├── references/
│   ├── google-docs-setup.md
│   ├── docx-setup.md
│   ├── derived/
│   └── sources/
├── scripts/
└── skills/
    └── unip-gerar-capa/
        ├── SKILL.md
        └── references/
            └── cover-and-title-page-formatting.md
```

## Status

Versao inicial: `0.1.0`.

As regras institucionais ainda estao em modo de bootstrap e devem ser completadas com fontes verificaveis antes de uso rigoroso.
