# Projeto AED — Uber Ride Analytics Dashboard (Kaggle)

Este projeto executa uma **Análise Exploratória de Dados (AED)** simples (nível Introdução à IA) usando o dataset do Kaggle:

- Dataset: **Uber Data Analytics Dashboard**
- Link: https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard/data

---

## 1) Estrutura do projeto

```
uber_aed_project/
  data/
    raw/                 # ncr_ride_bookings.csv
    processed/           # saída: base limpa
  outputs/
    figures/             # gráficos gerados (PNG)
    report.md            # relatório automático (Markdown)
  src/
    eda_uber.py          # script principal de AED
  requirements.txt       # dependências
```

---

## 2) Ambiente e execução

### 2.1 Criar ambiente e instalar dependências
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate

pip install -r requirements.txt
```

### 2.2 Rodar a AED
```bash
python src/eda_uber.py --data_dir data/raw --out_dir outputs
```

Ao final, o script gera:
- `data/processed/uber_rides_cleaned.csv`
- `outputs/figures/*.png`
- `outputs/report.md`

---

## (Opcional) Baixar o dataset automaticamente com `kagglehub`

Se você preferir não baixar manualmente pelo site, pode usar o script abaixo (na sua máquina):

```bash
pip install kagglehub
python src/download_dataset.py
```

Isso vai copiar os CSVs do dataset para `data/raw/`.


## 3) O que a AED analisa (visão geral)

O script:
1. **Carrega** o CSV principal (automaticamente escolhe o maior CSV, ou um nome conhecido).
2. **Limpa e organiza**:
   - padroniza nomes das colunas
   - cria `datetime` a partir de `Date` + `Time`
   - cria variáveis derivadas: `hour`, `day_of_week`, `month`
   - converte colunas numéricas (distância, valor, ratings, tempos)
   - trata `Avg VTAT` ausente com fallback em `Avg CTAT`
   - remove duplicatas por `Booking ID` (quando existir)
3. **Explora** padrões:
   - distribuição de *Booking Status*
   - série temporal diária de volume de corridas
   - heatmap **dia da semana x hora**
   - tipos de veículo e valor mediano por tipo
   - dispersão **distância x valor**
   - histogramas de *Driver Ratings* e *Customer Rating*
4. **Gera relatório** automático em Markdown com estatísticas e uma lista das figuras.

---

## 4) Possíveis aplicações em IA (para uso futuro)

- **Classificação**: prever `Booking Status` (Completed vs Cancelled/No Driver Found/Incomplete) com base em horário, tipo de veículo, local, distância, etc.
- **Regressão**: prever `Booking Value` usando `Ride Distance`, horário, tipo de veículo e variáveis contextuais.
- **Anomalias**: detectar corridas com valor fora do padrão para a distância/horário.

---

## 5) Como entregar (.zip/.rar)

1. Baixe o dataset do Kaggle e copie o(s) CSV(s) para `data/raw/`.
2. Rode o script para gerar `outputs/` e `data/processed/`.
3. Compacte a pasta do projeto inteira em `.zip` ou `.rar`, garantindo que o tamanho final fique <= 20 MB.

Dica: se o dataset for grande, verifique o limite do trabalho e, se necessário, inclua apenas o CSV principal (ou uma amostra justificada) **se o professor permitir**.

---

## 6) Notebook do Kaggle (execução no ambiente Kaggle)

Este projeto também inclui o notebook `notebooks/uber-analytics.ipynb`, que pode ser importado no Kaggle e executado usando o dataset como *Input*.

**Dica (Kaggle):**
- Depois de adicionar o dataset como *Input*, o Kaggle monta os arquivos em `/kaggle/input/<nome-do-dataset>/`.
- Neste dataset, o CSV principal é `ncr_ride_bookings.csv`.
- Exemplo de leitura no Kaggle:

```python
import pandas as pd
csv_path = "/kaggle/input/datasets/yashdevladdha/uber-ride-analytics-dashboard/ncr_ride_bookings.csv"
df = pd.read_csv(csv_path)
```

---

## 7) Checklist de conformidade com a entrega

Dentro do `.zip` você encontrará:
- **Código-fonte:** `src/eda_uber.py` (pipeline AED) + `src/download_dataset.py` (coleta via kagglehub, opcional)
- **Dataset utilizado:** `data/raw/ncr_ride_bookings.csv`
- **Visualizações geradas:** `outputs/figures/*.png` (geradas ao rodar o script)
- **Documentação:** `README.md` (este arquivo) + `outputs/report.md` (relatório automático)
- **Artefatos adicionais (do dataset):** `outputs/Uber.pbix` e `outputs/dashboard.gif`

Para reproduzir do zero:
1. (Opcional) rode `python src/download_dataset.py` **ou** coloque o CSV em `data/raw/`
2. rode `python src/eda_uber.py --data_dir data/raw --out_dir outputs`
3. verifique `outputs/figures/` e `outputs/report.md`

