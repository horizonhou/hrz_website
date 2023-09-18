---
title: "Predicting Box Office Failures with LLM"
date: 2023-05-26T23:15:00+07:00
slug: Machine-Learning, LLM
category: projects
summary:
description:
cover:
  image: "covers/BoxOffice.jpg"
  alt:
  caption:
  relative: true
showtoc: true
draft: false
author: ["Ruize Hou", "Hongjiao Zhang", "Jiao Wang", "Zijin Gao", "Curtis Chen"]
---

---
# Abstract
This report presents a comprehensive data science study designed to
predict box office performance of movies, leveraging an integrated
analysis of three extensive datasets: MovieLens 25M, IMDb
Non-commericial, and Kaggle Movie Revenue. These datasets collectively
provide a wealth of movie features, including ratings, revenue,
metadata, and audience preferences. The study primarily aims to
identify the key variables that influence a movie's box office success
or failure, seeking to unravel the potential impact of a movie's
budget on its box office performance, the likelihood of certain genres
failing at the box office, and the strategies that can be optimized to
maximize returns on movie production investments. We also delve into
the role of marketing expenses in shaping a movie's box office
performance, providing actionable insights that can help refine and
enhance the effectiveness of marketing campaigns. The datasets used in
this project are extensive, with the MovieLens dataset encompassing 25
million ratings applied to 62,000 movies by 162,000 users, the IMDb
dataset providing a vast trove of movie data, and the Kaggle Revenue
dataset offering 26 million ratings from 270,000 users for 45,000
movies. Rigorous data cleaning techniques were applied to ensure the
integrity and accuracy of the datasets. For our prediction models, we
utilized a range of machine learning algorithms, including Random
Forest, Logistic Regression, XGBoost, and Gradient Boosted Trees,
achieving a testing accuracy of around 0.92. The implications of this
research are substantial for the film industry. By offering predictive
models and insights that can help mitigate the risk of box office
failure, optimize both production and marketing strategies, and
enhance the return on investment for movie projects, this study
contributes significantly to understanding audience preferences and
establishing a pathway towards increased profitability in the movie
industry.

# Introduction {#sec:intro}

In an industry where the thin line between success and failure often
lies in the delicate balance of creativity, budgeting, and marketing,
understanding the dynamics of box office performance is crucial. As a
group of students with a shared passion for film and movies, we were
driven to use our data science skills to delve into the intriguing
complexities of the film industry. The motivation behind our study was
not just academic curiosity; we sought to contribute tangible insights
that could inform and influence the industry's approach to production
and investment strategies.

Our project aims to predict box office success by analyzing an extensive
array of movie features and audience preferences. To achieve this, we
have combined three expansive datasets: MovieLens, IMDb, and Kaggle
Revenue. These datasets collectively provide a wealth of data, including
ratings, revenue, and metadata for thousands of movies. Specifically,
the MovieLens dataset comprises 25 million ratings applied to 62,000
movies by 162,000 users, the IMDb dataset offers a comprehensive array
of movie data, and the Kaggle Revenue dataset presents 26 million
ratings from 270,000 users for 45,000 movies.

The scope of our study involves identifying the key variables that
influence a movie's box office performance. We intend to unravel
questions like the impact of a movie's budget on its box office
performance, the susceptibility of certain genres to failure, and the
role of marketing expenses in shaping a movie's financial success. Our
goal is not only to provide predictive models for box office success but
also to generate insights that can help optimize production and
marketing strategies.

By merging our passion for the film industry with our expertise in data
science, we aim to shed light on the factors that contribute to a
movie's success or failure at the box office. We believe that our
research will serve as a valuable resource for film studios and
investors, providing them with data-driven insights to optimize their
decisions and investments in the movie industry.

# Related Work {#sec:formatting}

In this section, we summarize some work that is most relevant to ours.

Our study builds upon a rich body of academic research that has applied
data science to the film industry. A seminal resource for our work was
the MovieLens dataset, the creation and application of which was
discussed in Harper and Konstan's \"The MovieLens Datasets: History and
Context\" [@harper2015movielens]. This dataset, encompassing 25 million
ratings applied to 62,000 movies, has proven invaluable in numerous
studies for understanding audience preferences and movie ratings.

Simultaneously, sentiment analysis has emerged as a significant tool in
this field. Asano and Motomura's \"Large-Scale Movie Review Dataset for
Sentiment Analysis\" [@asano2015large] demonstrates the utility of
sentiment analysis in understanding public opinion about movies, an
approach that complements traditional numerical ratings.

The question of whether critical reviews influence box office success
has also been examined. Maltby's study \"Predicting box-office success:
do critical reviews really matter?\" [@maltby2000predicting] provided
insights into the interplay between critical opinions and audience
reception, an important factor in determining a movie's financial
performance.

In recent years, machine learning has been increasingly leveraged to
predict box office performance. Narayanan et al.'s study
[@narayanan2019box] and Subramaniyaswamy et al.'s research
[@2017subramaniyaswamy] both employed machine learning algorithms to
predict box office success, laying the groundwork for our own predictive
models. These models have been further refined by studies such as \"A
Machine Learning Approach to Predict Movie Revenue Based on Pre-Released
Movie Metadata\" [@ML2020] and \"Finding Nemo: Predicting Movie
Performances by Machine Learning Methods\" [@Nemo2020], which emphasize
the predictive power of pre-released movie metadata.

Kim et al.'s study [@SNS2015] and Shen's research [@Shen2020] took a
different approach by integrating social media data into their machine
learning models. They demonstrated that the sentiment expressed on
social media platforms could be a valuable predictor of box office
performance, a finding that underscores the importance of considering a
wide range of data sources in our study.

Our research aligns with and extends upon a significant body of existing
academic work. We aspire to contribute to this ongoing dialogue by
providing new insights into the predictors of box office success and
exploring the potential for data science to optimize film industry
practices.

# Dataset {#sec:formatting}

Our study's dataset is a robust combination of three widely-recognized
sources, namely the MovieLens dataset, the IMDb dataset, and the Revenue
dataset from Kaggle. These datasets collectively present a comprehensive
array of movie features essential for our research.

The MovieLens dataset, developed by the GroupLens research lab at the
University of Minnesota, is an extensive resource that contains 25
million ratings and one million tag applications. These ratings and tags
have been applied to a total of 62,000 movies by an active user base of
162,000 individuals. This dataset allows us to access a vast and diverse
range of user opinions on a large collection of movies.

IMDb is a renowned online database that provides a plethora of
information about films, television programs, and video games, including
cast, production crew, plot summaries, and ratings. This dataset
provides us with a broad range of movie metadata, offering deeper
insights into the features that might influence a movie's box office
performance.

Lastly, the Revenue dataset from Kaggle includes 26 million ratings from
270,000 users for 45,000 movies, is a rich source of revenue data. It
allows us to study the relationship between various movie features and
their box office performance.

The combined dataset presents a comprehensive collection of movie
features, ratings, revenue data, and other associated metadata. The
breadth and depth of these datasets provide a strong foundation for our
analysis and predictive modeling in this study.

# Data Preprocessing

Our data-driven exploration began with a comprehensive process of
preparing and understanding our data. Exploratory Data Analysis (EDA)
was a critical part of this process. We examined our data using various
statistical and visualization tools to understand the features and
relationships within our dataset. Our exploration included the creation
of histograms to understand the distribution of our data, boxplots to
identify outliers, and a coefficient matrix to examine the relationships
between variables.

Through outlier analysis, we found that there exists many outliers in
budget and revenue. There are many successful movies that have enormous
investment in production and outstanding performance. However, we didn't
want to remove these outliers because we want to take all types of
movie, no matter it is big production or not, into consideration. We
will mitigate the outlier effect by making our target variable binary
and also through mitigating the imbalance of the data.

The insights from our EDA guided our data cleaning process. We
identified and addressed anomalies such as duplicate entries and missing
data. We also did our best to fill in gaps in our dataset where the data
was numerical. For example, there were missing 'budget' values, which we
estimated using other features like 'year' and 'genre', or using online
resources to impute missing values. Figure [4] is the
data without preprocessing and figure [3] is the data after removing entries with
missing budgets, which are entries with budget of 0 in the data.

![image1](/images/MoviePrediction/eda1.png)

We also acknowledged the potential for bias in our dataset. The IMDb
dataset may favor specific movie types or genres, and this had to be
addressed to ensure fair analysis. We mitigated this by integrating box
office revenue data into our analysis to complement the IMDb data.
Resolving class imbalance can begin with resampling techniques. This
process involves adjusting the dataset by either oversampling the
minority class, which duplicates instances from the minority class, or
undersampling the majority class by removing instances. The goal is to
achieve a balanced class distribution, which can improve the performance
of our model.

Modifying the learning algorithms to increase their sensitivity to the
minority class is also an effective strategy. This can involve adjusting
the decision threshold in models like logistic regression or utilizing
learning algorithms specifically designed to handle imbalanced datasets,
such as Gradient Boosted Classifiers. These modifications can help the
model pay more attention to the minority class and thus improve its
ability to make accurate predictions.

Finally, when dealing with imbalanced datasets, it's crucial to use
appropriate evaluation metrics. Accuracy might not provide a fair
assessment of the model's performance in such cases. Instead, metrics
such as precision, recall, F1-score, or the Area Under the Receiver
Operating Characteristic Curve (AUROC) can provide a more comprehensive
understanding of the model's performance, considering both the majority
and minority classes. By focusing on these metrics, we can better
evaluate and improve our model's performance on imbalanced datasets.

![image1](/images/MoviePrediction/figure5.png)
![image1](/images/MoviePrediction/figure6.png)

The final phase of our data preparation was feature engineering. We
identified ways to create new variables from the existing data that
could better inform our model. These included user ratings and
demographics, temporal trends, and movie metadata such as title, genre,
release year, director/actor popularity, and the budget-to-revenue
ratio. In the feature engineering step, we manipulated our data to
create new, potentially more informative features, aiming to enhance the
performance of our models. We focused primarily on profit-related
features, as they offer valuable insights into a movie's financial
success.

One key feature genre is stored in json form which is not available for
analysis on the first hand. We used techniques to deal with json type of
data and converted those genres into one-hot-encoding due to its
categorical nature.

We found that NA value in variable belongs-to-collection means that the
movie does not belong to any collections. We believed it is a
informative feature, so we turned it into a binary variable
if-in-collection that takes value 1 and 0. Value 1 means that the movies
belongs to a collection, and 0 means that the movie does not belong to
any collection. In the future, we could collect the popularity of the
collections which is known prior to the release of the new movie, and
then add the interaction of the collection popularity with
if-in-collection as a new feature in our model.

We constructed the Return on Investment (ROI) feature by subtracting the
movie's budget from the revenue and then dividing the result by the
budget. This feature provides a measure of the profitability of the
movie relative to its initial investment. It essentially tells us how
much return we get for each dollar spent on the movie's production.

Next, we created the 'box_office_failure_roi' feature, a binary variable
that uses the ROI to categorize movies as successful or unsuccessful. If
a movie has a negative ROI, indicating that it made less money than was
spent to produce it, we assigned a value of 1, signifying a box office
failure. Conversely, if a movie has a non-negative ROI, suggesting that
it broke even or made a profit, we assigned it a value of 0, marking it
as a box office success.

Another feature we engineered was 'Profitability', a binary indicator
that directly compares a movie's revenue to its budget. If a movie's
revenue exceeds its budget, indicating a profit, we assigned a flat
value of 1; if not, we assigned a value of 0. This feature gives a
straightforward measure of whether a movie made a profit or not.

We also created the 'Popularity to Budget' feature by dividing the
popularity of a movie by its budget. This feature gives an idea of how
popular a movie is relative to the amount spent on it. A high value for
this feature would suggest that the movie was able to achieve
significant popularity despite a relatively low budget, whereas a low
value might indicate that even a high budget was not able to guarantee
popularity. We also one-hot encoded the categorical features, such as
language, and only kept entries of entries with more than 30
observations to remove outliers. Through these steps, we aimed to better
capture the underlying patterns and relationships in our data, providing
our models with the necessary information to make accurate predictions.

![image1](/images/MoviePrediction/llm.png)

In order to utilize more features we have in hand, we wanted to convert
some text relating to the success of the movie into usable feature.
Thanks to the innovation in Large Language Model (LLM), we had it as a
powerful tool to do sentiment analysis on the overview of each movie. We
used the OpenAI API to access the GPT 3.5 model, did prompt engineering
which we tested several prompts and finally chose one that provided the
best output, and then cleaned the output to analyzable format. We
combine the overview of each movie with our prompt that asked the GPT
3.5 model to rate whether the movie overview is interesting in a scale
of 0 to 10 (normalized to 0 to 1 later), and then use the GPT 3.5 model
to generate the response. We used it as an additional feature in one of
our three sets of variables later.

# Analysis

In the analysis phase of our study, we adopted a range of predictive
modeling techniques, each aiming to forecast whether a movie would end
up as a box office failure. We utilized logistic regression, random
forests, and gradient boosted classifiers to experiment and test a wide
range of machine learning models that achieve good performance in
similar classification tasks.

Logistic regression offers simplicity and interpretability, outputting
results that can be understood in terms of probabilities. Random
forests, on the other hand, is an ensemble method offering greater
robustness and accuracy through decision tree aggregation, handling
high-dimensionality and potential overfitting effectively. We also used
XGBoost (Extreme Gradient Boosting), which is a sophisticated machine
learning algorithm known for its speed, accuracy, and efficiency. It's
widely used for various predictive tasks including classification and
regression and provides parallel processing, effective handling of
missing values, and a regularization parameter to prevent overfitting,
all of which contribute to its strong performance in generating highly
accurate models.

In hopes of our models generalizing well to new data, we took steps to
ensure they were not merely overfitting to our current dataset. We
implemented feature scaling and normalization to treat all our variables
on an even playing field and reduce the chance of higher-magnitude
features unduly influencing the model. Cross-validation, a crucial step
in our process, was used to gauge how well our model would perform on
unseen data. By dividing our dataset into multiple subsets and training
our model on various combinations of these subsets, we could gain
insight into our model's performance variance and its capability to
generalize. Regularization was another technique we utilized to prevent
overfitting. By adding a penalty term to the loss function, we could
keep the weights of our model's features small, thus reducing model
complexity and improving generalizability.

Lastly, evaluating the runtime of each model was crucial in our
selection process. While accuracy is vital, a model that takes too long
to run can be impractical, so we considered the trade-off between model
complexity and runtime.

# Results

Here we are predicting box office failure ROI using only meta data. The
Random Forest model had the highest training accuracy (0.77) and test
accuracy (0.70). The XGBoost model, however, had slightly better F1 and
F1macro scores, indicating a better balance between precision and
recall.

![image1](/images/MoviePrediction/table1.png)

This table introduces GPT ratings as an additional feature in predicting
box office failure ROI. Interestingly, all the models show a decreased
test accuracy and F1 score compared to their performance in Table 1.
This could imply that the GPT rating isn't providing a significant
benefit to the model's predictive power. The Random Forest model still
performs the best in terms of training accuracy, but the XGBoost model
surpasses it slightly on the F1 and F1 macro average scores.

![image1](/images/MoviePrediction/table2.png)

In this table, post-release data is added to the meta data for
predicting box office failure ROI. Here, we see a considerable
improvement in all models' performance metrics. The Random Forest and
XGBoost models perform particularly well, with perfect training accuracy
and very high test accuracy and F1 scores. The Cross-Validation (CV)
score is also quite high for all models, showing their ability to
generalize well.

![image1](/images/MoviePrediction/table3.png)

This table focuses on predicting profitability using meta data and
post-release data. Here, we see a significant drop in the F1 score
compared to Table 3, despite maintaining high training and testing
accuracies. This could imply that the models are not good at balancing
precision and recall in this task. The Random Forest and XGBoost models
are again the best performers, but the low F1 scores indicate a need for
model improvement or feature selection refinement.

![image1](/images/MoviePrediction/table4.png)

The Random Forest and XGBoost models generally outperformed the Logistic
Regression model. However, their performances varied depending on the
task and the features used. It also seems that post-release data
significantly improves the models' predictive capabilities. The GPT
ratings, on the other hand, did not seem to provide significant benefit.
These insights could help refine future models and feature selections
for better predictive performance.

In the above analysis, the models using post-release data provided much
higher performance than models using meta data only or meta data with
GPT ratings. While this highlights the potential impact and value of
post-release data in improving prediction accuracy, it also raises a
critical practical challenge as this kind of data is typically not
available until after a movie has been released, which is often too late
to inform many important decisions about marketing, distribution, and
other strategies aimed at maximizing box office success. Therefore,
while including post-release data significantly improved the models'
predictive performance, such models are not practically useful in most
real-world scenarios where predictions are needed before the movie
release.

Given the limitations of using post-release data, focusing on improving
predictive performance with only pre-release data (like meta data and
GPT ratings) becomes essential. The comparison between Tables 1 and 2
shows that the addition of GPT ratings did not enhance the models'
performance. This suggests that, at least in this specific case, the GPT
ratings did not add much value to the predictive power derived from the
meta data. More in-depth investigation is needed to understand why GPT
ratings did not improve performance - it could be due to the quality or
relevance of the ratings, or the way they are being used by the models.
Further exploration of other pre-release data, or more nuanced ways of
utilizing the GPT ratings, might enhance the models' predictive power in
practical scenarios where only pre-release data is available.

The Random Forest and XGBoost models consistently outperformed the
Logistic Regression model across all scenarios, which suggests that more
complex, non-linear models may be better suited to capturing the nuances
of box office success. However, it's important to note that all models
struggled with the profitability prediction task, as seen in Table 4,
indicating that this is a challenging problem that may require more
sophisticated modeling approaches or a different selection of features.
While these models show promise, the practical applicability of
predictive models for box office success depends heavily on the timing
and availability of data, as well as on the complexity of the problem
being addressed. Further work is needed to improve performance using
only pre-release data, which is what would be available in real-world
forecasting scenarios.

# Conclusion {#sec:formatting}

In conclusion, our study as film-interested students provided an
intriguing exploration into the utility of machine learning models for
predicting box office performance and profitability. The most important
findings from our study suggest that the use of post-release data
significantly improves the prediction of box office failures based on
return on investment; however, this kind of data is typically not
available until after a movie has been released, which is often too late
to inform many important decisions about marketing, distribution, and
other strategies aimed at maximizing box office success.. Models such as
Random Forest and XGBoost demonstrated promising results with high
training, testing accuracy, and F1 scores.

Additionally, our research underscored the importance of carefully
managing and processing data in the context of a real-world application.
We confronted and navigated multiple challenges, including dealing with
missing values, joining multiple large datasets, and understanding the
context of the data, all of which contributed to our practical learning
experience. This hands-on experience not only deepened our understanding
of the complexities of data science but also provided us valuable
insights into the film industry.

Despite the challenges encountered, our collective interest in film and
cinema motivated us, making the project both fascinating and rewarding.
This project provides insights into the potential of machine learning in
the film industry, and we hope our findings and experiences can serve as
a stepping stone for other students and researchers venturing into this
exciting intersection of data science and film.