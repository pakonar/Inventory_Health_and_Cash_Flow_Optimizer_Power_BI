##Total Revenue  
```
Total Revenue = SUMX(Fact_Sales, Fact_Sales[Quantity] * Fact_Sales[Unit Sales Price])
```
Calculation of the total sales scale. Using SUMX ensures correct aggregation by multiplying quantity and price at the individual transaction level before summing the results.  
##COGS (Cost of Goods Sold)  
```
COGS = SUMX(Fact_Sales, Fact_Sales[Quantity] * RELATED(Dim_Products[Unit_Cost_USD]))
```
The direct cost of goods sold. This measure links sales transactions with the purchase price from the product dimension, determining the actual capital cost involved in fulfilled orders.
##Gross Profit

Gross Profit = [Total Revenue] - [COGS]
Gross profit on sales. A key financial indicator representing the amount remaining to cover operating expenses, taxes, and fixed costs.
Gross Margin %
code
Dax
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)
Percentage profitability of sales. Enables an objective comparison of efficiency across different product categories regardless of their total sales volume.
Avg. Inventory Quantity
code
Dax
Avg. Inventory Quantity = 
AVERAGEX(
    VALUES(Fact_Inventory[Date]), 
    SUM(Fact_Inventory[Quantity])
)
Average number of units in stock. Using AVERAGEX over unique snapshot dates eliminates the error of double-counting inventory levels when aggregating over time.
Avg. Inventory Value
code
Dax
Avg. Inventory Value = 
AVERAGEX(
    VALUES(Fact_Inventory[Date]), 
    [Inventory Amount]
)
Average value of frozen capital. The primary cost indicator for logistics, determining the average value of goods held in stock during the analyzed period.
Inventory Turnover (Annualized)
code
Dax
Inventory Turnover = 
VAR DaysInPeriod = COUNTROWS(Dim_Date)
VAR AnnualizationFactor = DIVIDE(365, DaysInPeriod, 1)
VAR RawTurnover = DIVIDE([COGS], [Avg. Inventory Value], 0)
RETURN
RawTurnover * AnnualizationFactor
Inventory turnover ratio adjusted to an annual scale. The annualization mechanism allows for a reliable comparison of logistical efficiency across different time grains (e.g., comparing a single month to a full year).
Days of Supply
code
Dax
Days of Supply = DIVIDE(365, [Inventory Turnover], 0)
Number of days of supply. Translates the abstract turnover ratio into actionable operational data regarding how long current stock levels will last at the current sales velocity.
Potential Cash Released
code
Dax
Potential Cash Released = [Avg. Inventory Value] * [Inventory Reduction % Value]
Cash release simulation. A What-If analysis tool used to estimate the impact of inventory optimization on the company's liquidity and cash flow.
-----------------------------------------------------------------------
Total Revenue
code
Dax
Total Revenue = SUMX(Fact_Sales, Fact_Sales[Quantity] * Fact_Sales[Unit Sales Price])
Obliczenie całkowitej skali przychodu. Wykorzystanie funkcji SUMX zapewnia poprawną agregację poprzez mnożenie ilości i ceny na poziomie pojedynczej transakcji przed zsumowaniem wyników.
COGS (Cost of Goods Sold)
code
Dax
COGS = SUMX(Fact_Sales, Fact_Sales[Quantity] * RELATED(Dim_Products[Unit_Cost_USD]))
Koszt własny sprzedanych towarów. Miara łączy dane sprzedażowe z ceną zakupu z tabeli produktów, co pozwala określić realny koszt kapitału zaangażowanego w zrealizowane zamówienia.
Gross Profit
code
Dax
Gross Profit = [Total Revenue] - [COGS]
Zysk brutto na sprzedaży. Kluczowy wskaźnik określający kwotę pozostającą w przedsiębiorstwie na pokrycie kosztów operacyjnych i stałych.
Gross Margin %
code
Dax
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)
Rentowność procentowa sprzedaży. Pozwala na obiektywne porównanie efektywności różnych kategorii produktowych niezależnie od ich wolumenu sprzedaży.
Avg. Inventory Quantity
code
Dax
Avg. Inventory Quantity = 
AVERAGEX(
    VALUES(Fact_Inventory[Date]), 
    SUM(Fact_Inventory[Quantity])
)
Średnia liczba sztuk na magazynie. Zastosowanie AVERAGEX po unikalnych datach snapshotów eliminuje błąd wielokrotnego sumowania tych samych stanów magazynowych w czasie.
Avg. Inventory Value
code
Dax
Avg. Inventory Value = 
AVERAGEX(
    VALUES(Fact_Inventory[Date]), 
    [Inventory Amount]
)
Średnia wartość zamrożonego kapitału. Najważniejszy wskaźnik kosztowy logistyki, określający przeciętną wartość towaru zalegającego na regałach w analizowanym okresie.
Inventory Turnover (Annualized)
code
Dax
Inventory Turnover = 
VAR DaysInPeriod = COUNTROWS(Dim_Date)
VAR AnnualizationFactor = DIVIDE(365, DaysInPeriod, 1)
VAR RawTurnover = DIVIDE([COGS], [Avg. Inventory Value], 0)
RETURN
RawTurnover * AnnualizationFactor
Wskaźnik rotacji magazynu z uwzględnieniem skali roku. Mechanizm annualizacji pozwala na rzetelne porównywanie efektywności logistycznej w różnych przedziałach czasowych (miesiąc vs rok).
Days of Supply
code
Dax
Days of Supply = DIVIDE(365, [Inventory Turnover], 0)
Liczba dni zapasu. Przekłada abstrakcyjny wskaźnik rotacji na konkretną informację operacyjną o czasie, na jaki wystarczy obecny stan magazynowy przy aktualnym tempie sprzedaży.
Potential Cash Released
code
Dax
Potential Cash Released = [Avg. Inventory Value] * [Inventory Reduction % Value]
Symulacja uwolnienia gotówki. Narzędzie typu What-If pozwalające oszacować wpływ optymalizacji stanów magazynowych na płynność finansową przedsiębiorstwa.
