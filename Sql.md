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

- (1) Data Exploration \
  (I) Examine the structure of the dataset to understand the available variables :
  
        -- Display the first few rows of the dataset
        SELECT * FROM sp500 LIMIT 10;
  
        -- View the table structure
        DESCRIBE sp500;

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

  (2) Top Performers: \
  (I) Identify the top companies based on market capitalization, earnings per share (EPS), and other relevant metrics:
  
          -- Top companies by Market Capitalization
          SELECT Symbol, Name, Market_Cap
          FROM sp500
          ORDER BY Market_Cap DESC
          LIMIT 10;
  
          -- Top companies by Earnings Per Share (EPS)
          SELECT Symbol, Name, EPS
          FROM sp500
          ORDER BY EPS DESC
          LIMIT 10;
  
          -- Top companies by Price
          SELECT Symbol, Name, Price
          FROM sp500
          ORDER BY Price DESC
          LIMIT 10;
  
