# EMA Crossover Trading Strategy

This GitHub README article provides an overview of a simple long-only trading strategy coded in Pine Script using TradingView's //@version=4. The strategy is based on the Exponential Moving Average (EMA) crossover, a popular technical analysis tool. It generates buy signals when a shorter-term EMA crosses above a longer-term EMA, and it incorporates a trailing stop to manage risk.

## Strategy Overview

The "S EMA Cross L EMA Strategy (Long Only)" is designed for a bullish market. It uses two EMAs:

- **Short EMA (Blue)**: A faster EMA with a period of 9.
- **Long EMA (Red)**: A slower EMA with a period of 13.

When the short EMA crosses above the long EMA, a buy signal is generated, and a position is opened. Additionally, a trailing stop is applied to manage the position, with a specified stop loss value of 10 ticks (0.10). This strategy aims to capture upward price movements while mitigating potential losses.

## Pine Script Code

```pinescript
//@version=4
strategy("S EMA Cross L EMA Strategy (Long Only)", shorttitle="EMA Crossover", overlay=true)

// Define the EMA lengths
ema_small_length = 9
ema_larg_length = 13

// Calculate the EMAs
ema_small = ema(close, ema_small_length)
ema_larg = ema(close, ema_larg_length)

// Plot the EMAs on the chart
plot(ema_small, color=color.blue, title="Small EMA")
plot(ema_larg, color=color.red, title="Larg EMA")

// Define the conditions for buying (long) and selling
buy_condition = crossover(ema_small, ema_larg)

// Plot buy signals on the chart
plotshape(series=buy_condition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)

// Define the trailing stop and stop loss values
sl_value = 10
trail_value = sl_value  // 0.10 or 10 ticks
stop_loss_value = sl_value  // 0.10 or 10 ticks

// Strategy orders for long positions only
strategy.entry("Buy", strategy.long, when=buy_condition)

// Add trailing stop for long positions
strategy.exit("Trailing Stop", from_entry="Buy", trail_offset=trail_value, trail_price=trail_value, stop=stop_loss_value)
```

## How to Use

1. Copy the provided Pine Script code.
2. Open the TradingView Pine Script editor.
3. Create a new script and paste the code into the editor.
4. Save the script with a relevant name.
5. Apply the script to a chart with the desired trading instrument and timeframe.
6. The strategy will automatically plot the EMAs and buy signals on the chart.
7. Monitor the strategy and execute trades as per the generated buy signals.

Please note that this strategy is for educational purposes only and should be thoroughly tested before using it in a live trading environment. Always remember to use proper risk management and consider backtesting to assess its performance with historical data.

Happy trading! 🚀
