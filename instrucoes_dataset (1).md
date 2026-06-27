# Como obter os dados utilizados neste projeto

## Opção 1 — Download direto (recomendado)

Os arquivos `dados_1.xlsx` e `dados_2.xlsx` utilizados neste projeto estão disponíveis para download no Google Drive:

📁 **[Clique aqui para acessar os dados](https://drive.google.com/drive/folders/1g3Aqfj3uuLlyL4hebQji_ac3e1u8kjKn?usp=sharing)**

Baixe os dois arquivos e coloque-os na **raiz do repositório** (mesma pasta do notebook `v1.ipynb`) antes de executar o código.

```
📦 Trabalho-Final-IA-
 ┣ 📓 v1.ipynb
 ┣ 📊 dados_1.xlsx   ← coloque aqui
 ┣ 📊 dados_2.xlsx   ← coloque aqui
 ┣ 📄 README.md
 ┗ 📄 instrucoes_dataset.md
```

---

## Opção 2 — Obter diretamente do INEP

Caso prefira baixar os microdados originais do ENEM diretamente da fonte oficial:

### 1. Acesse o portal do INEP

https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem

### 2. Baixe e extraia o arquivo

Escolha o ano desejado e baixe o `.zip`. Dentro você encontrará:

```
MICRODADOS_ENEM_XXXX/
 ┣ DADOS/
 ┃ ┗ MICRODADOS_ENEM_XXXX.csv   ← arquivo principal
 ┗ DICIONARIO/
   ┗ Dicionario_Microdados_Enem_XXXX.xlsx
```

### 3. Carregue apenas as colunas necessárias

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

### 4. Gere os dois arquivos Excel

```python
metade = len(df) // 2
df.iloc[:metade].to_excel('dados_1.xlsx', index=False)
df.iloc[metade:].to_excel('dados_2.xlsx', index=False)
```

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

Os arquivos CSV dos microdados do ENEM utilizam encoding `latin-1` e separador `;`.  
Certifique-se de passar esses parâmetros ao ler o arquivo com pandas.
