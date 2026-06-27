# Como obter os microdados do ENEM

Os microdados do ENEM são disponibilizados gratuitamente pelo INEP e não estão incluídos neste repositório por conta do tamanho dos arquivos (vários GB).

## Passo a passo

### 1. Acesse o portal do INEP

Entre em: https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem

### 2. Baixe os microdados

Escolha o ano desejado e baixe o arquivo `.zip` correspondente.

### 3. Extraia o arquivo

Descompacte o `.zip`. Dentro você encontrará uma pasta com os seguintes arquivos principais:

```
MICRODADOS_ENEM_XXXX/
 ┣ DADOS/
 ┃ ┗ MICRODADOS_ENEM_XXXX.csv   ← arquivo principal (vários GB)
 ┗ DICIONARIO/
   ┗ Dicionario_Microdados_Enem_XXXX.xlsx  ← descrição das variáveis
```

### 4. Colunas necessárias para este projeto

O notebook utiliza as seguintes colunas do CSV de microdados. Você pode usar pandas para carregar apenas essas colunas e economizar memória:

```python
import pandas as pd

colunas_necessarias = [
    'SG_UF_ESC',
    'TP_STATUS_REDACAO',
    'NU_NOTA_REDACAO',
    'TP_DEPENDENCIA_ADM_ESC',
    'Q002',
    'Q020'
]

df = pd.read_csv(
    'MICRODADOS_ENEM_XXXX.csv',
    sep=';',
    encoding='latin-1',
    usecols=colunas_necessarias
)
```

### 5. Divida em dois arquivos Excel

O notebook espera dois arquivos `.xlsx` na raiz do projeto. Você pode gerá-los assim:

```python
metade = len(df) // 2
df.iloc[:metade].to_excel('dados_1.xlsx', index=False)
df.iloc[metade:].to_excel('dados_2.xlsx', index=False)
```

Ou simplesmente salve tudo em um único arquivo e adapte a primeira célula do notebook para ler apenas `dados_1.xlsx`.

---

## Dicionário das variáveis utilizadas

| Variável | Descrição | Valores |
|---|---|---|
| `SG_UF_ESC` | Sigla da UF da escola | Ex: MG, SP, RJ... |
| `TP_STATUS_REDACAO` | Status da redação | 1 = Corrigida normalmente |
| `NU_NOTA_REDACAO` | Nota da redação | 0 a 1000 |
| `TP_DEPENDENCIA_ADM_ESC` | Dependência administrativa da escola | 1=Federal, 2=Estadual, 3=Municipal, 4=Privada |
| `Q002` | Escolaridade da mãe | A=Nunca estudou ... H=Pós-graduação |
| `Q020` | Acesso à internet em casa | A=Não, B=Sim |

---

## Observação sobre encoding

Os arquivos CSV dos microdados do ENEM utilizam encoding `latin-1` (ISO-8859-1) e separador `;`. Certifique-se de passar esses parâmetros ao ler o arquivo com pandas.
