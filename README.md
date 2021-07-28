# Google Apps Analysis


PROJECT DESCRIPTION 

Project Purpose:
Analyzing Google Apps’ Rating, Price, Reviews, installs against their respective categories, and they are: art and design, auto and vehicles, beauty, books and reference, business, comics, communication, dating, education, entertainment, events, finance, food and drink, health and fitness, house and home, libraries and demo, lifestyle, game, family, medical, social, shopping, photography, sports, travel and local, tools, personalization, productivity, parenting, weather, video players,  news and magazines, maps and navigation.


Data Source:
Google Play Store Apps
https://www.kaggle.com/lava18/google-play-store-apps 

PORJECT PROCESS

Importing & Exploring:
-	Import suicide rates dataset
-	Explore the dataset
   o	see the first 5 rows (head())
   o	see the number of columns & rows (shape)
   o	see the statistical summary (describe())
   o	Check the missing values (info())
   o	create a boxplot & histogram to inspect the distribution of the data and inspect the outliers 
   
   ![Boxplot 1](https://user-images.githubusercontent.com/71211875/127317739-5845dd5a-4630-45b5-ad2c-dd1753ed993c.GIF)
   
   ![Hist !](https://user-images.githubusercontent.com/71211875/127317770-6677474b-9a7c-4525-b041-420aa0a930b3.GIF)

As it is shown in the boxplot, there is an outlier value reflects a rating score approximately equals to 19, and this rating score is not true (Rating score in this case is from 0 to 5)


Data Cleaning 
1-	Inspecting Outliers 
Inspecting the outliers value by calling google_data[google_data.Rating > 5]  and droping the outliers

![Boxplot 2](https://user-images.githubusercontent.com/71211875/127317874-aa509c2d-c68b-4b46-a92f-007d796b94b0.GIF)

![Hist 2 with Comment](https://user-images.githubusercontent.com/71211875/127317889-e4c64082-f989-4e6e-a7da-60e4cf11e099.GIF)


2-	Removing 90% Empty Rows  
Create a threshold to help in dropping 90% empty rows, and use the variable to drop the 90% empty rows 

'''threshold = len(google_data)*0.1 #10% of the rows (10840)'''


Data Imputation & Manipulation 

1-	Filling the Missing Values in Rating Column 

Define a function that will impute median for the missing values and then apply it to Rating column 

'''def impute_median(series):
    return series.fillna(series.median()) '''
    
2-	Filling the Missing Values of the Categorical Type Column

Fill the missing values in Type, Current Ver, Andorid Ver Columns (because they are categorical) with mode

3-	Converting Columns into Numerical Values

Convert Price, Reviews, and Installs columns into numerical values 
After finishing the imputation and manipulation, take a look at the dataset using head() & describe()


Data Visualization 

The point is to visualize & analyze rating, price, reviews, and installs against their respective categories. To do so, we need to group by category and aggregate the values by mean for Rating, Reviews, & Installs and by sum for Price.


'''grp = google_data.groupby('Category')
Rating = grp['Rating'].agg(np.mean)
Price = grp['Price'].agg(np.sum)
Reviews = grp['Reviews'].agg(np.mean)
Installs = grp["Installs"].agg(np.mean)'''

After grouping, each variable was plotted against the respective category as it is shown below

![Category wise Installs](https://user-images.githubusercontent.com/71211875/127318132-9cd616c2-f3ea-4f53-9cd1-f80128d3e083.GIF)
![Category wise Price](https://user-images.githubusercontent.com/71211875/127318135-593c5255-0a9b-4b91-8ef7-cca7a6e5b217.GIF)
![Category wise Rating](https://user-images.githubusercontent.com/71211875/127318137-28f0aee6-14bd-4a44-9bad-6aec4ca81a65.GIF)
![Category wise Reviews](https://user-images.githubusercontent.com/71211875/127318138-77869ba9-2e45-4d24-9c2a-95c275af0e53.GIF)

RESULTS
According to the analysis: 
Education & Event categories have the highest rating and Dating category has the lowest rating.
Finance, Family, Lifestyle, and Medical Categories score the highest in terms of price respectively.
Communication, Social & Game categories score the highest number of reviews.
Communication category has the highest number of installs.



