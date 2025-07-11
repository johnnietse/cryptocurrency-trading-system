# Cryptocurrency Trading System

## Overview
This Cryptocurrency Trading System is a sophisticated Python framework (more like a design concept for an actual system) for algorithmic trading that features multi-asset support, technical indicators, backtesting capabilities, and performance analytics. This system implements a dual moving average crossover strategy to generate trading signals and provides comprehensive portfolio simulation.

## Examples
### BTC-USD
![download (8)](https://github.com/user-attachments/assets/263ef957-6b27-4680-bf73-b66675a6ab6b)
![download (9)](https://github.com/user-attachments/assets/c7c362ce-bcec-49af-8ade-331c2e43d669)
### ETH-USD
![download (10)](https://github.com/user-attachments/assets/21678f29-e8f4-48df-abd6-2b240ac9bf65)
![download (11)](https://github.com/user-attachments/assets/d6559b6f-ac5d-497e-bf62-8c52298b89e3)


## Key Features
- Multi-Asset Support: Simultaneously analyze multiple cryptocurrencies (BTC, ETH, etc.)
- Technical Indicators: Dual moving average crossover strategy
- Backtesting Engine: Simulate trading strategies with configurable capital
- Performance Metrics: Sharpe ratio, volatility, max drawdown, and more
- Visual Analytics: Professional-grade visualizations of signals and performance
- Modular Architecture: Easily extendable components for custom strategies

## System Architecture

`Data Acquisition` --> `Technical Analysis` --> `Backtesting` --> `Performance Analytics` --> `Visualization`

    
## Modules
1. Data Acquisition with the `CryptoDataFetcher` function
- Fetches historical market data from Yahoo Finance
- Supports multiple assets and customizable timeframes
- Automatic data cleaning and normalization

2. Technical Analysis with the `TradingSignalsGenerator` function 
- Computes fast (10-period) and slow (40-period) moving averages
- Generates buy/sell signals based on MA crossovers
- Signal visualization with entry/exit markers

3. Backtesting Framework with the `PortfolioSimulator` function
- Simulates strategy performance with configurable starting capital
- Tracks strategy returns vs buy-and-hold benchmark
- Calculates position-based returns with realistic assumptions

4. Visualization with the `TradingVisualizer` function
- Professional trading charts with technical indicators
- Portfolio performance comparison visuals
- Publication-quality figures with high DPI settings

5. Performance Analytics
- Key metrics: Sharpe ratio, annual volatility, max drawdown
- Strategy vs buy-and-hold comparison
- Risk-adjusted return calculations

## Installation & Dependencies
```bash
pip install yfinance pandas numpy matplotlib seaborn scikit-learn
```

## Usage
```python
if __name__ == "__main__":
    # Configuration
    ASSETS = ['BTC-USD', 'ETH-USD']  # Add more assets as needed
    START = '2020-01-01'
    END = '2020-12-31'
    INITIAL_CAPITAL = 10000.0

    # Data pipeline
    data_engine = CryptoDataFetcher(ASSETS, START, END)
    market_datasets = data_engine.fetch_market_data()

    for symbol, dataset in market_datasets.items():
        print(f"\nProcessing {symbol}:")
        print("=" * 50)

        # Signal generation
        analysis_engine = TradingSignalsGenerator(dataset)
        # Compute moving averages and store them in analysis_engine.data
        data_with_indicators = analysis_engine.compute_moving_averages(short_window=10, long_window=40)
        signal_data = analysis_engine.generate_trading_signals()

        # Backtesting
        simulator = PortfolioSimulator(INITIAL_CAPITAL)
        # The portfolio simulation uses the original dataset for returns calculation,
        # but the trading strategy logic relies on signal_data which was derived
        # from the data with indicators. This part is okay as is.
        portfolio_results = simulator.simulate_strategy(dataset, signal_data)

        # Performance analysis
        performance = calculate_performance_metrics(portfolio_results)
        print("\nPerformance Metrics:")
        for metric, value in performance.items():
            print(f"{metric}: {value:.4f}")

        # Visualization
        # Pass the DataFrame containing the indicators (Fast_MA and Slow_MA)
        TradingVisualizer.plot_price_signals(data_with_indicators, signal_data, symbol)
        TradingVisualizer.plot_performance_comparison(portfolio_results)

    plt.show()
```

## Sample Output

<pre>
Processing BTC-USD:
==================================================

Performance Metrics:
Total Return: 3.2878
Annual Volatility: 0.4030
Sharpe Ratio: 2.6966
Max Drawdown: -0.2296
MSE vs Buy&Hold: 1882237.5880

Processing ETH-USD:
==================================================

Performance Metrics:
Total Return: 5.4548
Annual Volatility: 0.5688
Sharpe Ratio: 2.5508
Max Drawdown: -0.3017
MSE vs Buy&Hold: 23582755.0118
</pre>

## Visualizations
1. Price Action with Trading Signals:
- Closing price with fast/slow moving averages
- Green triangles for buy signals
- Red triangles for sell signals

2. Portfolio Performance Comparison:
- Strategy performance vs buy-and-hold approach
- Annotated final portfolio values
- Equity curve visualization

## Risk Disclosure
Cryptocurrency trading involves substantial risk of loss and is not suitable for every investor. Past performance is not indicative of future results. This system is for educational purposes only and should not be considered financial advice.

Note: This is a simulation framework only - not financial advice. Always test strategies with historical data before live trading.

## License
This project is licensed under the Apache License 2.0. See the LICENSE file for details.



---
## Major System Upgrades & Improvements (June 20th, 2025)
This new repository (https://github.com/johnnietse/cryptocurrency-trading-system-with-coingecko-api.git) now features a significantly enhanced cryptocurrency trading system with these key upgrades from the original Yahoo Finance-based version:

1. Premium Data Source Migration
- Replaced Yahoo Finance with CoinGecko API for more reliable, institutional-grade cryptocurrency data
- Added support for 28+ cryptocurrencies with proper coin ID mapping

2. Intelligent API Management
- Implemented robust rate limit handling with automatic throttling (50 calls/min)
- Added exponential backoff during rate limit errors (5s → 10s → 20s)
- Integrated API usage tracking with detailed performance reporting

3. Enhanced Data Processing
- Added missing data imputation (forward/backward filling)
- Implemented daily OHLC resampling from raw API data
- Added trading volume integration where available

4. Professional Visualization Upgrades
- Improved signal annotation styling with clear buy/sell markers
- Enhanced portfolio comparison charts with value callouts
- Added professional formatting for publication-quality outputs

5. Advanced Error Handling
- Implemented network timeout resilience
- Added comprehensive API error diagnostics
- Created empty dataset safeguards

6. Performance Optimizations
- Reduced data pipeline runtime through smart request batching
- Added concurrent processing for multi-asset analysis

7. Risk Management Features
- Implemented data validation checks throughout pipeline
- Added retry mechanisms for failed API calls (3 attempts)

Expanded Asset Support

```python
### Original (2 assets)
ASSETS = ['BTC-USD', 'ETH-USD']

### Enhanced (28+ assets)
ASSETS = [ 'BTC-USD', 'ETH-USD', 'LTC-USD', 'XRP-USD', 'ADA-USD', 'DOGE-USD', 'SOL-USD', 'BNB-USD', 'DOT-USD', 'AVAX-USD', 'MATIC-USD', 'SHIB-USD', 'TRX-USD', 'LINK-USD', 'ATOM-USD']
```

**Key System Advantage**: The new CoinGecko integration provides more consistent historical data, especially for newer altcoins, while the rate limit handling ensures reliable operation under the free API tier.

This upgraded system maintains all original features (dual MA strategy, backtesting, performance metrics) while delivering professional-grade reliability and expanded cryptocurrency coverage. The core architecture remains modular for easy extension, but now with enterprise-level robustness.


