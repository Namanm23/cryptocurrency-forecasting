# 🪙 Cryptocurrency Time Series Analysis and Forecasting

A comprehensive cryptocurrency forecasting platform combining classical statistical models and deep learning for intelligent price prediction. The system achieves **~8.7% average MAPE** using a highly optimized Bidirectional LSTM and compares performance across **Prophet**, **ARIMA**, and **LSTM** models with an interactive Power BI dashboard.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![Prophet](https://img.shields.io/badge/Prophet-1.1-green.svg)
![Power BI](https://img.shields.io/badge/PowerBI-Dashboard-yellow.svg)
![License](https://img.shields.io/badge/License-MIT-red.svg)

---

## ✨ Key Features

### 📈 Multi-Model Forecasting
- **3 Models Compared**: Facebook Prophet, ARIMA, and Bidirectional LSTM
- **180-Day Future Forecasts** for all 10 cryptocurrencies
- **LSTM wins 10/10** cryptocurrencies with best MAPE scores
- Per-cryptocurrency tuned model configurations for optimal accuracy

### 🧠 Deep Learning Architecture
- **Bidirectional Stacked LSTM**: 128 + 64 units with Dropout layers
- **6 Input Features**: Close, Volume, MA_7, MA_30, Daily_Return, Volatility_7
- **90-Day Lookback Window** for rich sequential context
- Huber loss function — robust to volatile crypto price outliers

### 📊 Interactive Power BI Dashboard
- **8 fully interactive pages** with dark theme and gold color scheme
- Real-time coin slicer with date range filtering
- Forecast comparison page with all 3 models overlaid
- LSTM Deep Dive with 30/90/180-day forward predictions

### 🔬 Comprehensive Analysis
- **Correlation Analysis**: BTC market influence, pairwise crypto correlations
- **Volatility Analysis**: Annualized volatility, Sharpe ratio, market stress index
- **Model Comparison**: MAPE heatmap, radar chart, win count visualization

---

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Power BI Desktop (for dashboard)
- Jupyter Notebook or VS Code

### Installation & Setup

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/cryptocurrency-forecasting.git
cd cryptocurrency-forecasting

# 2. Create and activate virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS/Linux

# 3. Install dependencies
pip install -r requirements.txt
```

### Running the Notebooks

```bash
# Launch Jupyter Notebook
jupyter notebook

# Run notebooks in this exact order:
# 01 → 02 → 03 → 04 → 05 → 06 → 07 → 08
```

### Open Power BI Dashboard

Open `dashboards/Final Dashboard.pbix` in **Power BI Desktop**

---

## 🤖 Model Architecture & Performance

### LSTM Architecture

**Base Model:** Bidirectional Stacked LSTM (TensorFlow/Keras)
- Reads sequences both forward and backward for richer temporal context
- Stacked bidirectional layers for learning complex non-linear patterns
- Optimized with Dropout regularization to prevent overfitting on crypto data

**Custom Architecture:**
```
Input (90 days × 6 features)
    → Bidirectional LSTM (128 units, return_sequences=True)
    → Dropout (0.3)
    → Bidirectional LSTM (64 units)
    → Dropout (0.3)
    → Dense (32, ReLU)
    → Dense (1) → Predicted Close Price
```

### Training Configuration

| Parameter | Value |
|-----------|-------|
| **Lookback Window** | 90 days |
| **Forecast Horizon** | 180 days |
| **Input Features** | 6 (Close, Volume, MA_7, MA_30, Daily_Return, Volatility_7) |
| **Max Epochs** | 100 (EarlyStopping applied) |
| **Batch Size** | 32 |
| **Optimizer** | Adam (lr=0.001) |
| **Loss Function** | Huber (robust to outliers) |
| **Data Split** | 70% Train / 15% Val / 15% Test |
| **EarlyStopping Patience** | 15 epochs |

### Model Performance — LSTM vs ARIMA vs Prophet

| Crypto | Prophet MAPE | ARIMA MAPE | LSTM MAPE | Winner |
|--------|-------------|------------|-----------|--------|
| BNB | 20.52% | 13.51% | 3.08% | ✅ LSTM |
| LTC | 100.36% | 28.21% | 2.98% | ✅ LSTM |
| ETH | 51.60% | 29.96% | 3.76% | ✅ LSTM |
| LINK | 272.82% | 50.90% | 3.44% | ✅ LSTM |
| SOL | 97.51% | 45.58% | 3.73% | ✅ LSTM |
| ADA | 83.89% | 71.73% | 4.46% | ✅ LSTM |
| DOGE | 135.47% | 54.20% | 4.62% | ✅ LSTM |
| BTC | 69.15% | 21.25% | 7.52% | ✅ LSTM |
| XRP | 2673.12% | 32.38% | 11.05% | ✅ LSTM |
| DOT | 150.25% | 64.59% | 38.60% | ✅ LSTM |
| **Average** | **~365%** | **~41.2%** | **~8.7%** | **LSTM (10/10)** |

### Inference Details

| Metric | Value |
|--------|-------|
| **Average LSTM MAPE** | ~8.7% |
| **Average ARIMA MAPE** | ~41.2% |
| **Average Prophet MAPE** | ~365% |
| **Best Performing Crypto** | LTC (LSTM MAPE: 2.98%) |
| **Hardest to Predict** | DOT (LSTM MAPE: 38.60%) |
| **Saved LSTM Models** | 10 × .keras files |

### Training Callbacks

| Callback | Configuration | Purpose |
|----------|--------------|---------|
| EarlyStopping | patience=15, restore_best_weights=True | Stop before overfitting |
| ReduceLROnPlateau | factor=0.5, patience=7, min_lr=1e-6 | Adaptive learning rate |
| ModelCheckpoint | monitor=val_loss, save_best_only=True | Save best weights per crypto |

---

## 📁 Project Structure

```
cryptocurrency-forecasting/
│
├── dashboards/
│   └── Final Dashboard.pbix             # Interactive Power BI Dashboard (8 pages)
│
├── data/
│   ├── raw/                             # 10 raw CSV files downloaded from yfinance
│   │   ├── ADA.csv
│   │   ├── BNB.csv
│   │   ├── BTC.csv
│   │   ├── DOGE.csv
│   │   ├── DOT.csv
│   │   ├── ETH.csv
│   │   ├── LINK.csv
│   │   ├── LTC.csv
│   │   ├── SOL.csv
│   │   └── XRP.csv
│   │
│   ├── processed/
│   │   └── combined_crypto_data.csv     # Cleaned & feature-engineered dataset
│   │
│   ├── correlation/                     # Correlation analysis outputs (6 files)
│   │   ├── close_price_correlation.csv
│   │   ├── close_price_correlation.png
│   │   ├── returns_correlation.csv
│   │   ├── returns_correlation.png
│   │   ├── pairplot_top5.png
│   │   └── rolling_correlation_btc.png
│   │
│   ├── volatility/                      # Volatility analysis outputs (8 files)
│   │   ├── annualized_volatility.png
│   │   ├── monthly_volatility_heatmap.png
│   │   ├── return_distribution.png
│   │   ├── rolling_volatility_all.png
│   │   ├── rolling_volatility_subplots.png
│   │   ├── sharpe_ratio.csv
│   │   ├── sharpe_ratio.png
│   │   └── volatility_summary.csv
│   │
│   ├── forecasts/
│   │   ├── prophet/                     # Prophet outputs (44 files)
│   │   │   ├── {CRYPTO}_forecast.csv
│   │   │   ├── {CRYPTO}_forecast.png
│   │   │   ├── {CRYPTO}_components.png
│   │   │   ├── {CRYPTO}_future.csv
│   │   │   ├── BTC_cross_validation.csv
│   │   │   ├── combined_forecast.csv
│   │   │   ├── model_metrics.csv
│   │   │   └── model_performance_comparison.png
│   │   │
│   │   ├── arima/                       # ARIMA outputs (24 files)
│   │   │   ├── {CRYPTO}_forecast.csv
│   │   │   ├── {CRYPTO}_forecast.png
│   │   │   ├── BTC_acf_pacf.png
│   │   │   ├── combined_forecast.csv
│   │   │   ├── model_metrics.csv
│   │   │   └── model_performance_comparison.png
│   │   │
│   │   └── lstm/                        # LSTM outputs (33 files)
│   │       ├── {CRYPTO}_forecast.csv
│   │       ├── {CRYPTO}_forecast.png
│   │       ├── {CRYPTO}_training_history.png
│   │       ├── combined_forecast.csv
│   │       ├── model_metrics.csv
│   │       └── model_performance_comparison.png
│   │
│   └── model_comparison/                # Comparison outputs (11 files)
│       ├── combined_metrics.csv
│       ├── overall_summary.csv
│       ├── mape_comparison.csv
│       ├── mae_comparison.csv
│       ├── rmse_comparison.csv
│       ├── mape_comparison_bar.png
│       ├── mape_comparison_log.png
│       ├── avg_mape_per_model.png
│       ├── mape_heatmap.png
│       ├── model_wins.png
│       └── radar_chart.png
│
├── models/                              # Saved LSTM .keras model files
│   ├── ADA_lstm.keras
│   ├── BNB_lstm.keras
│   ├── BTC_lstm.keras
│   ├── DOGE_lstm.keras
│   ├── DOT_lstm.keras
│   ├── ETH_lstm.keras
│   ├── LINK_lstm.keras
│   ├── LTC_lstm.keras
│   ├── SOL_lstm.keras
│   └── XRP_lstm.keras
│
├── notebooks/                           # 8 Jupyter notebooks
│   ├── 01_fetch_crypto_data.ipynb
│   ├── 02_data_preprocessing.ipynb
│   ├── 03_correlation_analysis.ipynb
│   ├── 04_volatility_analysis.ipynb
│   ├── 05_prophet_forecasting.ipynb
│   ├── 06_arima_forecasting.ipynb
│   ├── 07_lstm_forecasting.ipynb
│   └── 08_model_comparison.ipynb
│
├── report/
│   └── crypto_report.docx               # Complete project report
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 📓 Notebooks Description

| # | Notebook | Description | Output |
|---|----------|-------------|--------|
| 01 | fetch_crypto_data | Downloads OHLCV data for 10 cryptos from Yahoo Finance via yfinance | 10 raw CSVs |
| 02 | data_preprocessing | Cleans data, handles missing values, engineers 7 new features | combined_crypto_data.csv |
| 03 | correlation_analysis | Correlation matrices, heatmaps, pairplots, rolling BTC correlation | 6 files |
| 04 | volatility_analysis | Annualized volatility, rolling volatility, Sharpe ratio, market stress | 8 files |
| 05 | prophet_forecasting | Prophet with per-crypto tuning, volume regressor, BTC cross-validation | 44 files |
| 06 | arima_forecasting | ARIMA with ADF stationarity test, ACF/PACF analysis, AIC order selection | 24 files |
| 07 | lstm_forecasting | Bidirectional Stacked LSTM, 6 features, EarlyStopping, 90-day lookback | 33 files |
| 08 | model_comparison | Aggregates all metrics, MAPE heatmap, radar chart, win count analysis | 11 files |

---

## 📊 Power BI Dashboard

The interactive dashboard consists of **8 pages** with dark theme and gold color scheme:

| Page | Title | Key Visuals |
|------|-------|-------------|
| 1 | Cryptocurrency Dashboard | Historical price line chart, OHLC KPI cards, ATH/ATL |
| 2 | Price Trends | Close + MA7 + MA30 line chart, Trend Direction card |
| 3 | Performance & Returns | Total return bar, Risk vs Return scatter, Daily Return trend |
| 4 | Risk & Volatility | Volatility ranking bar, Market Stress trend, Daily Range % |
| 5 | Market Correlation | BTC Influence bar chart, Market Movement line, Insight text |
| 6 | Forecast Comparison | Actual vs LSTM vs ARIMA vs Prophet overlay chart |
| 7 | Model Performance | MAPE comparison table, model wins bar, MAPE per crypto chart |
| 8 | LSTM Deep Dive | Actual vs LSTM chart, 30/90/180-day forecast KPI cards |

---

## ⚙️ Feature Engineering

Features engineered from raw OHLCV data in notebook 02:

| Feature | Formula | Purpose |
|---------|---------|---------|
| Daily_Return | (Close_t / Close_t-1 − 1) × 100 | Percentage daily price change |
| Log_Return | log(Close_t / Close_t-1) | Normalized log return |
| Price_Range | High − Low | Intraday volatility proxy |
| MA_7 | 7-day rolling mean of Close | Short-term trend indicator |
| MA_30 | 30-day rolling mean of Close | Medium-term trend indicator |
| Volatility_7 | 7-day rolling std of Daily_Return | Short-term risk measure |
| Cumulative_Return | (Close_t / Close_0 − 1) × 100 | Total return from start date |

---

## 🛠️ Technical Details

### System Requirements
- **OS**: Windows 10+, macOS, or Linux
- **Python**: 3.8 or higher
- **RAM**: 8GB minimum, 16GB recommended
- **Storage**: 2GB for data, models, and outputs
- **GPU**: Optional (CUDA accelerated when available)

### Key Dependencies

| Category | Library |
|----------|---------|
| Data Collection | yfinance |
| Data Processing | pandas, numpy |
| Visualization | matplotlib, seaborn |
| Statistical Models | statsmodels, prophet |
| Deep Learning | tensorflow, keras |
| Evaluation | scikit-learn |
| Dashboard | Power BI Desktop |

---

## 📦 Requirements

```
yfinance
pandas
numpy
matplotlib
seaborn
scikit-learn
statsmodels
prophet
tensorflow
keras
jupyter
python-dotenv
ipykernel
```

Install all dependencies:

```bash
pip install -r requirements.txt
```

---

## 📅 Data Details

| Property | Value |
|----------|-------|
| Source | Yahoo Finance (via yfinance) |
| Date Range | 2021-01-01 to 2025-12-31 |
| Frequency | Daily (OHLCV) |
| Cryptocurrencies | 10 |
| Total Rows | ~18,250 (1,825 per crypto) |
| Features after preprocessing | 14 columns |
| Train / Val / Test Split (LSTM) | 70% / 15% / 15% |
| Forecast Horizon | 180 days |
| Total Output Files | ~157 files |

---

## 🔮 Future Enhancements

- **Real-Time Data Integration** — Connect live APIs (Binance, CoinGecko) for live forecasting
- **Sentiment Analysis** — Include Twitter/Reddit/news sentiment as LSTM input features
- **Hybrid Models** — Combine ARIMA + LSTM or Prophet + XGBoost for ensemble forecasting
- **Technical Indicators** — Add RSI, MACD, Bollinger Bands as additional features
- **Web Deployment** — Deploy as interactive Streamlit or Flask web application
- **Portfolio Forecasting** — Extend to multi-crypto portfolio-level risk analytics
- **Transformer Models** — Explore Temporal Fusion Transformer (TFT) for improved accuracy

---

## 🙏 Acknowledgments

- **Data Source**: [Yahoo Finance](https://finance.yahoo.com/) via [yfinance](https://github.com/ranaroussi/yfinance)
- **LSTM Architecture**: Hochreiter & Schmidhuber (1997) — Long Short-Term Memory
- **Prophet**: Taylor & Letham (2018) — Forecasting at Scale (Facebook Research)
- **ARIMA**: Box & Jenkins (1970) — Time Series Analysis: Forecasting and Control

---

## 📄 License

This project is licensed under the MIT License.

---

**⭐ If you found this project helpful, please consider giving it a star!**
