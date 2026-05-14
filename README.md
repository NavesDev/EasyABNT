# EasyABNT🇧🇷

Plugin local para orientar agentes de IA na escrita, estruturacao e revisao de documentos academicos conforme praticas ABNT.

## Objetivo

O EasyABNT fornece um conjunto inicial de instrucoes para que a IA ajude a produzir documentos como TCC, artigo cientifico, projeto de pesquisa, relatorio tecnico e monografia. O foco inicial e:

- estruturar elementos pre-textuais, textuais e pos-textuais;
- sugerir linguagem academica clara e impessoal;
- revisar consistencia de citacoes e referencias;
- sinalizar lacunas que precisam de confirmacao humana;
- evitar inventar fontes, normas, dados ou referencias.

## Estrutura

```text
.
├── README.md
└── plugins/
    └── easy-abnt/
        ├── .codex-plugin/plugin.json
        ├── .mcp.json
        ├── .app.json
        ├── README.md
        ├── marketplace.example.json
        ├── assets/
        ├── hooks/
        ├── scripts/
        └── skills/
            └── abnt-document-writer/
                ├── SKILL.md
                └── references/
                    └── abnt-writing-checklist.md
```

## Marketplace

O arquivo canonico do marketplace deveria ficar em `.agents/plugins/marketplace.json`. Neste ambiente, `.agents` esta somente leitura, entao foi criado um exemplo em:

```text
plugins/easy-abnt/marketplace.example.json
```

Quando `.agents` estiver gravavel, copie o conteudo equivalente para `.agents/plugins/marketplace.json`.

## Status

Versao inicial: `0.1.0`. A base ainda deve receber validacao contra normas ABNT especificas e templates finais de saida.

## Adicione sua instituicao

Se voce e estudante, professor, orientador ou pesquisador, contribua adicionando as regras da sua instituicao academica como um plugin proprio do marketplace. A ideia e que cada instituicao tenha um pacote separado, por exemplo `unip-abnt`, para preservar manuais, modelos e excecoes locais sem misturar tudo no plugin generico.

Ao contribuir, inclua sempre a fonte das regras institucionais quando possivel, como manual de trabalhos academicos, template oficial, edital, guia do curso ou orientacao formal da biblioteca.

## Comunidade

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing e padroes Git](CONTRIBUTING.md)
