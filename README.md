# Projeto AED — Uber Ride Analytics Dashboard (Kaggle)

Este projeto executa uma **Análise Exploratória de Dados (AED)** simples (nível Introdução à IA) usando o dataset do Kaggle:

- Dataset: **Uber Data Analytics Dashboard**
- Link: https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard/data



---

## 1) Estrutura do projeto

```
uber_aed_project/
  data/
    raw/                 # ncr_ride_bookings
    processed/           # saída: base limpa
  outputs/
    figures/             # gráficos gerados (PNG)
    report.md            # relatório automático (Markdown)
  src/
    eda_uber.py          # script principal de AED
  requirements.txt
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


