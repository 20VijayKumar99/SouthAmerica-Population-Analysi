# South American Population & Demographics Analysis

## Overview
This Power BI project analyzes the population growth, urbanization, and demographic trends of South America. It provides interactive visualizations to understand key indicators like total population, urbanization rate, and urban agglomeration.

## DAX Calculations
The following DAX calculations were used to derive insights from the dataset:

1. **Population Growth (Annual%)**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year]))
VAR PopGrowth = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.POP.GROW", 
        Data[Year] = SelectedYear
    )
RETURN IF(ISBLANK(PopGrowth), 0, PopGrowth)
```

2. **Population in Urban Agglomerations (>1 Million, % of Total Population)**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year])) 
VAR AgglomerationPercentage = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "EN.URB.MCTY.TL.ZS", 
        Data[Year] = SelectedYear
    ) / 100
RETURN IF(ISBLANK(AgglomerationPercentage), 0, AgglomerationPercentage)
```

3. **Total Population**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year])) 
VAR Population = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.POP.TOTL", 
        Data[Year] = SelectedYear
    )
RETURN IF(ISBLANK(Population), 0, Population)
```

4. **Urban Population**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year])) 
VAR UrbanPop = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.URB.TOTL", 
        Data[Year] = SelectedYear
    )
RETURN IF(ISBLANK(UrbanPop), 0, UrbanPop)
```

5. **Urban Population %**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year]))
VAR TotalPop = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.POP.TOTL", 
        Data[Year] = SelectedYear
    )
VAR UrbanPop = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.URB.TOTL", 
        Data[Year] = SelectedYear
    )
RETURN 
IF(NOT(ISBLANK(TotalPop)) && NOT(ISBLANK(UrbanPop)), (UrbanPop / TotalPop) * 100, 0)
```

6. **Urban Population Growth (Annual %)**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year])) 
VAR UrbanGrowth = 
    CALCULATE(
        SUM(Data[Indicator Value]), 
        Data[Indicator Code] = "SP.URB.GROW", 
        Data[Year] = SelectedYear
    )
RETURN IF(ISBLANK(UrbanGrowth), 0, UrbanGrowth)
```

7. **Avg Urban Population %**
```DAX
VAR SelectedYear = SELECTEDVALUE(Data[Year], MAX(Data[Year])) 
RETURN 
AVERAGEX(
    FILTER(Data, Data[Year] = SelectedYear && Data[Indicator Code] = "SP.URB.TOTL.IN.ZS"), 
    Data[Indicator Value]
)
```

## Visuals Used
The Power BI dashboard includes the following visualizations:
- **Cards**: Display key indicators such as Total Population, Urban Population, and Population Growth.
- **Line Chart**: Trends of population growth over the years.
- **Pie Chart**: Distribution of population by country.
- **Clustered Time Series Chart**: Earliest date, total population, urban population, and average urban population %.
- **Clustered Column Chart**: Urban agglomeration over the years.
- **Pie Chart**: Population by income group.
- **Comparison Charts**: Rural vs. urban population.
- **Predictive Analysis**: Line charts forecasting urban and total population trends.

## How to Use
1. Import the Power BI report.
2. Interact with filters to view trends across different years.
3. Use predictive analysis to forecast future urbanization trends.

## Conclusion
This Power BI report helps policymakers, urban planners, and researchers understand demographic changes in South America. Future improvements could include deeper analysis on income groups, migration trends, and regional comparisons.
