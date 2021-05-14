# DSI_Capstone

## **Problem Statement**
Cooking is how we survive but a lot of people are either intimidated or just don't know where to start.  We're going to fix this.  Using a data science approach I will create a recommendation system taking into account either current on-hand ingredients or past recipes that have been made.  At the end of this process we will have that base for a content based recommendation system that will provide recipes from a current data frame.


## **Executive Summary**
Using data attained from Kaggle I attempted to create a recommender system as well as running an unsupervised learning model on the data to further pair down the data.  Unsupervised learning was ineffective on this data set but this would be something to look at in the future with it being made potentially stronger by PCA or other feature engineering.  Best results with clustering were still heavily skewed into one category.  After taking a look at this I moved forward with recommendation system because at this point, especially with no users data yet, accurate clusters aren't necessarily a make or break item.  By vectorizing the data (descriptions and ingredients seperately) and then finding the cosine similarities we can compare recipes and get recommendations in this way.  Further work can be done to extract features to eventually fit into a neural network model and I would also like to explore feature embedding to make the predictions stronger.   


## **Data and Observations**

* Data Source:  [Kaggle Data Source](https://www.kaggle.com/shuyangli94/food-com-recipes-and-user-interactions?select=RAW_interactions.csv)

* Cleaning: Data was clean in the sense that it had a uniform format to it but there were some aspects that needed to be changed and updated.  Initially the nutrition information was all in the same column, this made it hard to read so these things were split into their own columns. With 'minutes'

* Observations: A couple of things that I noticed while taking a look at the data.  First, 

* Dictionary:

| Name | Data Type | Description |
|-|-|-|
| Name | string | name of recipe |
| Minutes | integer | Duration of the cooking recipe |
| Tags| string, list | popular categories helping to identify the recipe |
| n_steps | integer | total number of steps in the recipe |
| steps | string, list | the actual steps to completing the recipe |
| description | string | written out subjective description of dish |
| ingredients | string, list | list of specific items needed to complete the dish |
| n_ingredients | integer | total number of individual ingredients |
| calories | float | caloric total for the dish |
| tot_fat | float | total amount in grams |
| protein | float | total amount in grams  |

## **Methods**
* Methods:  For models I focused on clustering, this ideally would create smaller subsets of the data that would have better results when asked for recommendations.  I used DBSCAN as well as KMeans to finds this data.  Modelling was not strong for either case.  DBSCAN had a silhouette score of -0.26826 and this produced 20+ clusters, while KMeans scored better (0.5336) but between the 5 clusters being trained on 20,000 rows, 11,000 of them were classified into one cluster. By its nature cooking is very subjective as are recommendation systems so the lack of clear clustering is acceptable.  Unsurprisingly, the way that food is written about and the ingredients used are fairly common across the board and at the end of the day it is the method’s being used to cook that really change your product. We don't necessarily need this to have good results. Moving on from this I started down the path to get cosine similarities for my system.  I used 2 different vectorizers for this CountVectorizer and TfidfVectorizer.  CountVectorizer was used on ingredients because the order doesn't really matter.  TfidfVectorizer was used on the description data because context of the words definitely matters.  Description returns strange results and is not as effective as ingredients which returns pretty accurate and related results.  In addition to this I used a function to check available ingredients afgainst current recipes and bring back a recommendation.  On top of the ingredient list the user can specify how many of the available ingredients need to be included in the new recipe's ingredient list.

## **Outcome**
* Using the recommender system I was able to get some reasonable results by inputting a list of ingredients and then with the output recipe this could be used with the cosine similarity functions to further return related recipes.  This is not a finished model but is effective if one were to, for example, be planning a date night meal.  Satisfaction with the courses might vary but the overall result is that related recipes are being output.


## **Future Plans**

* Use embedding to link results and feed into a neural net.  This will allow us to pass in more generalized descriptions or ingredient lists and have the network learn the relationships.  This will contribute to better recommendations.  
* Classification through both PCA and feature engineering to pull out recipe types.  This would make the recommender able to specify things like appetizer, entree, soup, salad, and the like.  
* Deploying a streamlit app to make available outside of the JupyterNotebook.
