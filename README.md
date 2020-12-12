# 3340 Final Project
Eric Reich, Zheng Ge 

# Abstract 

The objective of the study is to understand create linear model that is able to accurately predict the selling price of cars using a set of variables. Data from car.dekho.com was analyzed an fit to a regression model to acertain the validity of the model. The statistically significant variables were discovered and the model was tranformed and then variables were chosen to create a more accurate model. The best model was found to be ln.y = -229.4 + -1.69*Seller type + 0.05212 * Presentation price + 0.1152 * Year + -0.4312 * Desel Fuel type + 0.2009 * Petrol Fuel type + -1.913 * 1 owner + -1.648 * 0 owner, though multiple models seemed to be effective predicors of selling price. It was found that Km driven should be removed from the model chosen. Transmission, fuel type and seller type may be removed without significantly affecting the model, though fuel type and seller type were found to have greater reasoning for being kept in the model. 

# Introduction

Cars are an important part of everyday life. As cost of living increases, the importance of finding affordable cars also increases. Many factors play a role in this including but not limited to age of the car (year), kilometers driven, how much the car is presented as, the number of previous owners, transmision type, fuel type and whether or not a dealer or and individual is selling the car. The Indian webstie Cer.Dekho.com is one such place where one can purchase a car based on a combination of the above variables.

In this analysis, we will use data from Car.Dekho.com to acertain if the above variables play a significant role in the selling price of cars and whether selling price can be predicted via these variables in the form of a linear model. It is expected that year of the car will be a large factor in the model based on my knowledge of the cost of new cars being greater than older cars. KM and owner also seem likely to be connected due to their connections with newness. Newer cars seem less likely to have high km driven as well as number of owners as not enough time would ahve passed for these factors to increase significantly.  I would also imagine that dealers would sell for higher prices, as dealers have dedicated and trained salespeople and also need to mark up cars bought from individuals. Transmission may play a role, as cars of the same make that are automatic sell for more than their manual counterparts on car.dekho.com. CNG and petrol are cheaper fuel sources than diesel, and deisel cars require more upkeep, so it is possible that these cars may sell for more due to the higher demand. Presentation price is also predicted to have a positive affect on selling price, as the percieved price may increase the percieved worth of the car to potential buyers. 
 

# Methods

Three data files, describing car data taken from CarDekho.com were obtained from https://lionbridge.ai/datasets/10-open-datasets-for-linear-regression/.  The data set Car Data.CSV was chosen to analyze. Using R, a new data point was attached to the data frame at point Price = 30, present price =60, year = 2003, KM driven = 300000, fuel type = Petrol, seller type = Individual, transmission = Manual,  owner = 3rd. This data point was chosen to represent an older vehicle with multiple owners and use that sold for a high amount due to it being rare or famous. Fuel type and transmission were chosen to reflect an average car in 2003 and seller type was chosen as individual to represent a car aficionado. This point was chosen in order to crate an unusual point of influence, as influence from an expensive newer car had already been noticed in the data.

To fit the model, N-1 Dummy variable were created for the nonnumeric variables. Two for number of sellers and for fuel type, as well as 1 for seller type and transmission type. A new data set was created using the dummy variables as replacement for their original variables. This data set was then fitted into a linear regression model and summarized using the lm and summary command. The coefficients, R^2, t statistic p values and f statistic p value were analyzed. The model was then checked for multicollinearity. The original indicator variables from the original data set were exchanged with variables replacing factors with 0,1 or 2, to make visualization easier. The pairs command was then used on this changed original data set and the linearity of each variable compared with each other as well as selling price was compared. The vif command was then used to discern a numeric value for collinearity. The residuals, leverage and influence were then reflected upon by using the plot command on the linear model and the resulting graphs analyzed. The H matrix diagonals was used to determine leverage at points greater than 2*p/n. The Influence was found via cooks’ distance at point with values greater than 1.

After finding issues with variation in the residual plot, the data was transformed; first by taking the square root of selling price and then then ln of the selling price and then adding them back into the data frame. the ln transformation was observed to create a better fitting model, so the ln transformation was chosen. Leverage, influence, and a summary of the model were then explored on the transformed model as with the original model. Using the transformed model, a stepwise comparison was done to ascertain which variables should be kept in the model via the step command. All possible combingation models of the transformed data were explored via adjusted R2 to see models that may have equivalent validity using the leaps command. The model produced by the stepwise command was then analyzed via the summary command. 

# Results 

Based on the plots there doesn't seem to be strong evidence of multicolinearity. Though logoically I think there are interactions between km driven, year and number of owners. VIF for model with dummy variables fuel and owner variables appear to be multicolinear, but when dummy variable are combined, multicolinearity dissapears.

A srong correlation between presentation price and selling price was observered (Figure 1). Three points appear to be potential outliers, with one of these points significantly higher presentation price than the rest (figure 1). 


![alt text](000017.png) 

Figure 1  Presentation Price (Indian Lakhs) vs Selling Price (Indian Lakhs)


There appears to be a positive relationship between year and price, though there are two significant outliers at year 2010 and 2003 (figure 2). there appears to be representives of each year at multiples price ranges at an increasing rate as year increases (figure 2) 


![alt text](000019.png)


Figure 2  Year vs Selling Price (Indian Lakhs)


There doesn not appear to be a correlation between Kilometers driven and selling price (figure 3). There are 2 noticable outliers (figure 3)


![alt text](00001b.png)

Figure 3  Kilometers Driven vs Selling Price (Indian Lakhs)


Fuel type CNG appears cheaper than the other fuels but has very few representitives (figure 4). Deisel appers to generally have a higher price than petrol (figure 4)


![alt text](00001d.png)

Figure 4  Fuel Type (0=CNG, 1=Deisel, 2=Petrol) vs Selling Price (Indian Lakhs)


The dealer seller type appears to sell more cars and at a generally higher price than individuals (figure 5). There appears to be 1 significant outlier in individual category (fiugure 5)


![alt text](000021.png)

Figure 5  Seller Type (0=Dealer, 1=Individual) vs Selling Price (Indian Lakhs)


Transmission does not appear to have significant differences between Automatic and Manual, through manual is more concentrated at a lower price with a few outliers, while automatic appears more spread out (figure 6)


![alt text](00001f.png)

Figure 6  Transmission (0=Automatic, 1=Manual) vs Selling Price (Indian Lakhs)


0 owners appears to have higher selling price in general though there are representitives at a wide range (figure 7). 1 owner appears lower and with less data and 3 owners appears to be two extremes with only a few data points (figure 7) 


![alt text](000023.png)

Figure 7  Number of Owners (0= 0 Owners, 1=1 Owner, 2=3 Owners) vs Selling Price (Indian Lakhs)

After the initial fit of the model, high f statistic and low p vaue showed that the variables have significant affect on selling price, given every variable is included in the model. The t test of KM drivin resulted in high p value, implying this variable may be insignificant. Other variables appeared to be significant in the model, based on t test. points 302, 86 and 87 were noticed as influence points. 

A fanning effect is noted, implying non constant variance amongst residual (figure 8).

![alt text](5.png)

Figure 8  Fitted values of full model (y~) vs Residuals

After transforming selling price to ln selling price, ther significance of the variables were similar to the original model, except for transmission. the p value of transmission changed from significant at 0.01 to not significant at 0.618. After transformation, Influence points 86 and 302 no longer appeared at such, though point 87 reamained as an influence point. 

The fanning effect seen in figure 8 is not present, and the data appears more random, though outliers are noticable at point 87 (figure 9). 

![alt text](000008.png)

Figure 9  Fitted values of ln transformed full model vs Residuals

The stepwise model produced formula:

ln.y = -229.4 + -1.69*Seller type + 0.05212 * Presentation price + 0.1152 * Year + -0.4312 * Desel Fuel type + 0.2009 * Petrol Fuel type + -1.913 * 1 owner + -1.648 * 0 owner

Km driven and transmission type were removed from the model. 15 models produced adjusted R^2 of greater than 0.88 (Figure 10). All of these models included year and presentation price (figure 10). The most removed variable in models with high adjusted R^2 was fuel (figure 10).


Adjusted R^2  | Removed Variable
------------- | ----------------
0.889624255   |None 
0.888295188   |Fuel
0.889273061   |Own 
0.889866619   |Tran
0.889959711   |Km
0.888118824   |Fuel/Own
0.888478215   |Fuel/Tran
0.888541218   |Fuel/Km
0.889469980   |Tran/Own
0.890212779   |Km/Tran
0.888257488   |Fuel/Own/Tran 
0.888317091   |Km/Fuel/Own
0.888749946   |Km/Fuel/Tran
0.889787240   |Km/Own/Tran
0.888488099   |Km/Fuel/Own/Tran

Figure 10  Adjusted R^2 compared to Variables removed from model, 


# Conclusion

Based on the stepwise comparison and adjusted R2 of every possible model, presenting price and year are necessary variables within the final model. The models with the highest adjusted R2 all had these variables in the model signifying their importance. The correlation could be seen visually between these two variables and selling type (figure 1; figure 2) This falls in line with what the prediction that these two variable would be significant. Though higher coefficient within the finished model was expected. 

Seller type also had significance in the model. It was found that it costs more to purchase from dealers rather than individuals (figure 5). This would make sense, as dealers often purchase cars from individuals and increase the price to turn a profit. Dealers would also have workers trained to sell, potentially increasing the selling price of vehicles sold. Experience in car sales of individuals seems less likely. 

Km driven did not follow our prediction. The KM variable had high pvalue in the full model and in its transformations. In the stepwise model, Km was removed and was the removed  in many of models with high adjusted R2. It was expected the Km would affect the price significantly, as higher km would mean more use and greater possibility of needing work done to maintain the car. It was also predicted that km driven would correlate with number of owners and year, though this was found to not be the case. This may be due to newer model test cars being sold with high km driven. Based on the data found it would be advisable to remove km driven from the model.

Number of owners was included in the stepwise comparison model. The affect of number of owners on selling price makes sense, as a car with more owners is more likely older. Rare or popular vehicles that may change hands often but are still worth a lot, like the data point introduced, may have effect on predictive ability of this varibale. Based on the models and comparison there seems to be no reason to remove this bvariable from the model.

The price of fuel was the most removed variable in the models with high adjusted R2, though it was used in the stepwise model. It was noticed that Fuel had higher p value even in the final model, so it’s validity in the model is suspect. When exploring CarDekho.com, it was noticed that cars of the same model using diesel were more expensive than those using petrol or CNG. This was also noticed when comparing fuel type and selling price in our data (figure 4). As such including fuel into the model does seems appropriate.

In the stepwise model, transmission was not included, though it was included in some of the models with high adjusted R2. When viewing the summary of the full, transformed model, transmission type p value was not significant implying that it does not play a significant role in the model. Similar to fuel type, when reviewing the differences in price on CarDekho.com it was noticed that automatic cars of the same make and model were more expensive than manual cars. In our data transmission type did not appear to play a role in selling price (figure 6). As such there is precedent to consider models that either include or remove transmission type from the model. 

The affect of influence of point 87 was also analyzed to see if it had any affect on which variables were removed from the model. Point 87 is a land cruiser, which are expensive vehicles. The results implied that point including point 87 resulted in decreased adjusted R^2 but did not affect the variables found within the model. It is recommended that point 87 remain in the model. 

Possible points of error could be found in the lack of variables available for the model. Car prices often reflect the technologies incorporated into the vehicle, while this may be absorbed by the newness of the vehicle in years, it is apparent that cars from the same year may have drastically different add-ons affecting their cost. This model also does not include the brand which would potentially have significant affect on price of cars with similar attributes. Another point of error is my personal lack of car knowledge. The logical arguements used were based on my understanding from looking through Car.Dekho.com, as well as a small amount of previous knowledge. 

In conclusion, the model we found to best fit the data was ln.y = -229.4 + -1.69*Seller type + 0.05212 * Presentation price + 0.1152 * Year + -0.4312 * Desel Fuel type + 0.2009 * Petrol Fuel type + -1.913 * 1 owner + -1.648 * 0 owners. However, based on the data as well as what we know about the price of cars, multiple models seemed to be effective predicors of selling price. 

# Appendix 
[Car Data CSV](https://github.com/eric-reich-dal/3340-Final-Data/blob/main/car%20data.csv)

[Car Data R Markdown](https://github.com/eric-reich-dal/3340-Final-Data/edit/main/Final_cardata.Rmd)

