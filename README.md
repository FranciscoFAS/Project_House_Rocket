<h1 align="center"> Business Solution for Real Estate Company </h1>

<p align="center">A Data Analysis Project</p>

<h1 align="center">
  <img alt="houserocketlogo" title="#houserocketlogo" src="image/house-rocket.jpg" />
</h1>

*Obs: The  company and business problem are both fictitious, although the data is real.*
  
*The in-depth Python code explanation is available in [this](https://github.com/FranciscoFAS/Project_House_Rocket/blob/cebfd6d5aa9cd7298dc8e1f743cc33a8bc81151a/notebook/Project_House_Rocket.py) Python Script.*

# 1. **House Rocket and Business Problem**
<p align="justify"> House Rocket is a real estate company whose business model consists in identifying good deals, so that those properties could be bought for an interesting price and futurely sold for a higher price, therefore the company could turn in a profit. For this particular instance, House Rocket will operate in King County, which includes Seattle. </p>

This **Data Science** project is focused on solving two problems: 

 - **Problem 1: Which properties should House Rocket buy and for which suggested price?**
 - **Problem 2: Once a property is bought, for which price should it be sold?**

# 2. **Data Overview**
The data was collected from [Kaggle](https://www.kaggle.com/). This [dataset](https://www.kaggle.com/datasets/harlfoxem/housesalesprediction) contains house sales prices for King County, from May 2014 to May 2015. The features descriptions are available below:


| Feature | Definition |
|---|---|
| id | Unique ID for each home sold |
| date | Date of the home sale |
| price | Price of each home sold |
| bedrooms | Number of bedrooms |
| bathrooms | Number of bathrooms, where .5 accounts for a room with a toilet but no shower |
| sqft_living | Square footage of the apartments interior living space |
| sqft_lot | Square footage of the land space |
| floors | Number of floors |
| waterfront | A dummy variable for whether the apartment was overlooking the waterfront or not |
| view | An index from 0 to 4 of how good the view of the property was |
| condition  | An index from 1 to 5 on the condition of the apartment |
| grade  | An index from 1 to 13, where 1-3 falls short of building construction and design, 7 has an average level of construction and design, and 11-13 have a high quality level of construction and design. |
| sqft_above | The square footage of the interior housing space that is above ground level |
| sqft_basement | The square footage of the interior housing space that is below ground level |
| yr_built | The year the house was initially built |
| yr_renovated | The year of the house’s last renovation |
| zipcode | What zipcode area the house is in |
| lat | Lattitude |
| long | Longitude |
| sqft_living15 | The square footage of interior housing living space for the nearest 15 neighbors |
| sqft_lot15 | The square footage of the land lots of the nearest 15 neighbors |


# 3. **Assumptions**

 - Location in real estate is undoubtedly a decisive factor in price evaluation.
 - So that the business problems could be solved the **ad_season** feature was created. It's a column that shows on which season the property was announced in the real estate market (spring, summer, fall or winter).

# 4. **Solution Plan**
## 4.1. How were both problems solved?

### **Problem 1: Which properties should House Rocket buy and for which suggested price?**
<p align="justify"> To solve this problem, we firstly need to analyse the properties by their location, because in real estate, location is undoubtedly a decisive factor in price evaluation. One interesting metric in this case is to calculate the price median by each zipcode, as the median isn't influenced by extreme values (outliers) in the data. </p>

The properties that will receive a buy suggestion will be the ones that fulfill the two following rules:

- Their asked price has to be lower than the median price for that region
- The property needs to be in good conditions, which means condition >= 3

<p align="justify"> As for the suggested price, the density by region will be taken into account, which means that for properties in regions that have a higher number of real estate ads it's viable to offer lower prices, and vice-versa. Therefore the rule for suggested buy prices is: </p> 

- From 0 to 204 properties in the region => Offer the asked price 
- From 205 to 282 properties in the region => Offer 3% less than the asked price
- From 283 to 408 properties in the region => Offer 4% less than the asked price
- From 409 properties upwards => Offer 5% less than the asked price

### **Problem 2: Once a property is bought, for which price should it be sold?**

<p align="justify"> To suggest a sell price, again the density by region will be considered, since for regions where the number of real estate ads is lower it's possible to sell the property for a higher price, and vice-versa. Hence, a reasonable rule for suggested sell prices is: </p>

- From 0 to 204 properties in the region => Sell for 16% than the suggested buy price 
- From 205 to 282 properties in the region => Sell for 14% than the suggested buy price
- From 283 to 408 properties in the region => Sell for 12% than the suggested buy price
- From 409 properties upwards => Sell for 10% than the suggested buy price

<p align="justify"> <i>It's important to point out that selling a property for 10-16% more than the paid price is just a suggestion, so that the selling prices are realistic, since selling a property on a short run for say 30-40% more, although it can happen, it seems unlikely (or it would take too long to sell).</i> </p>

## 4.2. What was delivered as a **solution**?
 - Solution to Problem 1:  
    
    - [Buy Suggestion Table](https://github.com/FranciscoFAS/Project_House_Rocket/tree/cebfd6d5aa9cd7298dc8e1f743cc33a8bc81151a/suggestion/buy): Contains buy suggestions and suggested buy prices

 - Solution to Problem 2: 
    - [Sell Suggestion Table](https://github.com/FranciscoFAS/Project_House_Rocket/tree/cebfd6d5aa9cd7298dc8e1f743cc33a8bc81151a/suggestion/sell): Contains suggested sell prices and profit

 - Financial Results:
    - [Profit descriptive analysis](https://github.com/FranciscoFAS/Project_House_Rocket/results/profit-descriptive-analysis.csv)
    - [Average and median profit grouped by ad_season]("https://github.com/FranciscoFAS/Project_House_Rocket/results/med-avg-profit-by-zipcode-season.csv")
    - [Average and median profit grouped by zipcode]("https://github.com/FranciscoFAS/Project_House_Rocket/results/med-avg-profit-by-zipcode.csv")
    - [Average and median profit grouped by ad_season and zipcode]("https://github.com/FranciscoFAS/Project_House_Rocket/results/med-avg-profit-by-season.csv")
    - [House Rocket Cloud App](https://projecthouserocket.onrender.com): App deployed using Streamlit Cloud containing all tables (Buy Suggestion Table, Sell Suggestion Table and Financial Results Tables) with filters and a Buy Suggestion Map, as well as data insights.
    
 <i> Because the deployment was made in a free cloud (Render) it could take a few minutes for the page to load in the **first time**. </i>

## 4.3. Tools and techniques used:
- [Python 3.9.12](https://www.python.org/downloads/release/python-3912/), [Pandas](https://pandas.pydata.org/), [Matplotlib](https://matplotlib.org/), [Plotly](https://plotly.com/python/) and [Geopandas](https://geopandas.org/en/stable/).
- [VSCode](https://code.visualstudio.com/). 
- [Render](https://dashboard.render.com/).
- [Github](https://github.com/).
- [Measures of Central Tendency and Dispersion](https://towardsdatascience.com/statistics-central-tendency-5e514a2f98fd).
- [Exploratory Data Analysis (EDA)](https://towardsdatascience.com/exploratory-data-analysis-8fc1cb20fd15). 

# 5. **Business Insights**

 - ### 1st - Properties that possess waterfront view are, on average, 212.38% more expensive in comparison to the ones that do not have such feature.
<p align="center">
  <img src="" alt="drawing" width="750"/>
</p>

#### **Usage**: House Rocket could focus on buying and selling waterfront view properties, since the profit will be higher in absolut values. 
--- 
- ### 2nd - Properties that do not have a basement are, on average, 27.71% cheaper in comparison to the ones that have such feature.
<p align="center">
  <img src="" alt="drawing" width="750"/>
</p>

#### **Usage**: House Rocket could look to buy properties without a basement that have the potential to possess one. Therefore these properties can be sold for a lot higher price. 
---
- ### 3rd - Properties with good views are, on average, 1.89 times more expensive than the ones with not so good views
<p align="center">
  <img src="" alt="drawing" width="750"/>
</p>

#### **Usage**: House Rocket could focus on buying and selling properties with good views, since the profit will be higher in absolut values.
---
- ### 4th - Regions bordering Lake Washington produce, on average, 36.23% more profit in comparison to other regions.
<p align="center">
  <img src="" alt="drawing" width="750"/>
</p>

#### **Usage**: House Rocket could focus on buying and selling properties around Lake Washington, since the profit will be higher in absolut values.
---
- ### 5th - Properties with the lowest prices (on average) were built from 1941 to 1983.
<p align="center">
  <img src="" alt="drawing" width="750"/>
</p>

#### **Usage**: House Rocket would have higher profits buying and selling properties built from the mid 1980's upwards, as well as the ones built from 1900 to 1940.

# 6. **Financial Results**

<p align="justify"> Three interesting metrics to evaluate the financial performance for this solution is the profit mean and median (grouped by ad_season, zipcode and ad_season with zipcode), as well as the total profit. This in-depth information can be found in <a href="https://github.com/FranciscoFAS/Project_House_Rocket/tree/cebfd6d5aa9cd7298dc8e1f743cc33a8bc81151a/results">here</a>. As for the profit for each property it can be checked in the <a href="https://projecthouserocket.onrender.com">House Rocket Cloud App</a>, where filters can also be applied for better visualization. </p>

<p align="justify"> <b> If this feasible solution strategy used in this project were applied by House Rocket the total obtained profit would be US$ 473,094,328.48, with an average profit of US$ 45,337.26 per property. The main profit metrics are displayed below: </b></p>

<div align="center">
 
| **Metric** | **US$** |
|---|---|
| Total Profit | 473,094,328.48 |
| Profit Mean | 45,337.26 |
| Profit Median | 39,995.00 |
| Min Profit | 8,217.50 |
| Max Profit | 350,036.80 |
 
</div>

# 7. **Conclusion**
In this project the two main objectives were accomplished:

 - A feasible solution was found for both business problems, leading to profitable results.
 - Five interesting and useful insights were found through Exploratory Data Analysis (EDA).

 We also managed to deliver tables with in-depth financial results, as well as buy and sell suggestion tables. All this information can be filtered by using the House Rocket Streamlit App, that also has the five business insights and a interactive Buy Suggestion Map.   
  
<div align="center">

|         **Click below to access the App**        |
|:------------------------:|
|         [![Render App](data:image/png;base64,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)](https://project-house-rocket.onrender.com/)
</div>
 
# 8. **Next Steps**
<p align="justify"> Further on, this solution could be improved by using <a href="https://www.imsl.com/blog/what-is-regression-model">regression models</a> to determine wheter a property has a good buying price, and for which price it could be bought and sold. Another interesting study would be to produce a market research, so that data about clients could be collected. Then, a <a href="https://machinelearningmastery.com/clustering-algorithms-with-python/">clustering algorithm</a> could be applied to identify what types of property features each group of customers would prefer. </p>

# Contact

- af_nand@outlook.com
- [![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fernando-francisco-06936512a/)
