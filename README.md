# Predição da Nota de Redação do ENEM com ANFIS

**Laboratório de Inteligência Artificial — Tópicos Especiais em Computação Aplicada**  
**CEFET-MG · 2026**

> Modelo neuro-fuzzy (ANFIS) para estimar a nota de redação do ENEM a partir de variáveis socioeconômicas, com validação externa em estudantes de cursinho popular.

---

## Sobre o projeto

Este trabalho propõe o desenvolvimento de um modelo preditivo baseado em **Sistemas Neuro-Fuzzy Adaptativos (ANFIS)** para estimar a nota da redação do ENEM utilizando exclusivamente variáveis socioeconômicas disponíveis nos microdados oficiais do exame.

O objetivo é investigar se informações de contexto familiar e escolar — coletadas antes da realização das provas — são capazes de fornecer estimativas úteis do desempenho dos candidatos, viabilizando o uso do modelo como ferramenta de **triagem pedagógica antecipada**.

### Variáveis de entrada utilizadas

| Variável | Descrição |
|---|---|
| `TP_DEPENDENCIA_ADM_ESC` | Tipo de dependência administrativa da escola |
| `Q002` | Nível de escolaridade da mãe |
| `Q020` | Acesso à internet em casa |

### Variável de saída

| Variável | Descrição |
|---|---|
| `NU_NOTA_REDACAO` | Nota da redação do ENEM (0 a 1000 pontos) |

---

## Estrutura do repositório

```
📦 Trabalho-Final-IA
 ┣ 📓 Trabalhofinal_IASamara.ipynb               # Notebook principal com todo o pipeline
 ┣ 📄 README.md              # Este arquivo
 ┗ 📄 instrucoes_dataset.md  # Como obter os microdados do ENEM
```

---

## Pipeline do projeto

```
Microdados ENEM (INEP)
        │
        ▼
 Pré-processamento
 • Filtro: TP_STATUS_REDACAO == 1
 • Filtro: SG_UF_ESC == 'MG'
 • Filtro: NU_NOTA_REDACAO > 0
 • Remoção de nulos (dropna)
 • Codificação ordinal de variáveis categóricas
        │
        ▼
 Seleção de variáveis
 • TP_DEPENDENCIA_ADM_ESC, Q002, Q020
        │
        ▼
 Modelo ANFIS
 • 3 entradas × 3 funções de pertinência gaussianas
 • Sistema Takagi-Sugeno de ordem zero
 • 21 parâmetros ajustáveis
 • Otimização: Nelder-Mead (300 iterações)
        │
        ├──────────────────────────┐
        ▼                          ▼
 Validação interna           Validação externa
 20% dos microdados          11 alunos de cursinho popular
 (conjunto de teste)         (formulário socioeconômico)
```

---

## Como reproduzir os resultados

### 1. Clone o repositório

```bash
git clone https://github.com/Samara19Narciso/Trabalho-Final-IA-.git
cd Trabalho-Final-IA-
```

### 2. Instale as dependências

```bash
pip install pandas numpy scikit-fuzzy scikit-learn scipy matplotlib openpyxl
```

### 3. Obtenha os microdados do ENEM

Os microdados não estão incluídos neste repositório por serem arquivos grandes se encontram no link abaixo do drive: https://drive.google.com/drive/folders/1g3Aqfj3uuLlyL4hebQji_ac3e1u8kjKn?usp=sharing

### 4. Execute o notebook

Abra o arquivo `Trabalhofinal_IASamara.ipynb` no Jupyter Notebook ou Google Colab e execute as células em ordem.

```bash
jupyter notebook Trabalhofinal_IASamara.ipynb
```

---

## Métricas de avaliação

O desempenho do modelo é avaliado por quatro métricas:

| Métrica | Descrição |
|---|---|
| **MAE** | Erro Absoluto Médio — desvio médio em pontos |
| **MSE** | Erro Quadrático Médio — penaliza erros maiores |
| **R²** | Coeficiente de Determinação — variância explicada |
| **Erro Relativo Médio (%)** | Erro percentual médio em relação à nota real |

---

## Validação externa — Cursinho popular

Como etapa adicional de validação, foi aplicado um formulário socioeconômico a **11 estudantes de um cursinho popular**. As respostas foram inseridas diretamente no modelo treinado e as notas previstas foram comparadas às notas reais obtidas no ENEM, permitindo avaliar a capacidade de generalização do modelo em um contexto educacional real.

| Aluno | Escolaridade da mãe | Nota real | Nota prevista |
|---|---|---|---|
| 1 | Médio completo | 720 | — |
| 2 | Fundamental incompleto | 600 | — |
| 3 | Superior completo | 760 | — |
| 4 | Médio incompleto | 700 | — |
| 5 | Médio completo | 840 | — |
| 6 | Médio completo | 720 | — |
| 7 | Médio completo | 840 | — |
| 8 | Superior completo | 880 | — |
| 9 | Médio completo | 840 | — |
| 10 | Fundamental incompleto | 600 | — |
| 11 | Médio completo | 820 | — |

> Preencha a coluna "Nota prevista" com os valores gerados na execução do notebook.

---

## Tecnologias utilizadas

| Tecnologia | Uso |
|---|---|
| Python 3 | Linguagem principal |
| pandas | Manipulação e pré-processamento dos dados |
| numpy | Operações numéricas |
| scikit-fuzzy | Funções de pertinência gaussianas |
| scipy | Otimização Nelder-Mead |
| scikit-learn | Métricas de avaliação |
| matplotlib | Visualização dos resultados |

---

## Autor

**Samara Narciso**  
CEFET-MG · Laboratório de Inteligência Artificial · 2026

---

## Referência dos dados

INEP — Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira.  
**Microdados do ENEM.** Disponível em: https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem

---

## Licença

Este projeto está disponível para fins acadêmicos e educacionais.
