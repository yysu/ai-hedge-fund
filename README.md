# AI Hedge Fund

This is a proof of concept for an AI-powered hedge fund.  The goal of this project is to explore the use of AI to make trading decisions.  This project is for **educational** purposes only and is not intended for real trading or investment.

This system employs several agents working together:

1. Ben Graham Agent - The godfather of value investing, only buys hidden gems with a margin of safety
2. Bill Ackman Agent - An activist investors, takes bold positions and pushes for change
3. Cathie Wood Agent - The queen of growth investing, believes in the power of innovation and disruption
4. Charlie Munger Agent - Warren Buffett's partner, only buys wonderful businesses at fair prices
5. Stanley Druckenmiller Agent - Macro trading legend who hunts for asymmetric opportunities with explosive growth potential
6. Warren Buffett Agent - The oracle of Omaha, seeks wonderful companies at a fair price
7. Valuation Agent - Calculates the intrinsic value of a stock and generates trading signals
8. Sentiment Agent - Analyzes market sentiment and generates trading signals
9. Fundamentals Agent - Analyzes fundamental data and generates trading signals
10. Technicals Agent - Analyzes technical indicators and generates trading signals
11. Risk Manager - Calculates risk metrics and sets position limits
12. Portfolio Manager - Makes final trading decisions and generates orders

<img width="1020" alt="Screenshot 2025-03-08 at 4 45 22 PM" src="https://github.com/user-attachments/assets/d8ab891e-a083-4fed-b514-ccc9322a3e57" />

**Note**: the system simulates trading decisions, it does not actually trade.

[![Twitter Follow](https://img.shields.io/twitter/follow/virattt?style=social)](https://twitter.com/virattt)

## Disclaimer

This project is for **educational and research purposes only**.

- Not intended for real trading or investment
- No warranties or guarantees provided
- Past performance does not indicate future results
- Creator assumes no liability for financial losses
- Consult a financial advisor for investment decisions

By using this software, you agree to use it solely for learning purposes.

## Table of Contents
- [AI Hedge Fund](#ai-hedge-fund)
  - [Disclaimer](#disclaimer)
  - [Table of Contents](#table-of-contents)
  - [Setup](#setup)
  - [Usage](#usage)
    - [Command Line Arguments](#command-line-arguments)
      - [Available Analysts:](#available-analysts)
      - [Available LLM Models:](#available-llm-models)
    - [Running the Hedge Fund](#running-the-hedge-fund)
    - [Running the Backtester](#running-the-backtester)
  - [Project Structure](#project-structure)
  - [Contributing](#contributing)
  - [Feature Requests](#feature-requests)
  - [License](#license)

## Setup

Clone the repository:
```bash
git clone https://github.com/virattt/ai-hedge-fund.git
cd ai-hedge-fund
```

1. Install Poetry (if not already installed):
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

2. Install dependencies:
```bash
poetry install
```

3. Set up your environment variables:
```bash
# Create .env file for your API keys
cp .env.example .env
```

4. Set your API keys:
```bash
# For running LLMs hosted by openai (gpt-4o, gpt-4o-mini, etc.)
# Get your OpenAI API key from https://platform.openai.com/
OPENAI_API_KEY=your-openai-api-key

# For running LLMs hosted by groq (deepseek, llama3, etc.)
# Get your Groq API key from https://groq.com/
GROQ_API_KEY=your-groq-api-key

# For getting financial data to power the hedge fund
# Get your Financial Datasets API key from https://financialdatasets.ai/
FINANCIAL_DATASETS_API_KEY=your-financial-datasets-api-key
```

**Important**: You must set `OPENAI_API_KEY`, `GROQ_API_KEY`, `ANTHROPIC_API_KEY`, or `DEEPSEEK_API_KEY` for the hedge fund to work.  If you want to use LLMs from all providers, you will need to set all API keys.

Financial data for AAPL, GOOGL, MSFT, NVDA, and TSLA is free and does not require an API key.

For any other ticker, you will need to set the `FINANCIAL_DATASETS_API_KEY` in the .env file.

## Usage

### Command Line Arguments

The following command line arguments are available for both the main program and backtester:

| Argument | Description | Default | Example Values |
|---------|-------------|---------|---------------|
| `--ticker` | Comma-separated list of stock ticker symbols | Required | `AAPL,MSFT,NVDA` |
| `--start-date` | Start date in YYYY-MM-DD format | 3 months before end date | `2024-01-01` |
| `--end-date` | End date in YYYY-MM-DD format | Current date | `2024-03-01` |
| `--analysts` | Comma-separated list of analysts to use | Interactive selection | `warren_buffett,charlie_munger,ben_graham` |
| `--model` | LLM model to use | Interactive selection | `gpt-4o`, `claude-3-sonnet-20240229` |
| `--show-reasoning` | Show reasoning from each agent | False | Flag (no value needed) |
| `--show-agent-graph` | Generate and show agent workflow graph | False | Flag (no value needed) |
| `--initial-cash` | Initial cash position (main.py) | 10000.0 | `50000` |
| `--margin-requirement` | Margin ratio for short positions | 0.0 | `0.5` |
| `--initial-capital` | Initial capital amount (backtester.py) | 10000 | `50000` |

#### Available Analysts:
- `ben_graham` - Benjamin Graham's value investing strategy
- `bill_ackman` - Bill Ackman's activist investing approach
- `cathie_wood` - Cathie Wood's innovation-focused growth investing
- `charlie_munger` - Charlie Munger's quality-focused approach
- `stanley_druckenmiller` - Stanley Druckenmiller's macro trading approach
- `warren_buffett` - Warren Buffett's quality-at-fair-price strategy
- `technical_analyst` - Technical analysis based on price and volume patterns
- `fundamentals_analyst` - Fundamental analysis based on financial metrics
- `sentiment_analyst` - Market sentiment analysis
- `valuation_analyst` - Quantitative valuation methods

#### Available LLM Models:
Depending on your API keys, you can use models from:
- OpenAI: `gpt-4o`, `gpt-4o-mini`, etc.
- Anthropic: `claude-3-opus-20240229`, `claude-3-sonnet-20240229`, etc.
- Groq: `llama3-70b-8192`, `mixtral-8x7b-32768`, etc.
- DeepSeek: `deepseek-coder`, etc.

### Running the Hedge Fund
```bash
poetry run python src/main.py --ticker AAPL,MSFT,NVDA
```

**Example Output:**
<img width="992" alt="Screenshot 2025-01-06 at 5 50 17 PM" src="https://github.com/user-attachments/assets/e8ca04bf-9989-4a7d-a8b4-34e04666663b" />

Example commands:

```bash
# Show detailed reasoning from each agent
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --show-reasoning

# Specify time period
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --start-date 2024-01-01 --end-date 2024-03-01

# Specify which analysts to use (instead of interactive selection)
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --analysts warren_buffett,charlie_munger,ben_graham

# Specify which LLM model to use (instead of interactive selection)
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --model gpt-4o

# Combine multiple options
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --analysts warren_buffett,charlie_munger --model gpt-4o --start-date 2024-01-01 --end-date 2024-03-01
```

### Running the Backtester

```bash
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA
```

**Example Output:**
<img width="941" alt="Screenshot 2025-01-06 at 5 47 52 PM" src="https://github.com/user-attachments/assets/00e794ea-8628-44e6-9a84-8f8a31ad3b47" />

Example backtester commands:

```bash
# Specify time period
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --start-date 2024-01-01 --end-date 2024-03-01

# Specify which analysts to use (instead of interactive selection)
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --analysts warren_buffett,charlie_munger

# Specify which LLM model to use (instead of interactive selection)
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --model gpt-4o

# Adjust initial capital and margin requirements
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --initial-capital 50000 --margin-requirement 0.5

# Combine multiple options
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --analysts warren_buffett,charlie_munger --model gpt-4o --start-date 2024-01-01 --end-date 2024-03-01 --initial-capital 100000
```

## Project Structure
```
ai-hedge-fund/
├── src/
│   ├── agents/                   # Agent definitions and workflow
│   │   ├── bill_ackman.py        # Bill Ackman agent
│   │   ├── fundamentals.py       # Fundamental analysis agent
│   │   ├── portfolio_manager.py  # Portfolio management agent
│   │   ├── risk_manager.py       # Risk management agent
│   │   ├── sentiment.py          # Sentiment analysis agent
│   │   ├── technicals.py         # Technical analysis agent
│   │   ├── valuation.py          # Valuation analysis agent
│   │   ├── warren_buffett.py     # Warren Buffett agent
│   ├── tools/                    # Agent tools
│   │   ├── api.py                # API tools
│   ├── backtester.py             # Backtesting tools
│   ├── main.py # Main entry point
├── pyproject.toml
├── ...
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

**Important**: Please keep your pull requests small and focused.  This will make it easier to review and merge.

## Feature Requests

If you have a feature request, please open an [issue](https://github.com/virattt/ai-hedge-fund/issues) and make sure it is tagged with `enhancement`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.