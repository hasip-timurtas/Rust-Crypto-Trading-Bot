# Crypto Trading Bot

A cryptocurrency trading bot built using Machine Learning and Rust. This project is inspired by [CyberPunkMetalHead's cryptocurrency machine learning prediction algorithm](https://github.com/CyberPunkMetalHead/cryptocurrency-machine-learning-prediction-algo-trading).


## Trading Bot Strategy

### Overview

This trading bot uses a machine learning-based strategy to predict market movements and place buy orders based on those predictions. It fetches hourly kline (candle) data from Binance and uses a pre-trained machine learning model to predict future price movements.

### Strategy

1. **Data Retrieval:**
   - Fetch the last X days of hourly kline (candle) data from Binance.

2. **Model Training:**
   - Train a machine learning model using the historical data. The bot utilizes [LightGBM](https://lightgbm.readthedocs.io/en/v3.3.2/), a fast, tree-based gradient boosting framework. While LightGBM may not be as accurate as other models like LSTM (Recurrent Neural Networks), it provides reliable indicators of basic price movements (up or down), which is sufficient for this strategy.

3. **Price Prediction:**
   - The trained model predicts the `high` price for the current candle.
   - If the predicted `high` price is lower than the current `open` or `close` price, the bot skips this candle and waits for the next one.
   - If the prediction is higher, a buy order is placed.

4. **Waiting for Price Target:**
   - Once a buy order is placed, the bot waits for the price to reach the predicted `high` value.
   - If the predicted price is not reached by the end of the candle, the bot continues to wait until the target is hit.

## Tools and Technologies

- **Data Source:** Binance API
- **Machine Learning Model:** [LightGBM](https://lightgbm.readthedocs.io/en/v3.3.2/)
  
This strategy offers a straightforward approach to predict short-term market movements and place trades accordingly.

## 💻 Installation & usage

Install [Rust](https://www.rust-lang.org/tools/install) and clone this repository:

```bash
$ git clone https://github.com/hasip-timurtas/Rust-Crypto-Trading-Bot.git
$ cd Rust-Crypto-Trading-Bot.git
```

Then, copy the config file and edit it accordingly (should be self-explanatory):

```bash
$ cp config.example.yaml config.yaml
$ vim config.yaml # or use any other text editor of choice to edit the config file
```

To run the bot in development mode, execute:

```bash
$ RUST_LOG=debug cargo run
```

To run the bot in production mode, execute:

```bash
$ RUST_LOG=info cargo run
```

You can also build a release binary with `cargo build -r` and copy it + your config file to a VPS or raspberry pi.

## 📷 Screenshots
<img width="1227" alt="image" src="https://user-images.githubusercontent.com/30344294/228659990-db8cf341-d8f1-4686-9ea9-3dd04cdb5fa4.png">

