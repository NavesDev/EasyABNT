# UNIP ABNT

Plugin institucional do EasyABNT para apoiar escrita, estruturacao e revisao de documentos academicos da Universidade Paulista (UNIP).

## Escopo

Este plugin deve concentrar regras especificas da UNIP, mantendo o plugin `easy-abnt` como base generica para ABNT.

Use este plugin para:

- estruturar trabalhos academicos conforme modelo institucional da UNIP;
- revisar textos, citacoes e referencias com foco em exigencias locais;
- registrar pendencias quando uma regra depender de manual, template ou orientacao da instituicao;
- evitar invencao de dados bibliograficos, fontes ou normas.

## Fontes

As regras especificas da UNIP ainda precisam ser preenchidas com fontes oficiais.

Fontes esperadas:

- manual de trabalhos academicos da UNIP;
- template oficial de TCC, artigo ou projeto;
- orientacoes da biblioteca;
- normas do curso, edital, disciplina ou professor orientador.

## Estrutura

```text
plugins/unip-abnt/
├── .codex-plugin/plugin.json
├── .mcp.json
├── .app.json
├── README.md
├── assets/
├── hooks/
├── scripts/
└── skills/
    └── unip-abnt-document-writer/
        ├── SKILL.md
        └── references/
            └── unip-abnt-checklist.md
```

## Status

Versao inicial: `0.1.0`.

As regras institucionais ainda estao em modo de bootstrap e devem ser completadas com fontes verificaveis antes de uso rigoroso.
