# ABOUT THE PROJECT

This is an education project, I am analyzed the real dataset from [nature.com]([url](https://www.nature.com/)) about Carbon Footprint. 
I aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, I hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.

*Pay attention:
The carbon-emission values ​​come from the survey, so aggreates calculated in this analysis will be prioritized as averages.*


## Top 20 of the most carbon-emitting products

``` 
SELECT product_name, ROUND(AVG(carbon_footprint_pcf),2) AS avg_carbon
FROM product_emissions GROUP BY product_name
ORDER BY ROUND(AVG(carbon_footprint_pcf),2) DESC
LIMIT 20
```
*The result*
| product_name                                                                                                                       | avg_carbon | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00 | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00 | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00 | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00  | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00  | 
| TCDE                                                                                                                               | 99075.00   | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00   | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00   | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00   | 
| Mercedes-Benz SL-Class                                                                                                             | 69000.00   | 
| Mercedes-Benz S-Class Hybrid (S 400 h)                                                                                             | 66000.00   | 
| Mercedes-Benz CLS (350 BlueEFFICIENCY)                                                                                             | 60000.00   | 
| Mercedes-Benz CLS-Class                                                                                                            | 57100.00   | 
| Mercedes-Benz S-Class                                                                                                              | 54000.00   | 
| Electric Motor                                                                                                                     | 53551.67   | 
| Commercial Air Conditioner                                                                                                         | 51066.00   | 
| Mercedes-Benz S-Class Hybrid (S 300 BlueTEC HYBRID)                                                                                | 51000.00   | 
| Mercedes-Benz C-Class                                                                                                              | 50500.00   | 
| Mercedes-Benz E-Class (E 200)                                                                                                      | 50000.00   | 

#### Conclusion: 
Wind Turbine, Mercedes-Benz, and Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit. emitted the most products/product line in 2013 - 2017.

## The industry groups of the top 20 most carbon-emitting products

```
SELECT ind.industry_group,
       pro.product_name,
       ROUND(AVG(carbon_footprint_pcf),2) AS avg_carbon
FROM product_emissions AS pro 
LEFT JOIN industry_groups AS ind
ON pro.industry_group_id = ind.id
GROUP BY pro.product_name
ORDER BY avg_carbon DESC
LIMIT 20;
```
*The result*
| industry_group                     | product_name                                                                                                                       | avg_carbon | 
| ---------------------------------: | ---------------------------------------------------------------------------------------------------------------------------------: | ---------: | 
| Electrical Equipment and Machinery | Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00 | 
| Electrical Equipment and Machinery | Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00 | 
| Electrical Equipment and Machinery | Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00 | 
| Electrical Equipment and Machinery | Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00 | 
| Automobiles & Components           | Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00  | 
| Materials                          | Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00  | 
| Materials                          | TCDE                                                                                                                               | 99075.00   | 
| Automobiles & Components           | Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00   | 
| Automobiles & Components           | Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00   | 
| Automobiles & Components           | Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00   | 
| Automobiles & Components           | Mercedes-Benz SL-Class                                                                                                             | 69000.00   | 
| Automobiles & Components           | Mercedes-Benz S-Class Hybrid (S 400 h)                                                                                             | 66000.00   | 
| Automobiles & Components           | Mercedes-Benz CLS (350 BlueEFFICIENCY)                                                                                             | 60000.00   | 
| Automobiles & Components           | Mercedes-Benz CLS-Class                                                                                                            | 57100.00   | 
| Automobiles & Components           | Mercedes-Benz S-Class                                                                                                              | 54000.00   | 
| Capital Goods                      | Electric Motor                                                                                                                     | 53551.67   | 
| Capital Goods                      | Commercial Air Conditioner                                                                                                         | 51066.00   | 
| Automobiles & Components           | Mercedes-Benz S-Class Hybrid (S 300 BlueTEC HYBRID)                                                                                | 51000.00   | 
| Automobiles & Components           | Mercedes-Benz C-Class                                                                                                              | 50500.00   | 
| Automobiles & Components           | Mercedes-Benz E-Class (E 200)                                                                                                      | 50000.00   | 
#### Conclusion
Look at the top 20 most carbon-emitted products. Electrical Equipment and Machinery, and Automobiles & Components are the 2 industries with the largest carbon-emissions in the world.

## The highest carbon emissions industry

```
SELECT ind.industry_group,
       ROUND(AVG(pro.carbon_footprint_pcf),2) AS avg_carbon
FROM product_emissions AS pro 
LEFT JOIN industry_groups AS ind
ON pro.industry_group_id = ind.id
GROUP BY ind.industry_group
ORDER BY avg_carbon DESC
LIMIT 5;
```
*The result*
| industry_group                                   | avg_carbon | 
| -----------------------------------------------: | ---------: | 
| Electrical Equipment and Machinery               | 891050.73  | 
| Automobiles & Components                         | 35373.48   | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.00   | 
| Capital Goods                                    | 7391.77    | 
| Materials                                        | 3208.86    | 

#### Conclusion
Electrical Equipment and Machinery has the highest carbon-emissions industry, more than 25 times the second place.

## The highest carbon emissions company
```
SELECT com.company_name,
       ROUND(AVG(pro.carbon_footprint_pcf),2) AS avg_carbon
FROM product_emissions AS pro 
LEFT JOIN companies AS com
ON pro.company_id = com.id
GROUP BY pro.company_id
ORDER BY avg_carbon DESC
LIMIT 5;
```
*The result*
| company_name                           | avg_carbon | 
| -------------------------------------: | ---------: | 
| "Gamesa Corporación Tecnológica, S.A." | 2444616.00 | 
| "Hino Motors, Ltd."                    | 191687.00  | 
| Arcelor Mittal                         | 83503.50   | 
| Weg S/A                                | 53551.67   | 
| Daimler AG                             | 43089.19   |  
#### Conclusion
Gamesa Corporación Tecnológica, S.A. is the highest carbon emissions company, nearly 13 times of carbon emissions with the second place.

## The highest carbon emissions country

```
SELECT coun.country_name,
       ROUND(avg(pro.carbon_footprint_pcf),2) AS avg_carbon
FROM product_emissions AS pro 
LEFT JOIN countries AS coun
ON pro.country_id = coun.id
GROUP BY pro.country_id
ORDER BY avg_carbon DESC
LIMIT 5;
```
*The result*
| country_name | avg_carbon | 
| -----------: | ---------: | 
| Spain        | 699009.29  | 
| Luxembourg   | 83503.50   | 
| Germany      | 33600.37   | 
| Brazil       | 9407.61    | 
| South Korea  | 5665.61    | 

 #### Conclusion
 Spain is the highest carbon emissions country.

 ## The trend of carbon footprints (PCFs) over the years
 
```
SELECT year,
       ROUND(SUM(carbon_footprint_pcf),2) AS total_carbon
FROM product_emissions GROUP BY year;
```
*The result*
| year | total_carbon | 
| ---: | -----------: | 
| 2013 | 503857.00    | 
| 2014 | 624226.00    | 
| 2015 | 10840415.00  | 
| 2016 | 1640182.00   | 
| 2017 | 340271.00    | 

#### Conclusion
The amount of carbon emitted into the world tends to increase gradually and peaked in 2015, then it decreased steadily until 2017 with the amount of carbon only about 3.1% of the 2015 peak.

## The most industries notable decrease in carbon footprints (PCFs) over time

To know the most notable industry decrease, we will set the values in 2015 (the peak milestone) into the old value, and 2017 (the last milestone) is the new value.

To retrieve the values of 2017 and 2015, we will utilize WITH (CTE) to create 2 fake table and then combine them to calculate the difference and percentage change.
Because reusability improves query readability and modularity more than sub queries.

```
WITH carbon_2015 AS (
                   SELECT ind.industry_group as industry,
                          ROUND(SUM(carbon_footprint_pcf),2) AS total_carbon
                   FROM product_emissions AS pro 
                   LEFT JOIN industry_groups AS ind
                   ON pro.industry_group_id = ind.id
                   WHERE pro.year = 2015 GROUP BY ind.industry_group
  		              ),
    carbon_2017 AS (
                  	SELECT ind.industry_group as industry,
                  	       ROUND(SUM(carbon_footprint_pcf),2) AS total_carbon
                  	FROM product_emissions AS pro 
                	  LEFT JOIN industry_groups AS ind
                	  ON pro.industry_group_id = ind.id
                	  WHERE pro.year = 2017 GROUP BY ind.industry_group
  		              )		
SELECT carbon_2017.industry,
       carbon_2017.total_carbon - carbon_2015.total_carbon as diff,
       ROUND((((carbon_2017.total_carbon - carbon_2015.total_carbon)/carbon_2015.total_carbon)*100),2) as pct_change
FROM carbon_2017 LEFT JOIN carbon_2015
ON carbon_2017.industry =  carbon_2015.industry
ORDER BY diff;
```
*The result*
| industry                           | diff      | pct_change | 
| ---------------------------------: | --------: | ---------: | 
| Commercial & Professional Services | [NULL]    | [NULL]     | 
| Materials                          | [NULL]    | [NULL]     | 
| Technology Hardware & Equipment    | -78565.00 | -74.01     | 
| Software & Services                | -22166.00 | -96.98     | 
| "Food, Beverage & Tobacco"         | 3162.00   | [NULL]     | 
| Capital Goods                      | 91444.00  | 2608.96    | 

#### Conclusion
Comparing to the amout carbon in 2015, Sofware & Services, and Technology Hardware & Equipment are the only two industries with the carbon emissions reduced, by 78,565 and 22,166 PCF. In particular, the Software & Services industry has almost reduced carbon emissions to the world by about 97%.

