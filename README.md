# Realty Kings
## Housing data investigation and modeling

<details><summary>Presentables</summary>

[Presentation](./KingCountyMod2_refined.pdf)
[Presentation Video](./Video_presentation.mp4)
[Relevant Blog](https://medium.com/@pchadrow/making-linear-regression-models-in-python-83b736f81266?sk=21383d751eb6ad185ccc64fc8aaf45d5)
</details>

## Purpose
Given housing data for Kings County Seattle, to find price predictors and create a linear regression model capable of predicting potential prices for new homes. This README shall also serve as a genreal outline and explanation of the analysis and devolpment process.

## Synopisis
<details><summary></summary>
An exploration into distances did find some interesting trends that warrant further investigation and after numerous tried and failed attempts at using recursive feature elimination we settled on standard feature selection for our final model. While initially the model seemed promising, further investigation revealed our perceived model score to be artifically high due to the lack of a constant in the model.
</details>

## Analysis
<details><summary></summary>

[Primary data used](./Data/kc_house_data.csv)

### First
Our initial investigation looked at the relationship between house grade and house price [here.](./EDA/Grade_Investigation_EDA.ipynb)

![grade_comparison](/images/grades1.png)
As we can see, there does appear to be a linear relationship with higher house grades and higher sell prices.
____________________________________

### Second
We would then look into the affects of renovation and if more recent renovations had a stronger effect of the sale price of the house

![renovation](/images/renovation.png)
While not a strong relationship with our data, it was interesting to see that there did appear to be a slight trend with more recently renovated homes tending to have a slightly higher possible selling price than those that were renovated longer ago.
_________________________________________

### Third
Due to the lack of information of waterfront properties, we were curious if the houses proximity to water would have an effect on the sale price as well as the houses distance from downtown Seattle, which we investigated [here](./EDA/gathering_distance_and_removing_outliers_EDA.ipynb)

![seattle](/images/seattle.png)
There did indeed appear to be a correlation between the price of a house and its distance from Seattle, with houses that were closer to the city tending to have higher price possibilites.

Next we would determine a few [hotspot locations](./Maps_and_additional_plots/clustered_maps(safe).ipynb) in the water to get a better idea of house prices and their proximity to water.
![map](/images/hotspot_map.png)
Using these few hotspots we would then compare the distance from the closest hotspot to the homes price which would give us...
![hotspot](images/hotspot.png)
Which shows a much stronger relationship between distance from water and house price than distance from Seattle. 
</details>

## Modeling
<details><summary></summary>

We attempted numerous modeling approaches with typically poor results. [Here](./Cleaning_and_Exploration/initial_model_attempt_using_all_features.ipynb) we made our first model using a blanket approach just to see what kind of results we'd get. In terms of R2, our results weren't bad. However, everything else about the model essentially was with numerous instances of multicollinearity and an unacceptable amount of kurtosis.

Next we attempted to use Recursive Feature Elimination [here](./Cleaning_and_Exploration/regressive_feature_elimination_test.ipynb) and [here](./Cleaning_and_Exploration/RFE_Filtered_test.ipynb)

While not all models were saved, numerous attempts were made with various adjustments that all seemed to provide similiar or diminishing results. High amounts of multicollinearity seemed unavoidable with this method.

Eventually we settled on our [final model.](./Cleaning_and_Exploration/Final_Model.ipynb)
At first glance, it looked like we had finally made a great model for our provided data!
![model](./images/result.png)
However, further investigation showed that our test results weren't matching up with each other. Essentially we had forgotten to include a constant in our model as a house will never sell for $0. After including the constant we got a much different result that confirmed what our initial test results were trying to tell us...
![actual](./images/actual_result.png)
</details>

## Conclusion
<details><summary></summary>
Our investigation showed that numerous factors can influence the price of a house. Based off of our main investigations we can recommend rennovating the house before selling to provide a small improvement before selling, and if that renovation provides you with an opportunity to add square footage or additional rooms, it would be wise to do so in order to maximize the potential selling price. In terms of predicting the selling price...at this time we do not recommend using our current model as its proven itself to be widely innaccurate. 
</details>