# BTS_Aviation_Delay_Project

## Introduction

As the world becomes more and more interconnected, air travel becomes an ever more important means of transit for the United States. Despite this importance, U.S. flight delays have become more numerous and unpredictable, exacerbated by the recent pandemics, supply chain disruptions, and climate change. In order to help guide America's future aviation, it is essential that we be able to monitor and predict flight delays. And in order to do this, scienctists and statisticians need access to a large, high quality collection of relevant data.

Hoping to address this need, the Bureau of Transportation Statistics, or BTS, has maintained an up-to-date dataset of information on every flight in America that it believes will help researchers and professionals track and predict flight delays. This dataset of [Carrier On-Time Performance](https://www.transtats.bts.gov/tables.asp?qo_vq=EFD&QO_anzr=) contains data dating back to 1987 and aims to document all the information that could relevant to those seeking to model flight delays. However, the BTS is always seeking to improve its data collection. A cursory look through this database will reveal the fact that information for each flight is not always collected in a complete state and numerous additional columns of data have been added over the years.

In order to maximize the efficiency of its data collection, the BTS aims to prioritize the most important data columns to ensure that future models are as accurate as possible.

The purpose of this project is to create a predictive model of U.S. flight delays with the BTS dataset and identify the data columns that are most important to the model's predictions to help guide the BTS' future data collection efforts and create the best models of American flight delays possible.

## Data Processing and Modelling

To begin with, the dataset was cleaned of `NaN` values and columns that contained irrelevant, redundant, or post-flight information were removed. Redundant columns were removed to prevent the model attempting to train on highly correlated models and dividing up its weights across each redundant column, making it impossible to detemine the true importance of a given column. Post-flight information was removed to ensure that the model was able to make predictions _before_ a flight had occured.

Afterwards, the model was thoroughly explored to ensure no outliers were present that could mislead the model and the remaining data was scaled down to one order of magnitude and converted into a purely numeric model-friendly format for use in model training.

As the purpose of the models was to identify the most important columns of data and guide improvements to the BTS' dataset, three interpretable models were selected for training: Logistic Regression, Random Forest, and AdaBoost. After optimizing each model's parameters, Logistic Regression showed both the highest accuracy and was the most interpretable.

Despite the use of multiple fine-tuned models and a large quantity of data, even the best model showed a negligible improvement over the baseline, resulting in suspiciously low performance across the board.

## Conclusions

In many cases, models fail to achieve a high level of performance due to insufficient data, insufficient complexity, or excessive complexity. Without enough data to pull from, no model can learn the underlying trends that connect a dataset to its target variable. Similarly, models that are too simple often fail to capture the complexities of real-world patterns and thus fail to find meaningful connections they can use to make predictions while models that ar etoo complex overfit to their data, choosing to memorize it rather than learn from it.

However, none of these issues are likely to be the cause of our models' poor predictive performance. The BTS' dataset is a truly gargantuan collection with billions of data points. Even when restricted to a single year's worth of data, there are millions of rows to pull from when training our model. Given the relative simpliicity of binary classification, it is unlikly that our models lack sufficient data to learn the relationship between the BTS' information and flight delays.

Similarly, our models' results are unlikely to be the result of insufficient or excessive complexity complexity. Both Random Forest and AdaBoost are tree-based models infamous for their potential to balloon in complexity and overfit to their datasets. However, the training accuracy of our models shows equally poor performance to their testing accuracies. In overfit models, training accuracy would far exceed testing accuracy, indicating that the model has attempted to perfectly conform to its tarining data and thus missed the broader patterns it was expected to find in the testing data. The fact that we do not see this indicates that our model's performance cannot be the result of excessive complexity.

From this, we can derive one major insight that the BTS can use to guide the improvement of its data collection. And that is the fact that __there is no meaningful connection between the BTS's data columns and flight delays__.

When training machine learning models, there is always an implicit requirement that the data provided bear some causal or correlated connection to the target that the model is attempting to predict. No one would expect to able to train a model of city traffic on a dataset of movie ratings. If our models are being given ample clean data, are complex enough to capture even the most intricate of relationships, and are not overfitting to their training set, then we can only conclude that the dataset is largely unrelated to the target.

In the case of flight delay prediction, this conclusion is not without precedent.

The majority of academic papers into the causes of flight delays center on one of three major causes: The maintenance and upkeep of the plane and airport, the amount of and rate of change in supply and demand for air travel, and the weather conditions along the flight's route.

Planes or airports that have gone without maintenance for an extended period of time are more likely to experience technical difficulties that delay takeoff. A sudden and unexpected increase in demand for flights can leave airports unable to send out flights on time as they struggle to deal with the fact that a majority of flight are overbooked under the assumption that some passengers will not arrive. And extreme weather conditions can hold back a flight's takeoff, postpone its landing, or change its flight path in ways that delay its arrival.

Despite the importance of these factors, __the BTS' dataset does not include any of these factors in its database of flight delay statistics, not even weather.__

Taking all this into consideration, we can conclude that the BTS should prioritize adding new data such as the date of a plane or origin airport's most recent maintenance, The ratio of traveller to active flights for the given time period, and the anticipated weather conditions during takeoff to its dataset. Doing this would allow future models to incorporate new data that may be more strongly correlated with flight delay and address the dataset's current lack of connection to the very thing its seeking to monitor.