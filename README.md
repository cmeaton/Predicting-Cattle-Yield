**Connor Eaton**

Metis - Project Luther - January 25th, 2019



# Predicting beef cattle production

### Why is this important?
Meat production, and particularily beef cattle, is a very interconnected, complex, and expensive process that is crucial to local and global economies. The complexities of its production stem from the fact that before one can raise cattle, one must raise its food. While cattle are natural ruminants, improvements in agricultural processes starting in the mid 20th century have trended towards the production of corn and soy for cattle feed. 

This makes raising and harvesting cattle reliant upon multiple sectors of the global agricultural industry. Despite its complexity and expense, demand for beef cattle has been rising world wide. As a result, I am posing the following questions:

**1.) Can total production of beef per country in a given year can be predicted?**

**2.) If so, what features most strongly predict production? **

Digging into these questions with regression analysis may improve our understanding and optimization of our global food production sytem.

## Gathering Data:

I used multiple data sources for this project, listed below:

*Food and Agriculture Organization.* 
http://www.fao.org/faostat/en/#data

Many .csv files were gathered here and required cleaning and merging. 

    - Total head of cattle (living)
    - Total area in soy production (hectares)
    - Total yield of soy (hectagrams per hectares)
    - Total area in corn production (hectares)
    - Total yield of corn (hectagrams per hectares)
    - Mean weight of harvested cattle (hectagrams per animal)
    - Total number of harvested cattle
    - Total human population in rural areas per country
    - Total human population in urban areas per country

*Weather from the WorldBank.*
http://sdwebx.worldbank.org/climateportal/index.cfm?page=downscaled_data_download&menu=historical

**Selenium was used to scrape this data**. The wesbite was structured with multiple drop down menus with a variety of categories. Once all the desired categories were selected, a few buttons had to be clicked and then a .xls file on the data could be downloaded to your machine. My selenium bot iterated through every drop down menu selection for each country and navigated the necassary pages to download each country-specific .xls file. Much cleaning, as well as using the pycountry library, was necassary to make the data usable in my project.

    - Cumulative precipitation data
    
*Consumption and Production Data from Our World in Data.*
https://ourworldindata.org/meat-and-seafood-production-consumption

Two .csv files were gathered here and required cleaning and merging. 

    - Production of beef.
    - Consumption of beef per capita
    
*GDP data from the WorldBank.*
https://data.worldbank.org/indicator/NY.GDP.MKTP.CD

One .csv files were gathered here and required cleaning and merging. 

    - GDP per country 
    
Upon merging and cleaning all of this data into one dataframe, I had **~2900 observations and 13 features** to work with.

## Preprocessing data:

**Normalization**. Data were in a variety of scales (ex. GDP(10e+8) and hg/animal(800-1200)). I manually adjusted data to be on the same order of magnitude. 

**Removal of outliers**. Outliers were removed for certain variables.

**Categorical features**. Categorical data (country name) was converted to GDP. 

## Feature engineering:

**Log transforms**. The y variable was log transformed so it depicted a more normal distribution. Several features were log transformed to bring residual plots closer to 0.

**Dummy variables** Dummy variables were created for China, Brazil, and India, who all had large effects on the data. Ultimately, India was entirely dropped from the dataset, and the Brazil dummy was dropped from the model. Much future work is needed here and is described later.

## Model construction

**LassoCV and RidgeCV**

To properly build an accurate model, I used cross validation with my training datasplit into 5 folds. I will do this with Lasso and Ridge regression and compare results. Lasso and Ridge regression were used and compared. Both models produced nearly identical metrics (MAE, alpha, and feature coefficents), but Ridge was selected as the r2 was slightly higher.

**Regularization**

Features with coefficents zeroed by my model were eliminated. Features with coefficents close to 0 were removed one by one too see how simple I get the model to be without losing efficacy. The final model had the following features: *cattle_head, soy_area_ha, soy_area_hg/ha, harvest_number,corn_area_ha, corn_hg/ha, urban_pop_e+01, GDP_e+05, supply_g/capita, and China*.

**Final Model**

My final model was trained on the previously untouched test data. The mean absolute error for my model was 13.08  This however is in log form. Calculating it back into its original scale, the MAE was is 479,269. This seems very high, but this is because of the large values in the y data. The range of data fell between 0 and 85,118,939, so this value seems appropriate.

The r2 score was .887, indicating strong predictive power.

## Future Work

There is plenty of opportunity for future work. Idealy, I would like to improve two factors of the project.

**Interaction features**

Creating dummy variables for China, Brazil, and India, and incorporating the China feature in my model, had a positive effect on my model. However, I did not have the time to explore interaction between this feature and others. My residual plot indicates several patterns straying from the cluster around 0, indicating potential for creating interaction features from countries, to improve my model.

**Tranformation of features**

Log transformations had a positive effect in centering residual plots closer to 0 for several plots. However, there were still clear patterns present in the transformed data. One of the patterns was the straying from 0 described above. The other was a tendency for the residuals to be further from 0 as the feature grew larger. I would like to dig further into this issue.
