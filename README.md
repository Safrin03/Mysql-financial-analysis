# S&P 500 Financial Insights: Analyzing Market Dynamics and Company Performance

## Data Used

**Data Description:**

Used a Kaggle Dataset **"[S&P Companies with Financial information](https://www.kaggle.com/datasets/paytonfisher/sp-500-companies-with-financial-information)"**

This is a comprehensive dataset including numerous financial metrics that many professionals and investing gurus often use to value companies. This data is a look at the companies that comprise the S&P 500 (Standard & Poor's 500). The S&P 500 is a capitalization-weighted index of the top 500 publicly traded companies in the United States (top 500 meaning the companies with the largest market cap). The S&P 500 index is a useful index to study because it generally reflects the health of the overall U.S. stock market. The dataset was last updated in July 2020.

There are 14 Columns included in this dataset:
 - 4 character variables:

        - Symbol: Ticker symbol used to uniquely identify each company on a particular stock market
        - Name: Legal name of the company
        - Sector: An area of the economy where businesses share a related product or service
        - SEC Filings: Helpful documents relating to a company
- 10 numeric variables:

        - Price: Price per share of the company
        - Price to Earnings (PE): The ratio of a company’s share price to its earnings per share
        - Dividend Yield: The ratio of the annual dividends per share divided by the price per share
        - Earnings Per Share (EPS): A company’s profit divided by the number of shares of its stock
        - 52 week high and low: The annual high and low of a company’s share price
        - Market Cap: The market value of a company’s shares (calculated as share price x number of shares)
        - EBITDA: A company’s earnings before interest, taxes, depreciation, and amortization; often used as a proxy for its profitability
        - Price to Sales (PS): A company’s market cap divided by its total sales or revenue over the past year
        - Price to Book (PB): A company’s price per share divided by its book value


## Objective :
To conduct a comprehensive financial data analysis of the S&P 500 companies dataset to gain insights into the financial performance and market dynamics. The primary focus is on understanding key financial metrics, identifying top-performing sectors, and uncovering patterns that may influence investment decisions.

## Questions :
1. Which companies have the highest market capitalization in the S&P 500?
2. Which sector has the highest average Price to Earnings (PE) ratio?
3. What is the distribution of dividend yields across the S&P 500?
4. Are there any sectors that consistently outperform others in terms of earnings per share (EPS)?
5. How do the Price to Book (PB) ratios vary among different sectors?
6. Which companies experienced the most significant price movements in the past 52 weeks, and what factors contributed to these movements?
7. Which sectors show the highest profitability based on EBITDA?
8. Are there any anomalies or outliers in the dataset that require further investigation?
9. Which are the Top Dividend-Yielding Companies in Each Sector?
10. Which Companies have the Highest EPS relative to Price?
11. What is the EBITDA Margins Across variuos Sectors?
12. Find stocks near 52-Week High with High Dividend Yields.

## Approach :
1) Created a Database
2) Imported the Dataset
3) Explored the Data
4) Performed Financial Analysis
5) Data Visualization

## Summary Findings :
**Dataset Overview:**
- The dataset contains information on various financial metrics for 494 companies, including symbols, names, sectors, prices, P/E ratios, dividend yields, EPS, and more.
- There are no missing values in the dataset, and it consists of 13 columns and 494 rows.

**Outliers:**
- Outliers were identified in companies like Google (GOOGL, GOOG), Amazon (AMZN), and Priceline (PCLN) across various financial metrics.

**Data Distribution:**
- The distribution of the Price column shows a wide range of prices, with the highest being $1806.06 for Priceline.com Inc.
- The Price to Earnings (PE) ratio distribution ranges from -251.53 to 520.15, with some negative values indicating potential data issues.

**Basic Statistics:**
- Average values for key financial metrics across all companies were calculated, providing insights into the overall market landscape.

**Top Companies and Sectors:**
- Top companies were identified based on market capitalization, earnings per share (EPS), and price. Apple Inc. emerged as the top company by market capitalization.
- Information Technology, Financials, and Health Care are the top sectors by market capitalization, EPS, and price, respectively.

**Average Metrics by Sector:**
- Average values of key financial metrics were calculated for each sector, revealing sector-specific insights into price, P/E ratio, dividend yield, and more.

**Price to Earnings (PE) Analysis:**
- The average PE ratio for the Information Technology sector is notably high, indicating potential overvaluation compared to other sectors.
- Telecommunication Services has the lowest average PE ratio, suggesting potential undervaluation.

**Price to Sales (PS) and Dividend Yield Analysis:**
- Real Estate has the highest average Price to Sales (PS) ratio, while Telecommunication Services has the lowest.
- Telecommunication Services has the highest average dividend yield, while Health Care has the lowest.

**Distribution Analysis:**
- The distribution of PE ratios shows a wide range, with the interquartile range (Q1 to Q3) between 15.35 and 25.76.

**Sectors Outperforming in EPS:**
- Telecommunication Services has the highest average EPS at 6.06, followed by Industrials and Materials.
- Energy sector has a negative average EPS, indicating lower earnings per share.

**Variation of PB Ratios Among Sectors:**
- Consumer Staples has the highest average PB ratio, followed by Consumer Discretionary and Information Technology.
- Utilities and Energy sectors have the lowest average PB ratios.

**Companies with the Most Significant Price Movements:**
- Amazon.com Inc (AMZN) has the highest price volatility, followed by Priceline.com Inc (PCLN) and Alphabet Inc (GOOG and GOOGL).

**Sectors with the Highest Profitability Based on EBITDA:**
- Telecommunication Services has the highest average EBITDA, followed by Information Technology and Consumer Staples.
- Financials and Real Estate sectors have relatively lower EBITDA.

**Companies with Highest EPS relative to Price:**
- Allergan, Plc (AGN) has the highest EPS-to-Price ratio, followed by Ford Motor (F) and Goodyear Tire & Rubber (GT).

**EBITDA Margins Across Sectors using Market Cap as a proxy for Revenue:**
- Telecommunication Services has the highest average EBITDA margin, followed by Utilities and Consumer Discretionary.
- Financials and Health Care sectors have lower EBITDA margins.

**Stocks Near 52-Week High with High Dividend Yields:**
- BlackRock (BLK) and Lockheed Martin Corp. (LMT) are near their 52-week highs and offer high dividend yields.
- Sherwin-Williams (SHW) has a lower dividend yield compared to others.

## Conclusion:
- The dataset provides a comprehensive view of the financial metrics of various companies in different sectors.
- Outliers and potential data issues, such as negative PE ratios, need further investigation and cleaning.
- **Overall Sector Performance:**
    - Telecommunication Services outperforms in terms of both EPS and EBITDA margin.
    - Consumer Staples has the highest PB ratio, indicating potentially overvalued stocks.
- **Company Performance:**
    - Amazon.com Inc (AMZN) has the most significant price movements, reflecting high volatility.
    - Allergan, Plc (AGN) stands out with the highest EPS-to-Price ratio.
- **Financial Health:**
    - Sectors like Energy and Financials exhibit lower average EPS and EBITDA, suggesting potential financial challenges.
- **Investment Opportunities:**
    - Companies near their 52-week highs with high dividend yields, such as BlackRock (BLK) and Lockheed Martin Corp. (LMT), might be of interest to investors.
- Investors and analysts can use this information to make informed decisions based on the financial health and performance of companies in different sectors.




