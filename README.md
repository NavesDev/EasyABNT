# EasyABNT🇧🇷

Plugin local para orientar agentes de IA na escrita, estruturacao e revisao de documentos academicos conforme praticas ABNT.

## Objetivo

O EasyABNT fornece um conjunto inicial de instrucoes para que a IA ajude a produzir documentos como TCC, artigo cientifico, projeto de pesquisa, relatorio tecnico e monografia. O foco inicial e:

- estruturar elementos pre-textuais, textuais e pos-textuais;
- sugerir linguagem academica clara e impessoal;
- revisar consistencia de citacoes e referencias;
- sinalizar lacunas que precisam de confirmacao humana;
- evitar inventar fontes, normas, dados ou referencias.

## Estrutura do repositorio

```text
.
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── claude-plugin/
│   └── marketplace.json
└── plugins/
    └── <plugin-id>/
        ├── .codex-plugin/plugin.json
        ├── .mcp.json
        ├── .app.json
        ├── README.md
        ├── assets/
        ├── hooks/
        ├── scripts/
        └── skills/
            └── <skill-id>/
                ├── SKILL.md
                └── references/
                    └── <reference>.md
```

Esta estrutura separa o que e fixo no repositorio do que varia por instituicao:

- `claude-plugin/marketplace.json` lista os plugins disponiveis no marketplace local.
- `plugins/easy-abnt/` e o plugin base com regras genericas de escrita academica em ABNT.
- `plugins/<instituicao>-abnt/` deve concentrar regras especificas de uma instituicao, como `unip-abnt`.
- `.codex-plugin/plugin.json` descreve o plugin, sua versao, metadados e capacidades.
- `skills/<skill-id>/SKILL.md` contem o comportamento principal carregado pela IA.
- `skills/<skill-id>/references/` guarda checklists, regras e notas tecnicas carregadas sob demanda.
- `assets/` fica reservado para icones, logos, screenshots e modelos de arquivo.
- `hooks/`, `scripts/`, `.mcp.json` e `.app.json` ficam reservados para integracoes futuras.

## Marketplace

O marketplace do repositorio fica em:

```text
claude-plugin/marketplace.json
```

Cada novo plugin institucional deve ser adicionado nesse arquivo para ficar disponivel no catalogo local.

## Desenvolvimento

Este repositorio deve evoluir como um catalogo de plugins ABNT. O plugin `easy-abnt` funciona como base generica; plugins institucionais devem especializar regras, modelos e excecoes locais sem alterar o comportamento generico.

### Criando um plugin institucional

Use o padrao:

```text
plugins/<instituicao>-abnt/
```

Exemplos:

```text
plugins/unip-abnt/
plugins/usp-abnt/
plugins/ufrj-abnt/
```

Cada plugin institucional deve conter:

- `.codex-plugin/plugin.json` com `name`, `version`, descricao, metadados e capacidades.
- `README.md` com escopo, fontes usadas e limitacoes conhecidas.
- `skills/<skill-id>/SKILL.md` com o comportamento principal da IA.
- `skills/<skill-id>/references/` com checklist, regras locais e notas tecnicas.
- Entrada correspondente em `claude-plugin/marketplace.json`.

### O que entra em cada lugar

- Regras genericas de escrita academica ficam em `plugins/easy-abnt/`.
- Regras de uma instituicao especifica ficam em `plugins/<instituicao>-abnt/`.
- Regras longas, checklists e guias ficam em `skills/<skill-id>/references/`.
- Instrucoes essenciais para a IA ficam em `SKILL.md`.
- Logos, icones, screenshots e templates binarios ficam em `assets/`.
- Scripts de validacao, conversao ou automacao ficam em `scripts/`.

### Fontes e confiabilidade

Ao adicionar regras institucionais, informe a origem sempre que possivel:

- manual oficial de trabalhos academicos;
- template institucional;
- norma interna da biblioteca;
- edital ou guia de curso;
- orientacao formal de professor, coordenacao ou orientador.

Se uma regra nao tiver fonte verificavel, marque como suposicao ou pendencia. O projeto nao deve inventar citacoes, referencias, dados bibliograficos, normas ou requisitos institucionais.

### Validacao local

Valide os manifests JSON antes de enviar mudancas:

```bash
python3 -m json.tool plugins/<plugin-id>/.codex-plugin/plugin.json
python3 -m json.tool claude-plugin/marketplace.json
```

Para revisoes de texto e regras ABNT, confira manualmente:

- se o plugin institucional nao alterou regras genericas indevidamente;
- se toda citacao no texto tem referencia correspondente;
- se referencias incompletas foram marcadas como campos faltantes;
- se as regras locais estao associadas a uma fonte ou pendencia explicita.

### Versionamento de plugins

Cada plugin versiona de forma independente:

- `MAJOR` para mudancas incompatíveis no comportamento ou estrutura do plugin.
- `MINOR` para novos tipos de documento, novos skills, templates ou regras institucionais.
- `PATCH` para correcoes de texto, metadados, pequenos ajustes e clarificacoes.

Commits e pull requests devem seguir os padroes descritos em [CONTRIBUTING.md](CONTRIBUTING.md).

## Status

Versao inicial: `0.1.0`. A base ainda deve receber validacao contra normas ABNT especificas e templates finais de saida.

## Adicione sua instituicao

Se voce e estudante, professor, orientador ou pesquisador, contribua adicionando as regras da sua instituicao academica como um plugin proprio do marketplace. A ideia e que cada instituicao tenha um pacote separado, por exemplo `unip-abnt`, para preservar manuais, modelos e excecoes locais sem misturar tudo no plugin generico.

Ao contribuir, inclua sempre a fonte das regras institucionais quando possivel, como manual de trabalhos academicos, template oficial, edital, guia do curso ou orientacao formal da biblioteca.

## Comunidade

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing e padroes Git](CONTRIBUTING.md)
