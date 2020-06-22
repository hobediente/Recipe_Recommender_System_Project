# Recipe Recommender System Project

Build a recipe reccomender system that recommends recipes based on nutrition metrics and ingredients.

Maintaining good eating habits is one of the best things a person can do for their wallet and health. Each year diabetes costs Americans $327 billion in medical fees and lost work and wages. Moreover, it is the 7th leading cause of death in America. More than 88 million US adults have Prediabetes-the precursor to diabetes 2,  which through lifestyle changes can be reversed. The goal of this project is to build a recipe reccomender system that helps people be more nutrition conscious with less effort.
 
<img src="Images/Fruit Banner.jpg"></img>

# DATA:

The data for this project is sourced from two places
1) Recipes - Kaggle (https://console.cloud.google.com/marketplace/details/iowa-department-of-commerce/iowa-liquor-sales) - Each recipe name is tokenized then later used as input for API calls.

2) Recipes - Edamam API (https://data.iowa.gov/) - Each observation is a recipe that has 28 measures for nutrition metrics, and other staple recipe information i.e. cook time.

# DATA ANALYSIS:

# 1. Data Collection:
In this step I collect, synthesize, and store recipe data.

# 2. Exploratory Analysis:
In this step recipe features are explored and visualized.

# 3. Data Cleaning:
In this step NLP cleaning of recipes takes place.

# 4. Modeling Sales:
In this step I build a system that reccomends recipes from my dataset that come closest to the desired nutrition meterics and ingredient specified by users.

### *For results, limitations, and takeaways scroll to bottom*

-----------------------------------------------------------------------------------------------------------

# Data Collection 

**Step 1 : Selecting the data**
The following steps were preformed using Google BigQuery

- Identify top distributers in Iowa Liquor Sales dataset
- Audit top distributers by the variety of alcohol they sell
- Select a top distributer that sells a wide variety of alcohol -- Luxico Inc-- and subset data for years 2017-2018 

- Select county-level demographic data for years 2017-2018

- Select county-level education data for years 2017-2018

### Conclusion: There are 99 counties in Iowa. Luxico Inc is the second largest distributer in Iowa, and sells 34 different categories of alcohol. 

**Step 2 : Aggregating the data**
The following steps were preformed using Python functionalities

- Clean the data
- Combine liquor invoice, demographic, and education CSV sheets on county name

**Step 3 : Feature Engineering**
The following steps were preformed using Pandas

- Create columns for...
   * The total educated population under the age of 25
   * The percent of population under the age of 25
   * The percent of population over 25
   * The percent of the population that is of drinking age
 
 - The df 
 <img src="Images/df.png"></img>
 
# Exploratory Analysis
- I divide the analysis into the following parts:

**A) Yearly Analysis**: Sales per category, sales per county, sales per bottle volume

**B) Monthly Analysis**: Total sales, sales per category

**C) Customer Analysis**: Analyzing relationship between population demographics and sales per county. 

**D) Predicting Sales**: Using demographic and sales data from 2017 to predict yearly sales per county for 2018.

# A) Yearly Analysis :
**Step 1 : Exploring the data**
The following steps are preformed using pandas functionalities

- Examine volume of liqour sold in gallons grouped by category
- Examine volume of liquor sold in gallons grouped by county
- Examine volume of liquor sold in gallons grouped by bottle size 

# A) Yearly Analysis :
**Step 2 : Visualizing the data**

In this step, I visualize the previous findings using plotly.express 

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/Gallons_per_Category.png"></img>

### Conclusion: American Vodkas account for nearly half of all sales

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/Gallons_per_County.png"></img>

### Conclusion: Ten out of ninety-nine counties account for over sixty percent of sales

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/Gallons_per_Bottle_Size.png"></img>

### Conclusion: 1750ml, 1000ml, and 750ml the dominate size of bottles sold

# B) Monthly Analysis :
**Step 1 : Exploring the data**

In this step, I preformed the following using pandas functionalities
- Examine total sales per month
- Examine total sales per month by category of alcohol 


# B) Monthly Analysis :
**Step 2 : Visualizing the data**

In this step, I visualized the previous findings using seaborn

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/2017_Sales_Over_Time.png" width="600" height="300"></img>

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/2018_Sales_Over_Time.png" width="600" height="300"></img>

### Conclusion: Sales appear to spike in even numbered months and fall in odd numbered months.

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/2017_Category_Sales.png" width="740" height="300"></img>

<img src="https://github.com/hobediente/Liquor_Sales_Supervised_Learning_Project/blob/master/Images/2018_Category_Sales.png" width="740" height="300"></img>

### Conclusion: Certain categories of alcohol appear to be seasonaly ordered i.e. mixto tequila, while others show more consistency. 

# C) Customer Analysis :
**Step 1 : Exploring the data**
In this step, I preformed the following using pandas functionalities

- Group DataFrame by county, summing for the total amount of liquor sold in gallons, and taking the mode for relevant population statics
- Examine the relationship between population demographics per county and sales

# C) Customer Analysis :
**Step 2 : Visualizing the data**

In this step, I visualized the previous findings using ploty.express

<img src="Images/Pop_Stats_and_Sales.png" width="600" height="600"></img>

### Conclusion: Sales are highly correlated to the percent of educated population under 25.


# Modeling Sales

**Step 1 : Selecting Model**
- Run random forest
- Run XGboost

**Step 2 : Tuning Models**
- Get feature importances
- Rerun models with only important features
- Run GridSearchCV to hypertune parameters
- Rerun models with hypertuned parameters

**Step 3 : Select Best Model**
- Compare goodness of model meterics and select best model
  * MAE, MSE, RMSE, MAPE
  
-----------------------------------------------------------------------------------------------------------

# Model Results :
- XGboost is the best preforming model 
- With input features of category, percent population with an education, and percent population under 25 the model achieved..
  * Training Score: 0.999, Test Score: 0.996
  * RMSE: 17357.78 (0.09% of total sales)
  
# Analysis Takeaways :
- Focus advertising resources on counties that bring in the most money
- Advertise for seasonal liquor at the beginning of their respective seasons
- Strengthen advertising to and around college campuses

# Limitations :
- I conducted this project before learning about techniques and models associated with time-series data
  * Moving forward I would check for seasonality and trends in sales, segment sales into quarters, engineer lag and window   features, then build new models to predict yearly sales based on first quarter sales. 
