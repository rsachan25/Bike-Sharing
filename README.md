# Bike Sharing Demand Prediction
This project aims to predict the demand for bike-sharing services using data from BoomBikes, a US-based bike-sharing provider. BoomBikes experienced a decline in revenue due to the COVID-19 pandemic and sought to understand the factors influencing bike rentals to prepare for a post-pandemic recovery. The goal of this project is to analyze various features, build a predictive model, and derive insights that can help BoomBikes optimize their business strategy to meet demand more effectively.

## Problem Statement
The global pandemic has led to a significant drop in bike-sharing usage, posing a challenge to BoomBikes' sustainability. As the company prepares to emerge from the lockdown, it aims to anticipate the demand for shared bikes by identifying the key factors that influence this demand. These insights will help BoomBikes adjust their strategy to attract more customers and stay competitive in the market.

## Business Objective
BoomBikes has collected a rich dataset on bike rentals, capturing various aspects like weather conditions, seasons, weekdays, and user behavior. The company has contracted a consulting firm to model the demand for shared bikes using this data. Specifically, the company wants to know:

* Which factors are significant in predicting bike demand.
* How well those factors explain the variation in bike rentals.
* Actionable insights to adjust business strategies and meet customer demand.
## Dataset Overview
The dataset contains 730 rows and 16 columns, capturing daily bike rental data across various seasons and weather conditions. Key columns include:

* cnt: The total number of bike rentals, including both casual and registered users.
* casual: Number of casual users who rented bikes.
* registered: Number of registered users who rented bikes.
* season: Encoded as 1 (spring), 2 (summer), 3 (fall), and 4 (winter).
* yr: Encoded as 0 for 2018 and 1 for 2019.
* mnth: Month of the year (1 to 12).
* weathersit: Weather conditions, ranging from clear skies to heavy rain or snow.
* temp, atemp, hum, windspeed: Continuous variables representing temperature, apparent temperature, humidity, and windspeed.
## Data Preparation
**Dropping Unnecessary Columns**

Certain columns were dropped to streamline the model-building process:

* instant: A unique identifier with no relevance to bike demand.
* dteday: The date column was dropped as its information is already captured in the mnth and weekday columns.
* casual and registered: Since the cnt column already sums both casual and registered users, these columns were removed to avoid redundancy and multicollinearity.

**Converting Numerical Variables into Categorical**
  
We converted several numerical variables into categorical values for better interpretability:

* season: Encoded as spring, summer, fall, and winter.
* weathersit: Weather conditions mapped to:\
  1: Clear skies or partly cloudy.\
  2: Mist or cloudy.\
  3: Light snow or light rain.\
  4: Heavy rain or snow.
  
**Insights from Exploratory Data Analysis (EDA)**

Through data exploration, we observed several key patterns:

* The fall season sees the highest demand for bike rentals, followed closely by summer. This indicates a clear seasonality in bike usage.
* September experiences the peak bike demand, while demand declines in the winter months.
* Clear weather conditions result in the highest number of bike rentals, while demand drops during misty, snowy, or rainy conditions.
* 2019 showed a significant increase in bike usage compared to 2018, reflecting the growing popularity of bike-sharing services.
* Demand remains fairly stable across weekdays, with a slight increase on weekends, particularly Fridays and Saturdays.

**Feature Engineering**

To prepare the dataset for analysis, we transformed the categorical variables into numerical values by creating dummy variables for columns like season, mnth, weekday, and weathersit. This step ensures that these categorical features can be effectively used in the predictive model, allowing for a more accurate linear regression by converting them into a numerical format. By doing so, we retain the meaningful distinctions between categories while making them usable for modeling purposes.\
This transformation allows the model to process these categories as numerical values, essential for linear regression.

## Model Building
**Splitting the Data**\
The data was split into training and testing sets to build and validate the model. The training set (70%) was used to train the model, while the test set (30%) was reserved for evaluating its performance.

**Rescaling the Features**\
We applied MinMaxScaler to normalize the continuous variables, ensuring all features are on the same scale.


**Correlation Analysis**\
A heatmap was used to assess the correlation between different variables and the target variable (cnt):

* Temperature (temp) and year (yr) showed the highest positive correlation with cnt.
* Windspeed and humidity had a negative impact on bike rentals, while holiday also showed lower bike usage on holidays.

**Recursive Feature Elimination (RFE)**

We used RFE to select the 15 most significant variables for the model. Variables like humidity and season_summer were dropped due to their high VIF values or insignificance in the presence of other factors.

## Final Model

The final linear regression model was built using the most significant variables. After iterative refinement, we arrived at a model that had an **R-squared score of 0.807** on the test data, meaning it explains 80.7% of the variance in bike demand.

**Final Model Equation**

The model's equation for predicting bike rentals (cnt) is:
Some basic Git commands are:
```
cnt = 0.2519 + 0.2341(year) - 0.0986(holiday) + 0.4515(temp) - 0.1398(windspeed)
     - 0.1108(season_spring) + 0.0473(season_winter) - 0.0727(month_july)
     + 0.0577(month_sep) - 0.2864(weathersit_Light_snow_rain) - 0.0811(weathersit_Mist)
```

**Significant Variables**

* Year: There was a notable increase in bike rentals in 2019 compared to 2018.
* Temperature: Higher temperatures encourage bike rentals, showing a positive correlation.
* Weather: Clear weather leads to higher demand, while light snow/rain and mist reduce demand.
* Seasonality: Spring has lower demand compared to fall, while July and September show higher bike rental activity.
* Windspeed: High windspeed discourages bike usage.

## Model Evaluation
To evaluate the model's effectiveness, we computed the R-squared score on the test data, yielding a result of 0.807. This indicates that the model successfully explains a large portion of the variability in bike demand. Additionally, the Adjusted R-squared score for the test dataset was 0.7774, further confirming the model's ability to generalize and perform well on new data.\

## Conclusion
This analysis provides valuable insights into the factors driving bike-sharing demand. The model demonstrates that weather, temperature, and seasonality significantly influence bike usage. The results suggest that BoomBikes can increase its service offerings during high-demand periods (summer and fall) and optimize pricing or marketing strategies based on weather conditions. Additionally, the steady growth in bike rentals from 2018 to 2019 indicates strong potential for continued business expansion in the future.
