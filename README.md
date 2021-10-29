# Well-Project

**Overview**

Tanzania is currently facing an issue with water. There are thousands of wells across Tanzania that are a mix of functioning and non-functioning. Through this project, we'll build several models that can predict wells that aren't functioning throughout Tanzania. 

We'll examine what features may be contributing to non-functioning wells, as well as functioning ones, to create a model that can best distinguish between the two and guide efforts for fixing the wells to the right place. 

**Stakeholder **

Through this project we'd like to help the organization, Wells Of Life. They're looking to save the community time. It can take an average of 4-5 hours to find a functioning water source daily. We want to help Wells of Life help get access to clean water. Many of these failing pumps are rudden with disease and it's having a direct impact on life expectancy. Wells of Life is also hoping that the results of this leads to families generating income, spending more time together, or having the time to now attend schools. 

**Business and Data Understanding**

We looked at Tanzania Water Pump Data from Taarifa and the Tanzanian Ministry of Water. There are over 59,000 water pump entries with 40 unique features. Some of these unique features include: 

1. Who funded the well

2. Organization that installed the well

3. GPS coordinates

4. Population around the well

5. Who operates the waterpoint

6. Year the waterpoint was constructed

7. What the water costs

8. The quality of the water

9. The quantity of water

10. The source of the water

In exploring the data, we found that there are over 10,000 wells that have enough water, but aren't functional or need repair. This is where Wells of Life could really make an impact for repair. 

For dried up wells, 97% of them aren't functional. That's 6,089 wells that aren't serving anyone. 

We dropped several columns that had repetitive data or no data like num_private, quantity_group, water_quality, payment, waterpoint_type, and source_type. 

We looked at wells by how they're paid for, as well. Payment type for the wells is categorized as 'Never Pay, Pay Per Bucket, Monthly, On Failure, Annually.' The majority of the free wells (which are a part of the 'Never Pay' category) are non-functional. That's 13,969 Wells that aren't functional. Of those wells, 5895 of them have enough water, but aren't functioning. 

We did some featuring engineering for the columns including the age of the wells. We did this by subtracting the year the waterpoint was constructed by 2021. We filled in any years that showed '0' with the average age of all the wells which came out to 15. We ordinally encoded the quantity column to give each quantity a rank. We set Unknown = 0, Dry = 1, Seasonal = 2, Insufficient = 3, and Enough = 4. 

**Modeling**

We iterated over several different types of models. For our initital train test split, we created a holdout set of 10% to test on once we came to a final model, then we did another train test split that was a 75/25 split. 

For our first simple model, we chose a Decision Tree because with a Decision Tree we wouldn't have to scale any data. We concluded that our Decision Tree was overfit. It scored 100% accuracy on the training data and about 73% accuracy on the test data. 

We then tried a Random Forest Classifier, Logistic Regression, XGBoost, and a KNeighbors Classifier. We created a Pipeline so we could OneHotEncode the columns more rapidly. We also performed a Grid Search that allowed us to tune the hyperparameters to get a more accurate model. 

Our final model was an XGBoost model that gave us the best results on precision without overfitting. 

**Evaluation**

The final XGBoost Model we came to was slightly overfit on the training data but performed well on our unseen holdout data. Out of 5438 wells that were classified as functional only 1180 of them were actually non functional.  A precision score of 78% means that we have a pretty low false positive rate. Test precision score is 4 points higher than our original simple decision tree model, but that model was severely overfit due to there being no max depth limit in that model. 

**Conclusion**

We reccommend that Wells of Life use this model in conjuction with their own resources to identify faulty wells. Our model will still classify some non -functional wells as functional 20% of the time so further investigation will be needed at times.

**Future Work**

We'd like to further engineer more features to give our model better data to make predictions off of. We'd also like to further tune hyperparameters to optimize our model's performance on unseen data. With more time we would like to input climate data into our model to see how climate may be affecting wells, as well. 

Overall, we'd like to continuous gather more information on the wells in Tanzania to add to our data and improve our model.

**How To Navigate the Repository**

- The Data that we used in this project can be found in the data folder.
- All of the jupyter notebooks are located in the notebooks folder and  __final_notebook__ is where the bulk of our analysis can be found.
