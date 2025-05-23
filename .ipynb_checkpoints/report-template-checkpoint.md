# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Alexandre Knihar

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
I didn’t encounter any unexpected issues when submitting my predictions, as the notebook instructions ensured that I set any negative predicted values to zero. This step was important because Kaggle would reject submissions containing negative values for the count. As a result, my output was already in the correct format and ready for submission.

### What was the top ranked model that performed?
The top ranked model in my initial training was a WeightedEnsemble model created by AutoGluon, which combines predictions from multiple base models (such as LightGBM, Random Forest, and NeuralNet). This ensemble approach outperformed any single base model, as shown in the leaderboard output from AutoGluon.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
Before conducting the exploratory plots, I engineered new features by splitting the datetime column into “hour,” “month,” and “day of week” to help the model capture time-based trends. The visualizations that followed confirmed the value of this approach. Demand for bikes peaked sharply during commuting hours in the morning and late afternoon, and was much lower during nighttime. The monthly and seasonal plots showed that rentals were highest in the summer and lowest in winter, highlighting strong seasonal effects. Demand was relatively stable throughout the week, with only a slight drop on Sundays. These patterns justified the decision to add these time-related features, as they correspond to real fluctuations in bike usage and help to improve the model’s ability to predict demand.

### How much better did your model preform after adding additional features and why do you think that is?
After adding the additional time-based features, my model’s performance improved significantly. The validation RMSE decreased from 53.1 to 30.3. This improvement is likely because features like “hour,” “month,” and “day of week” allowed the model to recognize important temporal patterns in bike usage, such as daily commute times and seasonal trends. By giving the model more relevant information about when rentals occur, it was better able to capture the factors driving demand, leading to more accurate predictions.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Although hyperparameter tuning did not lead to further improvement in the validation RMSE (the RMSE increased slightly from 30.36 to 32.79), my Kaggle score improved from 0.62767 to 0.52294. This suggests that after Hyperparameter optimization, the model was better able to generalize to the test set, even if it did not achieve the best score on the validation data. Tuning the hyperparameters allowed the model to adapt its complexity and fitting process, which ultimately led to better performance on the competition leaderboard.

### If you were given more time with this dataset, where do you think you would spend more time?
If I had more time to work with this dataset, I would focus on more advanced feature engineering, such as incorporating weather interactions,  or exploring holiday effects in more detail. I would also try additional hyperparameter optimization with a larger search space and experiment with more complex ensembling techniques. 

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|None|None|None|1.80057|
|add_features|None|None|None|0.62767|
|hpo|num_boost_round: 100-500|num_leaves: 25-64|extra_trees: True|0.52294|

Note: The exact best hyperparameter values for the HPO model are not shown because AutoGluon’s API does not provide direct access to the final fitted hyperparameters for individual models within bagging and stacking ensembles. Instead, I have listed the hyperparameter ranges that were explored during tuning.

### Create a line plot showing the top model score for the three (or more) training runs during the project.


![model_train_score.png](model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.


![model_test_score.png](model_test_score.png)

## Summary
In this project, I applied AutoGluon to forecast bike sharing demand using a real-world Kaggle dataset. By first adding relevant time-based features and then tuning model hyperparameters, I was able to significantly improve my model’s performance, as reflected by the improved public leaderboard score. My analysis highlighted the importance of feature engineering. Particularly extracting “hour,” “month,” and “day of week” from the datetime column, as well as the importance of systematic hyperparameter optimization. Although the validation RMSE did not always correspond exactly to improvements on the test set, the final model achieved strong results on Kaggle. This process reinforced the importance of careful data analysis, targeted feature engineering, and robust model selection in a practical machine learning workflow.
