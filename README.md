# AI Hedge Fund

This is a proof of concept for an AI-powered hedge fund.  The goal of this project is to explore the use of AI to make trading decisions.  This project is for **educational** purposes only and is not intended for real trading or investment.

This system employs several agents working together:

1. Ben Graham Agent - The godfather of value investing, only buys hidden gems with a margin of safety
2. Bill Ackman Agent - An activist investors, takes bold positions and pushes for change
3. Cathie Wood Agent - The queen of growth investing, believes in the power of innovation and disruption
4. Charlie Munger Agent - Warren Buffett's partner, only buys wonderful businesses at fair prices
5. Peter Lynch Agent - Legendary growth investor who seeks "ten-baggers" and invests in what he knows
6. Phil Fisher Agent - Legendary growth investor who mastered scuttlebutt analysis
7. Stanley Druckenmiller Agent - Macro legend who hunts for asymmetric opportunities with growth potential
8. Warren Buffett Agent - The oracle of Omaha, seeks wonderful companies at a fair price
9. Valuation Agent - Calculates the intrinsic value of a stock and generates trading signals
10. Sentiment Agent - Analyzes market sentiment and generates trading signals
11. Fundamentals Agent - Analyzes fundamental data and generates trading signals
12. Technicals Agent - Analyzes technical indicators and generates trading signals
13. Risk Manager - Calculates risk metrics and sets position limits
14. Portfolio Manager - Makes final trading decisions and generates orders

<img width="1042" alt="Screenshot 2025-03-22 at 6 19 07 PM" src="https://github.com/user-attachments/assets/cbae3dcf-b571-490d-b0ad-3f0f035ac0d4" />


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
  - [Portfolio](#portfolio)
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
- OpenAI: `gpt-4o`, `gpt-4.5-preview`, `o1`, `o3-mini`, etc.
- Anthropic: `claude-3-7-sonnet-latest`, `claude-3-5-sonnet-latest`, `claude-3-5-haiku-latest`, etc.
- DeepSeek: `deepseek-reasoner`, `deepseek-chat`, etc.

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


## Portfolio

⸻

📌 價值投資派（保守型、穩健增值）
	•	Benjamin Graham (ben_graham)：價值投資、低估資產、強調安全邊際。
	•	Charlie Munger (charlie_munger)：著重企業品質與競爭優勢。
	•	Warren Buffett (warren_buffett)：品質企業合理價，長期持有。
	•	Valuation Analyst (valuation_analyst)：量化估值、協助評估公司價值。

理由：
	•	Graham、Buffett、Munger 策略高度互補，都重視基本面、長期價值與安全邊際。
	•	Valuation Analyst 提供數據支持，幫助精確衡量企業價值。

⸻

📈 積極增長型（高成長潛力、承擔較高風險）
	•	Cathie Wood (cathie_wood)：投資創新科技、成長股。
	•	Sentiment Analyst (sentiment_analyst)：透過市場情緒掌握趨勢。
	•	Fundamentals Analyst (fundamentals_analyst)：基本面篩選高成長潛力股。

理由：
	•	Cathie Wood 的創新成長策略風險較高，但有高回報潛力。
	•	Sentiment Analyst 協助掌握市場情緒、增強時機掌控。
	•	Fundamental Analyst 則確保基本面穩健，避免投資於純粹炒作標的。

⸻

📊 激進主動型（積極管理、願承受波動、強調主動參與）
	•	Bill Ackman (bill_ackman)：積極介入公司經營改善價值（主動派）。
	•	Stanley Druckenmiller (stanley_druckenmiller)：宏觀交易、短期與中期趨勢布局。
	•	Sentiment Analyst (sentiment_analyst)：市場情緒協助進出點掌握。

理由：
	•	Ackman 的主動介入與 Druckenmiller 的宏觀趨勢交易可互補，一者是微觀公司內部價值挖掘，另一者掌握大環境趨勢。
	•	Sentiment Analyst 提供即時市場情緒訊號，輔助投資時機判斷。

⸻

📉 短線交易與技術導向型（短期操作、技術指標為主）
	•	Technical Analyst (technical_analyst)：專注價格與成交量訊號，適合短線或波段交易。
	•	Sentiment Analyst (sentiment_analyst)：輔助技術訊號，以情緒佐證市場走勢。

理由：
	•	技術分析與市場情緒高度互補，技術面掌握進出點，情緒分析增加勝率。
	•	適合風格傾向短期獲利、重視市場動能的投資人。

⸻

👥 不同投資人心態適合的策略組合：

心態與需求	策略組合推薦	原因解釋
🛡️ 保守穩健型	Graham + Munger + Buffett + Valuation Analyst	長期價值為主，注重安全邊際與穩定收益。
🚀 積極成長型	Cathie Wood + Fundamentals + Sentiment Analyst	注重高成長、創新、善用市場情緒來掌握風險與時機。
⚔️ 激進主動型	Ackman + Druckenmiller + Sentiment Analyst	主動介入、短中期趨勢布局，積極獲取超額報酬。
📈 技術短線型	Technical Analyst + Sentiment Analyst	以價格趨勢、情緒波動迅速掌握短期獲利時機。
⚖️ 均衡混合型	Buffett + Valuation Analyst + Technical Analyst	長期價值持股，搭配技術分析掌握進出場時機，穩健中尋求增長。


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