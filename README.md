# VILLEFORT · Portal de Ferramentas

> Portal web com 6 ferramentas de processamento de dados para prefeituras e órgãos públicos.  
> Tudo roda **100% no navegador** — nenhum dado é enviado para servidor.

---

## Como usar

1. Baixe o arquivo `villefort_portal.html`
2. Abra no navegador (Chrome ou Edge recomendado)
3. Escolha a ferramenta no menu lateral
4. Carregue o arquivo e clique em **Processar**

Não requer instalação, servidor ou conexão com internet após o carregamento.

---

## Ferramentas

### 1 · Castanhal — Processador TXT → CSV

Lê um arquivo `.txt` delimitado por `;` e gera três CSVs separados com base no prefixo da primeira coluna.

| Arquivo gerado | Regra de filtro |
|---|---|
| `servidor_<sufixo>.csv` | Linhas cujo campo 1 começa com `F` |
| `movimentacao_<sufixo>.csv` | Linhas cujo campo 1 começa com `D` ou `P` |
| `evento_<sufixo>.csv` | Colunas 6, 7 e 1 das linhas D/P — deduplicado |

**Encoding de entrada:** ISO-8859-1 (Latin-1)  
**Encoding de saída:** UTF-8 com BOM (compatível com Excel)

---

### 2 · Codó / MA — Conversor de Folha de Pagamento (XLSX)

Processa planilhas de folha no formato horizontal (wide) e gera CSVs estruturados.

**Seção A — Folha de Pagamento**
- Entrada: um ou mais arquivos `.xlsx`
- Saída: `movimentacao_<sufixo>.csv` (Registro; Atributo; Valor) e `evento_<sufixo>.csv` (COD; DES)

**Seção B — Cadastro de Servidores**
- Entrada: um ou mais arquivos `.xlsx`
- Saída: `servidor_<sufixo>.csv`
- CPF limpo (remove pontuação), datas convertidas de serial Excel para `dd/mm/aaaa`, coluna `Tipo = EFETIVOS` adicionada automaticamente

---

### 3 · Santo Antônio da Patrulha — Processador de Eventos (XLSX)

Lê relatórios gerenciais `.xlsx` com eventos agrupados e exporta um CSV consolidado.

- **Saída:** `Movimentacao_<sufixo>.csv`
- **Colunas:** `Matrícula; Nome; Valor; Evento; Descrição`
- Suporte a múltiplos arquivos processados em lote

---

### 4 · Renomeador de Arquivos com Data

Adiciona prefixo `MM_AAAA_` (e complemento opcional) ao nome dos arquivos.

- Aceita qualquer tipo de arquivo
- **Extrai ZIPs automaticamente** e renomeia o conteúdo
- Prévia com checkboxes antes do download
- Baixa os arquivos renomeados num único ZIP

**Exemplo:**
```
BANCO_DIGIO.xlsx  →  06_2025_RELATORIO_BANCO_DIGIO.xlsx
```

---

### 5 · Processador de Matrícula (Excel)

Insere hífen antes do último dígito da coluna `MATRÍCULA`, copia o valor para `MATRÍCULA ORIGEM` e exporta o arquivo com prefixo de data.

- **Entrada:** `.xlsx` / `.xls`
- **Transformação:** `2100015` → `210001-5`
- **Saída:** `MM_AAAA_<nome_original>.xlsx`

---

### 6 · Porto Nacional — Fechamento / Comparador TXT

Filtra linhas do Arquivo 1 que contenham `00100000600`, compara a matrícula (campo 1) com o campo 2 do Arquivo 2 (CSV) e gera três saídas.

| Arquivo gerado | Conteúdo |
|---|---|
| `dados_validados.csv` | Linhas com match |
| `excecoes_sem_match.csv` | Linhas sem match, com número de linha original |
| `<nome>_ajustado.txt` | Arquivo 1 limpo, sem as exceções (e sem intervalo de linhas removido, se configurado) |

---

## Tecnologias

| Biblioteca | Versão | Uso |
|---|---|---|
| [SheetJS (xlsx)](https://sheetjs.com) | 0.18.5 | Leitura e escrita de arquivos Excel |
| [JSZip](https://stuk.github.io/jszip/) | 3.10.1 | Criação e extração de arquivos ZIP |
| [Inter](https://rsms.me/inter/) | — | Tipografia da interface |
| [JetBrains Mono](https://www.jetbrains.com/legalnotices/mono/) | — | Tipografia de código e dados |

Todas as dependências são carregadas via CDN na primeira abertura.

---

## Estrutura do projeto

```
villefort_portal.html   # Arquivo único — toda a aplicação
README.md               # Este arquivo
```

---

## Compatibilidade

| Navegador | Suporte |
|---|---|
| Chrome 90+ | ✅ Recomendado |
| Edge 90+ | ✅ |
| Firefox 88+ | ✅ |
| Safari 14+ | ✅ |

---

## Privacidade

Nenhum arquivo é enviado para servidores externos. Todo o processamento ocorre localmente via [File API](https://developer.mozilla.org/en-US/docs/Web/API/File_API) do navegador.

---

## Licença

Uso interno. Distribuição restrita.
