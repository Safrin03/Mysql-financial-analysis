1. Companies with the Highest Market Capitalization
   
        SELECT
            Symbol,
            Name,
            Market_Cap
        FROM
            sp500
        ORDER BY
            Market_Cap DESC
        LIMIT 5;
   
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/9d8dba29-f8bc-48cb-9631-e465127912de)

2. Sector with the Highest Average PE Ratio
   
        SELECT
            Sector,
            AVG(PE) AS Avg_PE
        FROM
            sp500
        GROUP BY
            Sector
        ORDER BY
            Avg_PE DESC
        LIMIT 1;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/b631d5ac-5676-4784-bc8d-11473bda887e)

3. Distribution of Dividend Yields
   
        SELECT
            Dividend_Yield,
            COUNT(*) AS Frequency
        FROM
            sp500
        GROUP BY
            Dividend_Yield
        ORDER BY
            Dividend_Yield;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/4fbfa2a0-c1bf-4d52-8346-48cd22716ba7)

4. Sectors Outperforming in EPS
   
        SELECT
            Sector,
            AVG(EPS) AS Avg_EPS
        FROM
            sp500
        GROUP BY
            Sector
        ORDER BY
            Avg_EPS DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/daa5e01e-1812-426f-b559-0edf013edcaa)

5. Variation of PB Ratios Among Sectors
   
        SELECT
            Sector,
            AVG(PB) AS Avg_PB
        FROM
            sp500
        GROUP BY
            Sector
        ORDER BY
            Avg_PB DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/d284e0a8-d234-459f-963e-ad4d998748d0)

 6. Companies with the Most Significant Price Movements
    
        SELECT
            Symbol,
            Name,
            ABS(`52_Week_High` - `52_Week_Low`) AS Price_Volatility
        FROM
            sp500
        ORDER BY
            Price_Volatility DESC
        LIMIT 5;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/d1d074f6-a709-4a96-bcca-37d1342fd96b)


7. Sectors with the Highest Profitability Based on EBITDA
   
        SELECT
            Sector,
            AVG(EBITDA) AS Avg_EBITDA
        FROM
            sp500
        GROUP BY
            Sector
        ORDER BY
            Avg_EBITDA DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/806b74f7-d4ab-48fd-af2a-25a109cb952b)


8. Anomalies or Outliers Detection (example using Price as a metric)

        SELECT
            Symbol,
            Name,
            Price
        FROM
            sp500
        WHERE
            Price > 3 * (SELECT AVG(Price) FROM sp500);

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/4ab50055-93d6-42ef-9f42-7cbd9762f9f1)


9. Top Dividend-Yielding Companies in Each Sector :

        SELECT
            Sector,
            Symbol,
            Name,
            Dividend_Yield
        FROM
            sp500
        WHERE
            (Sector, Dividend_Yield) IN (
                SELECT
                    Sector,
                    MAX(Dividend_Yield) AS Max_Dividend_Yield
                FROM
                    sp500
                GROUP BY
                    Sector
            );

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/34294ac1-8f91-46c9-82c3-a43727ffd34b)


10. Companies with Highest EPS relative to Price

          SELECT
              Symbol,
              Name,
              EPS,
              Price,
              (EPS / Price) AS EPS_to_Price_Ratio
          FROM
              sp500
          ORDER BY
              EPS_to_Price_Ratio DESC
          LIMIT 5;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/ed3c4b5d-a69d-4e5c-8d33-76d02214e8a8)


11. EBITDA Margins Across Sectors using Market Cap as a proxy for Revenue

          SELECT
              Sector,
              AVG(EBITDA / Market_Cap) * 100 AS Avg_EBITDA_Margin
          FROM
              sp500
          GROUP BY
              Sector
          ORDER BY
              Avg_EBITDA_Margin DESC;

![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/ca1d5165-8cab-40f7-a129-a497a420a306)


12. Stocks Near 52-Week High with High Dividend Yields :

          SELECT
              Symbol,
              Name,
              `52_Week_High`,
              `52_Week_Low`,
              Dividend_Yield
          FROM
              sp500;
    
          WHERE
              `52_Week_High` > 0.9 * `52_Week_High` AND Dividend_Yield > 0.03
          ORDER BY
              `52_Week_High` DESC
          LIMIT 5;
  
![image](https://github.com/Safrin03/Mysql-financial-analysis/assets/135222070/5a0e4f7c-58ff-4848-ad2c-0ad539454349)
   
