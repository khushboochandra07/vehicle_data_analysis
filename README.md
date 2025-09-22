## feature-determining-car-prices

Vehicle data analysis repository investigates and creates independent analysis to provide clear recommendation to my client-a used car dealreship-as to what consumers value in a car using CRISP-DM framework. vehicles.csv data from kaggle contains information of 426K cars for the analysis. 

## Jupyter Notebook

[Link to Jupyter Notebook](https://https://github.com/khushboochandra07/vehicle_data_analysis/blob/main/jupyternotebook/1_feature_determining_car_price.ipynb)


[Link to CSV data](https://https://github.com/khushboochandra07/vehicle_data_analysis/blob/main/data/vehicles.csv)


## CRISP_DM Framework

![CRISP-DM Framework](/images/crispdm.png)

### **Business Understanding**  

*   The used car dealership stocks preowned vehicle models from various manufacturers.
*   Business wants to understand what features determine the price of the car.
*   This could result in various decision taken by the client to maximize profit and stock cars that attract more users.


### **Data Understanding**  

The vehicle data provided as part of the analysis has data about sale price from few years for various cars, vans, trucks for preowned vehicles. It also contains columns columns like condtion, odometer reading, drive and fuel. This data directly ties to the ask from the client.

*   Size of original data is 426880 rows and 18 columns
*   Many columns are missing data
*   Price column looks good for most part but there are outliers in the data
*   Id column doesn't convey any information about the data itself
*   Size column is missing 71.8% values
*   Manufacturer, model, type, year are missing data which may or may not have VIN
*   Title status, type, condition, cylinders, fuel have finite categorical values
*   Data quality for model column is poor and will need some more work

### **Data Preparation**  

Multiple steps have been applied to clean the data:
*   Remove duplicates - there were none in the dataset provided
*   Drop columns id and size as id is not adding any value to the dataset and size is missing for 71.8% of the data.
*   Fix datatype for columns

Multiple data transformations steps were applied:
*   VIN based transformation to impute missing year, model, type and manufacturer for the cars.
*   Drop rows with missing values for subset 'year','odometer','model','manufacturer'
*   Remove outliers for price. This step can be skipped as price is the target.
*   Apply transformation for cylinders to make it numeric
*   Apply transformation to type column to make it standard types like SUV, CUV, truck, etc
*   Model has a very poor data quality but one of the important feature of the data. Applied possible transformation to fix model column
*   Fill 'Unknown' for missing values of type, paint_color, VIN, drive
*   Apply ordinal encoding for condition, title_status, drive from worst to best
*   Apply label encoding to model, manufacturer, state so that it can be used in the regression models


Visualization

**Top 10 car sales by manufacturer, year, model**
![alt text](/images/top_10_selling.png)

**Total sales by condition, cylinders, title_status, type, fuel, transmission, state**

![alt text](/images/total_sales.png)

**Average price of sold car by condition, cylinders, title_status, type, fuel, transmission, state**

![alt text](/images/average_price.png)

**Correlation Matrix for features**

![alt text](/images/correlation_matrix.png)

Conclusion from the visualization and correlation matrix;
*   Ford sells the most followed by Chevrolet and toyota. Model data is very poor but initial transformation indiactes that the trucks like silverado, f150, laramie, sierra are resold more than sedan and SUV. There is an upside sale for 2018, 2017 cars but doesn't indicate a lot more about the behavior.
*   Buyers prefer preowned vehicles in excellent and good condition more than others. 4,6,8 cylinders sell more than others. Clean title has a better sale. Sedan and SUV are more preferred. Gas takes the lead in fuel category. Auto transmission is way more preferred by the buyers. Resale is more in CA compared to any other state.
*   average prices are higher for electric cars.
*   Correlation matric shows that price is positively correlated to year, cylinders, drive and negatively correlated to odometer. That means higher the odometer reading lower the prices.

### **Modeling**  

**Results from RandomForestRegressor and XGBRegressor**

After running the RandomforestRegressor and XGBRegressor and comparing the results of both the model it is eveident that prices is mainly controlled by year, drive, odometer reading and model. The results also show that cylinders are an important feature but the column has 150K+ missing values so we cannot deterministically say that it is contributing to the price.

![alt text](/images/randomforest_and_xgb.png)

**Results from Linear, Reidge, Lasso and ElasticNet Regression models**

Results from the 4 models are very consistent with each other and the results indiacte that higher odometer reading and conditions negatively impact the sale price of the car. Year, drive, title, model are most important feature for the prices of preowned cars. 

![alt text](/images/linear_ridge.png)

### **Modeling**  
After running multiple visualization and models we can conclude on this ask from the client. From the results of RandomForestRegressor and XGBRegressor and comparing the results as well as Linear, Ridge, Lasso and ElasticNet models it can be concluded that **Year, drive, odometer, title and model** of the car play an important role in **determining the price of the car**.

# Copyright (c) Khushboo Chandra.
