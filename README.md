<img src="images/avatar.png" width="277" alt="Robinhood AI Trading Bot"/>


# Robinhood AI Trading Bot
## ⚡ TL;DR
Once you've added your OpenAI API Key and Robinhood credentials, and run this bot in "Auto" mode, it will analyze your portfolio stocks and some of your watchlist stocks (if available). 
It calculates moving averages for these stocks, checks Robinhood analyst ratings (covering what "bulls" and "bears" say), feeds this data to OpenAI, and asks the AI to decide on actions for each stock (sell, buy, or hold, including amount). 
It then directly executes all AI-made decisions.

So be smart — don’t run this bot in "Auto" mode right after your first test. 
This involves real money, and there’s no cancel button! 
Begin with "Demo" mode, which performs everything as in "Auto" mode except the actual sell and buy actions, which are just printed as if executed.

Then, try "Manual" mode, where the bot asks for confirmation before each sell or buy action.

P.S. I still run it in "Auto" mode, and, to be honest, I’m happy with the results so far.


## 🌟 Fun Part
Welcome to the Robinhood Trading Bot! This Python script pairs OpenAI's intelligence with Robinhood's trading power to help you automate and optimize your stock moves.


### Motivation
This is a scientific experiment to see how AI can trade stocks better than humans (or at least me). 


### Features
- **AI-Powered Trading**: Leverages OpenAI to provide smart, data-driven trading decisions.
- **Portfolio & Watchlist Integration**: Analyze and trade stocks from both your Robinhood portfolio and watchlist.
- **Customizable Parameters**: Set trading limits and conditions to fit your strategy.
- **Trading Exceptions**: Exclude specific stocks from trading.
- **Demo Mode**: Safely test trades without real execution.
- **Manual Mode**: Approve each trade individually.
- **Auto Mode**: Automate trades based on AI guidance.
- **Workday Schedule**: Align bot activity with market hours.
- **Logging**: Track bot activity and trade history in the console.


### How It Works
1. **Login to OpenAI**: Authenticates using your OpenAI API key.
2. **Login to Robinhood**: Logs into your Robinhood account with your credentials.
3. **Fetch Portfolio Stocks**: Retrieves stocks from your portfolio.
4. **Fetch Watchlist Stocks**: Retrieves a limited number of stocks from your watchlist, selecting randomly if needed to meet the limit.
5. **Analyze Stock Prices and Ratings**: Calculates RSI, moving averages and includes Robinhood analyst ratings.
6. **AI-Powered Decisions**: Sends stock data to OpenAI, receiving trading decisions (sell, buy, or hold) for each stock.
7. **Execute Trades**: Executes initial trading decisions.
8. **Execute Adjusted Trades**: Executes refined trading decisions.
9. **Repeat**: Continues to analyze, trade, and adjust as market conditions evolve.


#### Analyze Stock Prices and Ratings System
The bot's analytical system incorporates moving averages and Robinhood analyst ratings to inform trading decisions:
1. **Relative Strength Index (RSI)**: The bot calculates the RSI for each stock to determine overbought or oversold conditions.
2. **Moving Averages**: The bot calculates moving averages (50-day and 200-day) for each stock to evaluate price trends and identify optimal buy and sell points.
2. **Robinhood Analyst Ratings**: The bot fetches bullish and bearish ratings from Robinhood for each stock, providing additional insights into market sentiment and potential price movements.

This is Robinhood's analyst rating system example:

![Robinhood Analyst Ratings](images/robinhood_analyst_ratings.png)


#### AI-Powered Decision-Making System
The bot leverages OpenAI to make data-driven trading decisions based on the stock data:
1. **Input Data**: The bot feeds the stock data (rsi, moving averages, analyst ratings) to OpenAI.
2. **Output Data**: OpenAI provides trading decisions (sell, buy, or hold) for each stock.

Decision-making AI-prompt example:  
``````
**Context:**
Today is 2025-01-31T14:31:12Z.
You are a short-term investment advisor managing a stock portfolio.
Every 3600 seconds, you analyze market conditions to make investment decisions.
You need to decide whether to buy, sell, or hold each of these stocks based on the given data.

**Constraints:**
- Your current budget (initial buying power): 0.0 USD.
- Maximum portfolio size (maintain a portfolio size of fewer this number): 20 stocks.
- Trade Exceptions (exclude from trading in any decisions): VOO, SPY, IVV

**Stock Portfolio Overview:**
```json
{
 "AAPL": {
  "current_price": 235.19,
  "my_quantity": 0.00066,
  "my_average_buy_price": 242.42,
  "rsi": 32.99,
  "50_day_mavg_price": 240.01,
  "200_day_mavg_price": 219.38,
  "analyst_summary": {
   "num_buy_ratings": 31,
   "num_hold_ratings": 16,
   "num_sell_ratings": 5
  },
  "analyst_ratings": [
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "sell",
    "text": "Regulators have a keen eye on Apple, and recent regulations have chipped away at parts of Apple\u2019s sticky ecosystem. "
   },
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "sell",
    "text": "Apple\u2019s supply chain is highly concentrated in China and Taiwan, which opens up the firm to geopolitical risk. Attempts to diversify into other regions may pressure profitability or efficiency."
   },
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "sell",
    "text": "Apple is prone to consumer spending and preferences, which creates cyclicality and opens the firm up to disruption."
   },
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "buy",
    "text": "Apple has a stellar balance sheet and sends great amounts of cash flow back to shareholders."
   },
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "buy",
    "text": "We like Apple\u2019s move to in-house chip development, which we think has accelerated its product development and increased its differentiation. "
   },
   {
    "published_at": "2025-01-30T19:07:26Z",
    "type": "buy",
    "text": "Apple offers an expansive ecosystem of tightly integrated hardware, software, and services, which locks in customers and generates strong profitability."
   }
  ]
 },
 "MSFT": {
  "current_price": 416.59,
  "my_quantity": 0.0,
  "my_average_buy_price": 0.0,
  "rsi": 35.86,
  "50_day_mavg_price": 431.35,
  "200_day_mavg_price": 425.72,
  "analyst_summary": {
   "num_buy_ratings": 57,
   "num_hold_ratings": 3,
   "num_sell_ratings": 0
  },
  "analyst_ratings": [
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "sell",
    "text": "Microsoft is not the top player in its key sources of growth, notably Azure and Dynamics."
   },
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "sell",
    "text": "Microsoft lacks a meaningful mobile presence."
   },
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "sell",
    "text": "Momentum is slowing in the ongoing shift to subscriptions, particularly in Office, which is generally considered a mature product."
   },
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "buy",
    "text": "Microsoft has monopoly like positions in various areas (OS, Office) that serve as cash cows to help drive Azure growth."
   },
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "buy",
    "text": "Microsoft 365 continues to benefit from upselling into higher-priced stock-keeping units as customers are willing to pay up for better security and Teams Phone, which should continue over the next several years."
   },
   {
    "published_at": "2025-01-31T11:05:36Z",
    "type": "buy",
    "text": "Public cloud is widely considered to be the future of enterprise computing, and Azure is a leading service that benefits the evolution to first to hybrid environments, and then ultimately to public cloud environments."
   }
  ]
 },
 ...
}
```

**Response Format:**
Return your decisions in a JSON array with this structure:
```json
[
  {"symbol": "<symbol>", "decision": "<decision>", "quantity": <quantity>},
  ...
]
```
- `symbol`: Stock symbol.
- `decision`: One of `buy`, `sell`, or `hold`.
- `quantity`: Recommended transaction quantity.

**Instructions:**
- Provide only the JSON output with no additional text.
- Return an empty array if no actions are necessary.
``````

AI-response example:
```
[
    {"symbol": "AAPL", "decision": "sell", "quantity": 0.564172},
    {"symbol": "BL", "decision": "hold", "quantity": 0.0},
    {"symbol": "EQIX", "decision": "buy", "quantity": 1.0},
    ...
]
```


#### Logging System
The bot logs its activity and trading decisions in a console log.
Log example:
```
Are you sure you want to run the bot in auto mode? (yes/no): yes
[2024-11-01 11:06:58] [INFO]    Market is open, running trading bot in auto mode...
[2024-11-01 11:06:58] [INFO]    Getting portfolio stocks...
[2024-11-01 11:07:02] [INFO]    Portfolio stocks to proceed: NVDA (1.07%), MSFT (0.12%), SNAP (0.25%), NWSA (13.71%), ...
[2024-11-01 11:07:02] [INFO]    Prepare portfolio stocks for AI analysis...
[2024-11-01 11:07:07] [INFO]    Getting watchlist stocks...
[2024-11-01 11:07:08] [INFO]    Watchlist stocks to proceed: VRT, BB, VRNT, PBI, BMBL, IESC, WB, LITE, ...
[2024-11-01 11:07:08] [INFO]    Prepare watchlist overview for AI analysis...
[2024-11-01 11:07:09] [INFO]    Making AI-based decision...
[2024-11-01 11:07:21] [INFO]    Executing decisions...
[2024-11-01 11:07:21] [INFO]    NVDA > Decision: sell of 2.012
[2024-11-01 11:07:21] [ERROR]   NVDA > Sold 2.012 stocks
[2024-11-01 11:07:21] [INFO]    MSFT > Decision: sell of 1.5422
[2024-11-01 11:07:21] [ERROR]   MSFT > Error selling: Not enough shares to sell.
[2024-11-01 11:07:22] [INFO]    VRT > Decision: buy of 2.09
[2024-11-01 11:07:23] [INFO]    VRT > Bought 2.09 stocks
[2024-11-01 11:07:23] [INFO]    SNAP > Decision: hold of 0.0323
[2024-11-01 11:07:23] [INFO]    VIAV > Decision: hold of 0.0212
[2024-11-01 11:07:24] [INFO]    Stocks sold: NVDA (2.0)
[2024-11-01 11:07:24] [INFO]    Stocks bought: VRT (2.09)
[2024-11-01 11:07:24] [INFO]    Errors: MSFT (Not enough shares to sell.)
[2024-11-01 11:07:24] [INFO]    Waiting for 600 seconds...
```


## 🥱 Boring Part
### Install
1. Clone the repository:
    ```sh
    git clone https://github.com/siropkin/robinhood-ai-trading-bot.git
    cd robinhood-ai-trading-bot
    ```

2. Install dependencies:
    ```sh
    pip install robin_stocks openai onepassword pandas
    ```


### Config
Clone `config.py.example` to `config.py` and fill in the required parameters:
   ```sh
   cp config.py.example config.py
   ```

Configuration parameters:
```python
# 1Password Credentials
OP_SERVICE_ACCOUNT_NAME = "..."             # 1Password service account name (for Robinhood MFA secret)
OP_SERVICE_ACCOUNT_TOKEN = "..."            # 1Password service account token (for Robinhood MFA secret)
OP_VAULT_NAME = "..."                       # 1Password vault name (for Robinhood MFA secret)
OP_ITEM_NAME = "..."                        # 1Password item name (for Robinhood MFA secret)

# Credentials
OPENAI_API_KEY = "..."                      # OpenAI API key
ROBINHOOD_USERNAME = "..."                  # Robinhood username
ROBINHOOD_PASSWORD = "..."                  # Robinhood password
ROBINHOOD_MFA_SECRET = ""                   # Robinhood MFA secret (if enabled)

# Basic config parameters
MODE = "demo"                               # Trading mode (demo, auto, manual)
LOG_LEVEL = "INFO"                          # Log level (DEBUG, INFO)
RUN_INTERVAL_SECONDS = 600                  # Trading interval in seconds (if the market is open)

# Robinhood config parameters
TRADE_EXCEPTIONS = []                       # List of stocks to exclude from trading (e.g. ["AAPL", "TSLA", "AMZN"])
WATCHLIST_NAMES = []                        # Watchlist names (can be empty, or "My First List", "My Second List", etc.)
WATCHLIST_OVERVIEW_LIMIT = 10               # Number of stocks to process in decision-making (e.g. 20)
PORTFOLIO_LIMIT = 10                        # Number of stocks to hold in the portfolio
MIN_SELLING_AMOUNT_USD = 1.0                # Minimum sell amount in USD (False - disable setting)
MAX_SELLING_AMOUNT_USD = 10.0               # Maximum sell amount in USD (False - disable setting)
MIN_BUYING_AMOUNT_USD = 1.0                 # Minimum buy amount in USD (False - disable setting)
MAX_BUYING_AMOUNT_USD = 10.0                # Maximum buy amount in USD (False - disable setting)

# OpenAI config params
OPENAI_MODEL_NAME = "gpt-4o-mini"           # OpenAI model name
```


#### Robinhood MFA Secret
If you have Multi-Factor Authentication (MFA) enabled on your Robinhood account, you will need to provide the MFA code.
This can be done in one of two ways:
1. Directly setting the `ROBINHOOD_MFA_SECRET` environment variable.
2. Or using 1Password credentials to retrieve the code.

##### Using ROBINHOOD_MFA_SECRET (Generate MFA Code Locally)
If you prefer to set the MFA secret directly, follow these steps:
1. Log in to your Robinhood account on your phone. Important to use your phone because it will display the secret key but not the QR code.
2. Navigate to the security settings.
3. Enable MFA if it is not already enabled. When setting up MFA, you will be asked to select an authentication method on your phone. Choose "Authenticator app" and Robinhood will provide you with a secret key. This is your `ROBINHOOD_MFA_SECRET`.
4. Copy this secret key and set it as the `ROBINHOOD_MFA_SECRET` environment variable or paste it directly into the `config.py` file.
5. Enter the same secret key into your authentication app on the same PC where you run the script (e.g., Google Authenticator). Note: If you enter the secret on a different device, it will generate a different value.
6. After entering the same secret on the same PC, use the generated TOTP number to authenticate with the Robinhood app.

##### Using 1Password (Retrieve MFA Code)
If you do not set the `ROBINHOOD_MFA_SECRET` environment variable, the script will attempt to retrieve the MFA secret from 1Password using the following credentials:
```python
# 1Password Credentials
OP_SERVICE_ACCOUNT_NAME = "..."             # 1Password service account name (for Robinhood MFA secret)
OP_SERVICE_ACCOUNT_TOKEN = "..."            # 1Password service account token (for Robinhood MFA secret)
OP_VAULT_NAME = "..."                       # 1Password vault name (for Robinhood MFA secret)
OP_ITEM_NAME = "..."                        # 1Password item name (for Robinhood MFA secret)
```

To use this feature:
1. Ensure the above 1Password credentials are correctly configured in your environment or `config.py` file.
2. Store your Robinhood MFA secret in the specified 1Password vault and item.
3. The script will automatically fetch the MFA secret from 1Password if `ROBINHOOD_MFA_SECRET` is not provided.

For more information on setting up 1Password Service Accounts, read the guide: [Get started with 1Password Service Accounts](https://developer.1password.com/docs/service-accounts/get-started/)


### Run
To start the bot, run the following command in your terminal:
   ```sh
   python main.py
   ```


## ⚠️ Disclaimer
This bot is for educational purposes only. Trading stocks involves risk, and you should only trade with money you can afford to lose. The author is not responsible for any financial losses you may incur.


## 📄 License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.


## 🤝 Contributing
I'm genuinely excited to welcome contributors! 
Whether you're interested in refining the logging system, enhancing AI-prompt strategies, or enriching stock data — there’s room for your ideas and expertise. 
Feel free to submit pull requests or open issues with suggestions and improvements!


## 📧 Contact
If you have any questions or feedback, feel free to reach out at [goodbotty@proton.me](mailto:goodbotty@proton.me).
