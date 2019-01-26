*Project Luther: Web scraping and linear regression*
​
​
# Predicting annual cattle production.
​
**Connor Eaton**
​
    
## Scope:
Beef cattle is one of the most valuable agricultural commodities traded on a global scale. As it is such a crucial component of local and global economies, being able to predict annual production would be very helpful for variety of stakeholders, from producers, policy makers, and all the way to commodity traders.
​
## Prediction: 
* My model will be predicting annual cattle production.
    
## Data:
* Weather data will be scraped from here: http://sdwebx.worldbank.org/climateportal/index.cfm?page=downscaled_data_download&menu=historical
* Cattle production by country/year will be downloaded from here: http://www.fao.org/faostat/en/#data/QV
        
## Features:
        
| **Feature**       | **Description **         
|:-------------:|:-------------:                                                             | 
| harvest_num (y)          | Total number of harvest animals                             |
| country   | Country   |               |
| cattle_head           | Total number of living cattle               |
| hg/an           | Mean total weight (hectogram/animal    |
| corn_area_ha         | Total hectares of corn  |
| corn_hg/ha           | Total yield of corn (hg/ha)                                                                        |
| soy_area_ha      | Total hectares of soy                                     |
| soy_hg/ha       | Total yield of soy (hg/ha)                                                     |
| rural_pop_10^3          | Rural population (1000)                                             |
| urban_pop_10^3          | Urban population (1000)                                             |
| prec          | annual rainfall                                          |

​
