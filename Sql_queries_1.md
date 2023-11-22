 - Step 1: Create a Database
 
        CREATE DATABASE financial_analysis;
        USE financial_analysis;

- Step 2: Create a Table

        CREATE TABLE sp500 (
        Symbol VARCHAR(10),
        Name VARCHAR(255),
        Sector VARCHAR(255),
        Price DECIMAL(10, 2),
        PE DECIMAL(10, 2) SIGNED,
        Dividend_Yield DECIMAL(10, 9),
        EPS DECIMAL(10, 2) SIGNED,
        `52_Week_Low` DECIMAL(10, 2),
        `52_Week_High` DECIMAL(10, 2),
        Market_Cap DECIMAL(20, 2),
        EBITDA DECIMAL(20, 2) SIGNED,
        PS DECIMAL(10, 7),
        PB DECIMAL(10, 2),
        )


- Step 3: Load Data into the Table
 
        LOAD DATA LOCAL INFILE '"C:\Users\l\Downloads\financials.csv"'
        INTO TABLE sp500
        FIELDS TERMINATED BY ','
        LINES TERMINATED BY '\n'
        IGNORE 1 ROWS;
        -- Show table 
        SELECT * FROM sp500 LIMIT 10;

          
- (1) Data Exploration \
  (I) Examine the structure of the dataset to understand the available variables :
  
        -- Display the first few rows of the dataset
        SELECT * FROM sp500 LIMIT 10;
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/f06e21af-dc49-46d4-bc4c-0eddba531466)
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/72ed2bd0-8bb5-4b5e-a95b-8650182a75ec)

        -- View the table structure
        DESCRIBE sp500;
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/b4599180-bad2-4542-80da-a1bf1a64ce69)


  (II)  Check for missing values, outliers, and data distribution:

        -- Check for missing values in each column
        SELECT
            COUNT(*) AS TotalRows,
            COUNT(Symbol) AS Symbol_Not_Null,
            COUNT(Name) AS Name_Not_Null,
            COUNT(Sector) AS Sector_Not_Null,
            COUNT(Price) AS Price_Not_Null,
            COUNT(PE) AS PE_Not_Null,
            COUNT(Dividend_Yield) AS Dividend_Yield_Not_Null,
            COUNT(EPS) AS EPS_Not_Null,
            COUNT(`52_Week_Low`) AS `52_Week_Low_Not_Null`,
            COUNT(`52_Week_High`) AS `52_Week_High_Not_Null`,
            COUNT(Market_Cap) AS Market_Cap_Not_Null,
            COUNT(EBITDA) AS EBITDA_Not_Null,
            COUNT(PS) AS PS_Not_Null,
            COUNT(PB) AS PB_Not_Null
        FROM sp500;
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/0de09869-4e6e-4c7c-8166-39af56f00dbc)
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/822fc255-5a81-4e82-852c-3ebfb11a6438)

  
        -- Check for outliers
        SELECT
            Symbol,
            Name,
            Price,
            PE,
            Dividend_Yield,
            EPS,
            `52_Week_Low`,
            `52_Week_High`,
            Market_Cap,
            EBITDA,
            PS,
            PB
        FROM sp500
        WHERE Price IS NOT NULL AND (Price < 0 OR Price > 1000);
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/54d83191-1c2b-4e90-a9be-34f0d2521f53)

  
        -- Check data distribution for Price
        SELECT
            Price,
            COUNT(*) AS Frequency
        FROM sp500
        GROUP BY Price
        ORDER BY Price;


  (III) Gain an initial understanding of the overall financial landscape represented in the dataset:
  
        -- Calculate and display basic statistics for numerical columns
        SELECT
            AVG(Price) AS Avg_Price,
            MIN(Price) AS Min_Price,
            MAX(Price) AS Max_Price,
            AVG(PE) AS Avg_PE,
            AVG(Dividend_Yield) AS Avg_Dividend_Yield,
            AVG(EPS) AS Avg_EPS,
            AVG(`52_Week_Low`) AS Avg_52_Week_Low,
            AVG(`52_Week_High`) AS Avg_52_Week_High,
            AVG(Market_Cap) AS Avg_Market_Cap,
            AVG(EBITDA) AS Avg_EBITDA,
            AVG(PS) AS Avg_PS,
            AVG(PB) AS Avg_PB
        FROM sp500;

  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/b27ebd00-ac6a-49ef-97cc-ede8b80bd368)
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/55a8a140-b5bd-4541-bf21-30cef835cb94)      

- (2) Top Performers: \
  (I) Identify the top companies based on market capitalization, earnings per share (EPS), and other relevant metrics:
  
          -- Top companies by Market Capitalization
          SELECT Symbol, Name, Market_Cap
          FROM sp500
          ORDER BY Market_Cap DESC
          LIMIT 10;
  
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/acf1b120-ed41-4a98-afd4-f426e2128b62)
 
          -- Top companies by Earnings Per Share (EPS)
          SELECT Symbol, Name, EPS
          FROM sp500
          ORDER BY EPS DESC
          LIMIT 10;
          
 ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/f5c94ffd-564f-45a3-a86b-984f4524747c)
 
          -- Top companies by Price
          SELECT Symbol, Name, Price
          FROM sp500
          ORDER BY Price DESC
          LIMIT 10;
          
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/a886ef7c-ce82-4283-9b2b-8aeb72fd46b0)

   (II)  Determine the sectors that dominate the top-performing companies:
          -- Top sectors by Market Capitalization
          SELECT Sector, SUM(Market_Cap) AS Total_Market_Cap
          FROM sp500
          GROUP BY Sector
          ORDER BY Total_Market_Cap DESC
          LIMIT 5;
          
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/258a90c3-f2ee-47b1-97c7-c4034827524e)

          -- Top sectors by Earnings Per Share (EPS)
          SELECT Sector, AVG(EPS) AS Avg_EPS
          FROM sp500
          GROUP BY Sector
          ORDER BY Avg_EPS DESC
          LIMIT 5;
          
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/af5d53d2-905e-43ba-9cbf-a6f6068b9d5a)

          -- Top sectors by Price
          SELECT Sector, AVG(Price) AS Avg_Price
          FROM sp500
          GROUP BY Sector
          ORDER BY Avg_Price DESC
          LIMIT 5;
          
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/52a5b58e-e0ea-4629-9250-3ab82c2810ec)

 - (3) Sector Analysis :  \
   (I) Explore the average values of key financial metrics for each sector:
  
        -- Average values of key financial metrics for each sector
        SELECT
            Sector,
            AVG(Price) AS Avg_Price,
            AVG(PE) AS Avg_PE,
            AVG(Dividend_Yield) AS Avg_Dividend_Yield,
            AVG(EPS) AS Avg_EPS,
            AVG(Market_Cap) AS Avg_Market_Cap,
            AVG(PS) AS Avg_PS,
            AVG(PB) AS Avg_PB
        FROM sp500
        GROUP BY Sector;
   
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/191bf820-a2e6-4268-aaf3-9b841d8f76d5)

   (II) Identify sectors with the highest and lowest average values for metrics such as Price to Earnings (PE), Price to Sales (PS), and Dividend Yield:
  
         -- Sectors with the highest average Price to Earnings (PE)
         SELECT
             Sector,
             AVG(PE) AS Avg_PE
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_PE DESC
         LIMIT 1;
         
  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/875ac914-53a6-4bc3-b71c-acf3a0602eb5)

         -- Sectors with the lowest average Price to Earnings (PE)
         SELECT
             Sector,
             AVG(PE) AS Avg_PE
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_PE ASC
         LIMIT 1;
         
 ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/33f1b02e-f4d7-4ccd-867f-adb53eabe9d9)
 
         -- Sectors with the highest average Price to Sales (PS)
         SELECT
             Sector,
             AVG(PS) AS Avg_PS
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_PS DESC
         LIMIT 1;

  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/1faf7a06-f14c-4956-9cfc-e12d3fca6e9e)

         -- Sectors with the lowest average Price to Sales (PS)
         SELECT
             Sector,
             AVG(PS) AS Avg_PS
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_PS ASC
         LIMIT 1;

  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/6de1b197-9561-421b-b441-5c0d65627ba7)

         -- Sectors with the highest average Dividend Yield
         SELECT
             Sector,
             AVG(Dividend_Yield) AS Avg_Dividend_Yield
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_Dividend_Yield DESC
         LIMIT 1;

  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/345cf7d2-1d26-41a9-9814-35d619986656)

         -- Sectors with the lowest average Dividend Yield
         SELECT
             Sector,
             AVG(Dividend_Yield) AS Avg_Dividend_Yield
         FROM sp500
         GROUP BY Sector
         ORDER BY Avg_Dividend_Yield ASC
         LIMIT 1;

   ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/ef73323c-667b-4f04-bbe5-70be90295fa7)
     

 - (4) Market Dynamics:  \
   (I) Analyze the distribution of Price to Earnings (PE) ratios across the S&P 500 companies:
  
       -- Distribution of Price to Earnings (PE) ratios
       SELECT
           MAX(CASE WHEN PercentileRank <= 0.25 THEN PE END) AS Q1_PE,
           MAX(CASE WHEN PercentileRank <= 0.50 THEN PE END) AS Median_PE,
           MAX(CASE WHEN PercentileRank <= 0.75 THEN PE END) AS Q3_PE,
           MIN(PE) AS Min_PE,
           MAX(PE) AS Max_PE
       FROM (
           SELECT
               PE,
               PERCENT_RANK() OVER (ORDER BY PE) AS PercentileRank
           FROM sp500
       ) AS ranked_data;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/fd003d6c-b303-44f0-92c0-4a5c21d175b7)

       -- Number of companies in different PE ratio ranges
       SELECT
           CASE
               WHEN PE < 10 THEN '0-10'
               WHEN PE BETWEEN 10 AND 20 THEN '10-20'
               WHEN PE BETWEEN 20 AND 30 THEN '20-30'
               WHEN PE BETWEEN 30 AND 40 THEN '30-40'
               WHEN PE BETWEEN 40 AND 50 THEN '40-50'
               WHEN PE BETWEEN 50 AND 60 THEN '50-60'
               WHEN PE BETWEEN 60 AND 70 THEN '60-70'
               ELSE '70+'
           END AS PE_Range,
           COUNT(*) AS Num_Companies
       FROM sp500
       GROUP BY PE_Range
       ORDER BY PE_Range;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/1a6db4d9-9437-47ac-9529-69fbc3f4e2c7)


- (5) Dividend Analysis:  \
  (I) Distribution of Dividend Yields:
  
      -- Distribution of Dividend Yields
      SELECT
          Dividend_Yield,
          COUNT(*) AS Frequency
      FROM
          sp500
      GROUP BY
          Dividend_Yield
      ORDER BY
          Dividend_Yield;

  (II) Companies with High Dividend Yields:

        -- Companies with High Dividend Yields
        SELECT
            Symbol,
            Name,
            Dividend_Yield,
            Market_Cap,
            Earnings_Per_Share
        FROM
            sp500
        WHERE
            Dividend_Yield > 0.05
        ORDER BY
            Dividend_Yield DESC
        LIMIT 10;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/21e92ffd-be78-4b47-ba10-7d0156dffeec)


-  (6) Price Movement:  

        -- Analysis of 52-Week High and Low Prices
        SELECT
            Symbol,
            Name,
            `52_Week_High`,
            `52_Week_Low`,
            ABS(`52_Week_High` - `52_Week_Low`) AS Price_Volatility
        FROM
            sp500
        ORDER BY
            Price_Volatility DESC;
   
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/45ddf16f-5a62-4cd4-aa91-224b42976eed)

         -- Companies with Significant Price Movements
       SELECT
           Symbol,
           Name,
           `52_Week_High`,
           `52_Week_Low`,
           ABS(`52_Week_High` - `52_Week_Low`) AS Price_Volatility,
           Market_Cap
       FROM
           sp500
       WHERE
           ABS(`52_Week_High` - `52_Week_Low`) > 300 
       ORDER BY
           Price_Volatility DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/34fec350-ce09-46e0-9f8d-7f0e04e51c70)

   -  (7) Profitability Analysis:

          -- Profitability Assessment Using EBITDA
          SELECT
              Symbol,
              Name,
              Sector,
              EBITDA,
              Market_Cap,
              EBITDA / Market_Cap AS EBITDA_Margin
          FROM
              sp500
          ORDER BY
              EBITDA_Margin DESC;

  ![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/f19d20b0-9675-4dde-99f9-b93d311e2622)
   
          -- Comparison of Profitability Across Sectors
          SELECT
              Sector,
              AVG(EBITDA) AS Avg_EBITDA,
              AVG(Market_Cap) AS Avg_Market_Cap,
              AVG(EBITDA / Market_Cap) AS Avg_EBITDA_Margin
          FROM
              sp500
          GROUP BY
              Sector
          ORDER BY
              Avg_EBITDA_Margin DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/cea15ff7-1747-4144-a001-73096e42576d)

  
  -  (8) Valuation Metrics:

         -- Examination of Price to Book (PB) Ratios
         SELECT
             Symbol,
             Name,
             PB
         FROM
             sp500
         ORDER BY
             PB DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/ffef05b1-234a-49c5-a4bd-07fe991de705)

        -- Examination of Price to Sales (PS) Ratios
        SELECT
            Symbol,
            Name,
            PS
        FROM
            sp500
        ORDER BY
            PS DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/953756e3-3514-447f-b8e8-b816b502cd66)















