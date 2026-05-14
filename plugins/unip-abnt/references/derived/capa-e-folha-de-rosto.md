# Capa E Folha De Rosto - UNIP ABNT

Fonte: `plugins/unip-abnt/references/sources/manual_de_normalizacao_abnt_unip.pdf`

Metadados do PDF:

- Titulo: Guia de Normalizacao ABNT.
- Autor: Universidade Paulista - UNIP.
- Ano: 2025.
- Secoes usadas: `2 Apresentacao do trabalho`, `3.1.1 Capa`, `3.2.1.1 Folha de rosto`, `3.2.1.2 Ficha catalografica`.

## Formatacao Geral Aplicavel

- Papel: A4, `21 x 29,7 cm`.
- Fonte: Arial ou Times New Roman.
- Tamanho principal: `12`.
- Titulo: Arial ou Times New Roman, tamanho `12`, maiusculo e negrito.
- Subtitulo: Arial ou Times New Roman, tamanho `12`, minusculo.
- Margens no anverso: esquerda `3 cm`, superior `3 cm`, direita `2 cm`, inferior `2 cm`.
- Recuo de primeira linha para texto comum: `1,25 cm`.
- Alinhamento do texto comum: justificado.
- Alinhamento de titulos e secoes: esquerda.
- Alinhamento de titulos sem indicacao numerica: centralizado.
- Espacamento principal: `1,5`.
- Bloco de natureza/objetivo do trabalho: espaco simples, fonte tamanho `12`, alinhado do meio da folha para a direita.
- Elementos pre-textuais devem ser impressos no anverso da folha, exceto a ficha catalografica no verso da folha de rosto.

## Capa

Finalidade: protecao externa do trabalho com informacoes indispensaveis para identificacao.

Conteudo exigido pelo modelo:

- `UNIVERSIDADE PAULISTA`.
- Nome do aluno.
- Titulo do trabalho.
- Subtitulo, quando houver.
- Cidade.
- Ano.

Formatacao observada no modelo:

- Conteudo centralizado horizontalmente.
- Nome da instituicao no topo da pagina.
- Nome do aluno abaixo da instituicao.
- Titulo no centro visual da pagina.
- Subtitulo imediatamente abaixo do titulo, quando houver.
- Cidade e ano no rodape visual da pagina.
- Instituicao, nome do aluno, titulo, cidade e ano aparecem em maiusculas no modelo.
- Subtitulo aparece em minusculas no modelo.

Template operacional:

```text
UNIVERSIDADE PAULISTA

NOME DO ALUNO

TITULO DO TRABALHO:
subtitulo

CIDADE
ANO
```

Notas para implementacao:

- Nao adicionar numero de pagina na capa.
- Substituir `CIDADE` e `ANO` pelos dados exigidos na entrega.
- Nao inventar campus, curso, departamento ou orientador na capa sem fonte ou instrucao do usuario.

## Folha De Rosto

Finalidade: pagina pre-textual interna com elementos essenciais de identificacao do trabalho.

Conteudo exigido pelo modelo:

- Nome do aluno.
- Titulo do trabalho.
- Subtitulo, quando houver.
- Bloco de natureza/objetivo.
- Nome da instituicao.
- Nome do curso.
- Orientador.
- Cidade.
- Ano.

Formatacao observada no modelo:

- Nome do aluno centralizado na parte superior.
- Titulo centralizado abaixo do nome do aluno.
- Subtitulo imediatamente abaixo do titulo, quando houver.
- Bloco de natureza/objetivo posicionado do meio da folha para a direita.
- Bloco de natureza/objetivo em espaco simples e fonte tamanho `12`.
- Linha de orientador alinhada com a area do bloco da direita.
- Cidade e ano centralizados no rodape visual da pagina.
- Nome do aluno, titulo, cidade e ano aparecem em maiusculas no modelo.
- Subtitulo aparece em minusculas no modelo.

Template operacional:

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

Notas para implementacao:

- Confirmar o tipo de trabalho antes de preencher o bloco de natureza.
- Confirmar nome do curso, titulacao pretendida e orientador antes de substituir placeholders.
- Nao adicionar numero de pagina na folha de rosto, mas considerar a regra de contagem indicada no manual.

## Contracapa / Verso Da Folha De Rosto

O termo `contracapa` nao aparece como titulo de secao no trecho extraido do manual. A exigencia relacionada e o verso da folha de rosto com ficha catalografica.

Regras extraidas:

- O verso da folha de rosto deve conter a ficha catalografica.
- A ficha catalografica deve seguir o Codigo de Catalogacao Anglo-Americano vigente, conforme o manual.
- O manual orienta gerar a ficha pelo site da instituicao em Servicos, Biblioteca, Ficha catalografica.
- Em formato eletronico, a ficha catalografica deve aparecer imediatamente apos a pagina de rosto.
- O verso da folha de rosto com ficha catalografica nao deve ser contado nem numerado.

Notas para implementacao:

- Se o usuario pedir `contracapa`, confirmar se ele quer dizer `folha de rosto` ou `verso da folha de rosto/ficha catalografica`.
- Nao gerar ficha catalografica falsa. Solicitar a ficha oficial ou os metadados necessarios.

## Paginacao Relacionada

- As folhas sao contadas sequencialmente a partir da folha de rosto.
- A numeracao aparece a partir da Introducao.
- O verso da folha de rosto com ficha catalografica nao e contado nem numerado.
- Numeros de pagina usam algarismos arabicos.
- Posicao do numero de pagina: `2 cm` da margem direita e `2 cm` da margem superior.
