# EasyABNT Plugin

Plugin Codex para escrita e revisao assistida por IA de documentos academicos em padrao ABNT.

## Componentes

- `.codex-plugin/plugin.json`: manifesto do plugin.
- `skills/abnt-document-writer/SKILL.md`: workflow principal usado pela IA.
- `skills/abnt-document-writer/references/abnt-writing-checklist.md`: checklist operacional carregado quando a tarefa exigir revisao ou redacao detalhada.
- `.mcp.json` e `.app.json`: placeholders para futuras integracoes.
- `assets/`, `hooks/` e `scripts/`: pastas reservadas para evolucao do plugin.

## Uso esperado

Acione o plugin quando o usuario pedir para criar, revisar, formatar ou planejar documentos academicos brasileiros com requisitos ABNT.

Exemplos:

- "Crie um esqueleto ABNT para meu TCC sobre educacao inclusiva."
- "Revise a introducao abaixo e aponte problemas de ABNT."
- "Monte referencias ABNT com estas fontes."

## Limites

O plugin deve tratar ABNT como padrao tecnico que pode variar por instituicao, curso e versao de norma. Quando uma regra depender de manual institucional, o agente deve pedir ou usar esse manual como fonte prioritaria.
