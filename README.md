# ETF Comparative Analysis

**Team members:** Deema Hazim & Haresh Subaskaran

The **Colab notebook** can be accessed [here](https://colab.research.google.com/drive/1DrV7vO8mA72VKXd0IC9ByuhX21YvhtMd?usp=sharing)

## Introduction
Exchange-Traded Funds (ETFs) have become one of the most popular investment vehicles in modern financial markets due to their low cost, liquidity, and diversified exposure. They allow investors to easily access entire indices, sectors, or asset classes without purchasing individual securities. However, not all ETFs perform equally. Even among major index-tracking funds, differences in composition, volatility, and fees can significantly influence investor returns.

This project investigates how popular ETFs we selected compare in returns, volatility, and fees, and how they behave under different market conditions. The analysis covers roughly ten years of historical price data obtained through the Yahoo Finance API via the yfinance Python library.

The results reveal how different ETF compositions and market exposures translate into risk-return trade-offs, offering insight into portfolio diversification and investor decision-making.

---

## Data Overview

### Data Sources:
The price data was retrieved using the yfinance Python library, which sources from Yahoo Finance. Additionally, the official Vanguard and Invesco websites were used for our categorical data which shows each ETFs top holdings, sector distribution, and the regional distribution for one of the ETFs which covers international (non U.S.-based) companies. 

### Selected ETFs:
Below are our selected ETFs and their expense ratios. An ETF expense ratio is the annual fee to cover management and operating costs, expressed as a percentage of the fund's assets. These fees are deducted automatically from the fund's value, reducing your net returns.

- **VOO (Vanguard S&P 500 ETF):** Tracks the S&P 500 (500 large-cap U.S. companies). Expense ratio 0.03%.

- **VTI (Vanguard Total Stock Market ETF):** Tracks the CRSP U.S. Total Market Index (roughly 3,500 U.S. companies including small and mid caps). Expense ratio 0.03%.

- **QQQ (Invesco NASDAQ-100 ETF):** Tracks the NASDAQ-100 index (technology and growth-heavy large-cap stocks). Expense ratio 0.20%.

- **VEU (Vanguard FTSE All-World ex-U.S. ETF):** Tracks international developed and emerging markets excluding the U.S. Expense ratio 0.07%.

### Dataset Shape and Features:
The main dataset from yfinance contains around 2,500 daily observations (rows) over ten years. The original dataset just included the closing price and fees, and then we calculated and added the daily return, annualized return, annualized volatility, rolling volatility, cumulative return, Sharpe ratio, drawdown, max drawdown, and trading volume.

Categorical features include ticker, region, holdings, sectors, and market condition (bull, bear, crash).

---

## Categorical Data Overview

### Top 10 Holdings:
<img src="https://github.com/user-attachments/assets/c1341c2f-8617-4a3b-a74d-08de0036187d" width="70%" />

The above pie charts display the top 10 holdings of each ETF, and what percentage of the top 10 does each company hold. We notice that VTI  and QQQ are heavily concentrated in U.S. mega-cap technology stocks. NVIDIA, Microsoft, and Apple are the top 3 holdings in both funds, making up a significant portion of their value.

VOO is also focused on large U.S. companies, but its top holdings are slightly more varied, with JPMorgan Chase & Co. (15.9%) and Eli Lilly & Co. (11.6%) in the top spots.

VEU is the clear outlier. It holds no U.S. companies in its top 10 (or dataset at all). Instead, it's dominated by international stocks, with Taiwan Semiconductor Manufacturing Co. Ltd. (27.3%) and Tencent Holdings Ltd. (13.6%) as its two largest positions.

---

### Sector Allocation:
<div style="display: flex; justify-content: center; gap: 10px;">
  <img src="https://github.com/user-attachments/assets/78ae2b3f-cdbf-4a17-96c1-ce32c05268db" width="35%" />
  <img src="https://github.com/user-attachments/assets/6514165d-3bc3-49d4-89a2-7ed7ae2435b3" width="35%" />
  <img src="https://github.com/user-attachments/assets/f4415a18-378c-4ff0-8146-523228623198" width="35%" />
</div>

Both VTI and VOO represent the broad US market (VOO tracks the 500 largest companies, VTI tracks the entire market). Their sector allocations are very similar, with a heavy tilt toward technology (35-38%).

QQQ, which tracks the NASDAQ-100, is not a diversified fund in the same way. It is a highly concentrated bet on the technology sector. Together, its top two sectors (Technology and Consumer Discretionary) account for over 82% of the fund.

---

### VEU Region Distribution:
<img src="https://github.com/user-attachments/assets/4dfca9f4-bc5d-49ff-9eed-3dd4df2f63f9" width="50%" />

Since VEU does not include any U.S. companies, we decided to look at the regions their holdings come from. We notice this distribution supports the top 10 holdings we saw earlier. We see that the Pacific makes up 25.5% of the fund, driven by the fund's #1 holding, Taiwan Semiconductor Manufacturing from Taiwan, and another major holding, Samsung from South Korea.

Europe makes up 38.1% of the fund, being the most heavily represented in the top 10 list. It includes the Swiss giants Nestle, Roche Holding AG, and Novartis AG, as well as ASML Holding NV (Netherlands), HSBC Holdings plc (United Kingdom), and SAP SE (Germany).

Emerging Markets make up 27.5% of the fund, represented at the top of the holdings list by the two Chinese tech giants, Tencent Holdings Ltd. and Alibaba Group Holding Ltd.

---

## Risk vs. Return:
<img src="https://github.com/user-attachments/assets/61e4a24a-850e-48b9-a6ce-3cbc7e054a8c" width="50%"/>

QQQ has the highest annualized return and risk. This is a direct consequence of its 64% concentration in the high-growth (and high-volatility) technology sector.

VOO shows slightly better risk-adjusted returns than VTI in this period. VOO's focus on the 500 largest, most established companies was slightly more efficient than VTI, which also holds thousands of smaller, mid-cap, and small-cap stocks that may have slightly dragged on performance.

VEU’s low return is a well-known result of the U.S. market dramatically outperforming international markets over the last decade. Its lower volatility is a key feature of its diversification. It's spread across many countries and sectors (Healthcare, Financials, Consumer Goods, etc.) rather than being dominated by US tech.

It is important to note that this is just a 10-year window, which may not be representative of the time horizon and global circumstances in the future.

---

## Rolling Volatility (Dynamic Risk):
<img src="https://github.com/user-attachments/assets/5c4d0986-4fe3-462e-9713-86dd9e615b53" width="50%" />

The 1-Month Rolling Annualized Volatility graph illustrates how short-term market risk fluctuates over time. Rolling volatility is better at capturing short-term risk while annualized volatility is better at capturing long-term risk. What we did was capture short-term volatility, but scaling it to what it would be if that same level of volatility continued for a year.

All four ETFs exhibited synchronized volatility movements. When the market is calm, all funds are calm. When a crisis hits, all funds become volatile. This shows they are all sensitive to major macroeconomic events.

The enormous spike in early 2020 is the COVID-19 market crash. It's the most significant volatility event of the last 10 years by a huge margin, with short-term volatility briefly exceeding 90% for some funds.

The green (VOO) and red (VTI) lines are almost indistinguishable. This confirms that the S&P 500 and the Total U.S. Market have a virtually identical risk profile on a day-to-day basis. They are consistently the least volatile of the group, while QQQ consistently exhibits the highest volatility due to its tech concentration.

---

## Dollar Loss Due to Expense Ratios:
<img src="https://github.com/user-attachments/assets/e55f4fa1-6854-4d9f-97f0-c2af74523614" width="50%"/>

Over the 10-year period, holding QQQ would have cost an investor nearly $140,000 in cumulative fees, assuming a $1M initial investment. This is because QQQ's 0.2% expense ratio is nearly 7 times higher than VOO/VTI's 0.03%.

VOO, VTI, VEU are clustered at the bottom, with total costs of only around $10,000 - $12,000 over the same period.

It is important to note that the expense ratio is charged on the total value of your investment, not just the initial $1M. As we saw in the previous charts, QQQ had the highest returns. This means the 0.20% fee was being applied to a rapidly growing pile of money. So, the "loss" shown in the chart isn't just the fee; it's the fee plus the money that fee would have earned if it had stayed invested.

---

## What weights of each ticker would yield the best return, lowest volatility and efficient sharpe ratio:
<img src="https://github.com/user-attachments/assets/2ac4534b-6192-4af1-965c-a2d081ddfae1" width="50%" />
<img src="https://github.com/user-attachments/assets/275a807b-3c5c-4adb-8db0-30bdd9ae46e0" width="50%"/>


To evaluate how different allocations among VOO, VTI, QQQ, and VEU perform, three portfolios were modeled: Aggressive (60% QQQ), Equal-weighted (25% each), and Conservative (80% VOO/VTI combined).

The Aggressive portfolio delivered the highest total return but also the highest volatility, consistent with QQQ’s tech-heavy exposure. The Equal and Conservative portfolios produced similar long-term returns with lower volatility, showing that diversification smooths compounding and reduces risk.

Overall, concentrated exposure to technology increases both return potential and short-term fluctuations, while balanced allocations across U.S. and international markets offer more stable, efficient growth.

---

## Market-Condition Performance

### a) COVID Crash (Feb–Mar 2020):
<img src="https://github.com/user-attachments/assets/941db183-4c49-490b-91e2-093d5e3bd2ef" width="50%" />

All four ETFs dropped ~30–35% highlighting how correlated global markets were during the COVID panic. 

QQQ recovered first, showing how tech’s relative immunity to lockdowns (remote work, e-commerce, etc.) helped it rebound faster.

VEU and VTI illustrate the drag from small caps and international exposure during global uncertainty.

### b) Interest Rates Hike (Jan 2022 - Dec 2022):
<img src="https://github.com/user-attachments/assets/6aef444e-0414-49de-b241-7e61ce19b344" width="50%" />

VEU was the least volatile fund throughout 2022. This is likely because international markets are less concentrated in the high-growth US tech stocks that were being hit hardest. And QQQ is consistently and dramatically higher than all the others. This is because high-growth technology stocks are the most sensitive to interest rate hikes.

### c) Interest Rate Cut Period (2023-2024):
<img src="https://github.com/user-attachments/assets/34fe77b6-5138-4ee1-82f9-6aa894b30458" width="50%"/>

QQQ shows the highest and most frequent volatility spikes, reflecting tech’s sensitivity to interest-rate shifts. VOO and VTI remain more stable, with lower, smoother volatility typical of broad U.S. market exposure. VEU moves similarly but with occasional divergences driven by global/geopolitical factors. Volatility clusters around policy uncertainty, then compresses once easing becomes clearer. The synchronized spikes indicate system-wide macro risk rather than ETF-specific shocks.

---

## Conclusions

Over the past decade, ETFs have provided efficient and low-cost diversification for investors. For cost-efficient, stable long-term exposure, VOO and VTI are optimal. QQQ offers superior growth potential at the expense of higher volatility and fees. VEU provides diversification benefits that smooth risk but may sacrifice returns. Allocation decisions should balance return objectives, tolerance for volatility, and desired geographic exposure.

Market condition analysis shows all ETFs were impacted by systemic shocks like COVID-19, yet the magnitude of their responses depended on composition. Large-cap ETFs (VOO) were more stable, total market funds (VTI) more sensitive to small-cap swings, and tech ETFs (QQQ) experienced the most dramatic rebounds and corrections.

---

## Resources:

- [Vanguard VEU ETF Profile](https://investor.vanguard.com/investment-products/etfs/profile/veu)
- [Vanguard VOO ETF Profile](https://investor.vanguard.com/investment-products/etfs/profile/voo)
- [Vanguard VTI ETF Profile](https://investor.vanguard.com/investment-products/etfs/profile/vti)
- [Invesco QQQ ETF Overview](https://www.invesco.com/qqq-etf/en/about.html)
- [yfinance](https://finance.yahoo.com/)
