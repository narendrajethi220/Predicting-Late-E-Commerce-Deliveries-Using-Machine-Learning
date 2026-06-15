#### Baseline Model
We have selected Logistic Regression as our baseline model, because it is simple, fast, probabilities, Good baseline and our first goal is not accuracy.
Our first goal is to establish a benchmark.

#### Split,

0 - 91.8% (No late deliveries)
1 - 8.1 % (late deliveries)

So we have to split carefully so that during data splitting, it must be ensures that our training and testing sets maintain the exact same propration of class labels as our original dataset.

- stratify=y : This splits guarantees that exactly the training and testing dataset will be having the exact same proportion of class labels as our original dataset.

#### Evaluation Metrics

The objective of the project is to identify orders that are likely to be delivered late. 
Missing a delayed order means the business loses the opportunity to take prevention action.
Therefore Recall is important because it measures how many actual delayed orders were correctly identified by the model.

1. Accuracy : 0.9189343285129321
2. Precision: 1.0 
- Out of all order predicted as late, how many were actually late?
    - 1/1+0 = 1
3. Recall   : 0.0006389776357827476
- Out of all actually late orders, how many did we find?
    - 1/1+1564 = 0.000639 ~ 0
4. F1 Score : 0.001277139208173691
- How well am I balancing Precision and Recall, One is amazing, one is terrible.
    - F1= 0.001 , This model is bad.
5. ROC AUC  : 0.5847508967601297
- If I randomly pick , "one late order","one on-time order" , what is the probability that my model gives a higher score to the late order.
    - .5847 - chance that a randomly selected delayed order receives a higher probability score than a randomly selected on-time order.
    - Not good, random guessing .50.
    - Model guessing - .58

On printing Confusion matrix:
confusion_matrix(y_test,y_pred)
[[17728     0]
 [ 1564     1]]

Although accuracy is high, model fails to identify delayed orders effectively due to sever class imbalane. Low recall indicates that most delayed deliveries are being misclassified as on-time.

On using class class_weight = 'balanced'
class_weight='balanced' automatically gives more importance to the minority class and less importance to the majority class during training.
It is used when target class is imbalanced, ensuring the model pays sufficient attention to the minority class during training.

Model accuracy decreased but recall increased
Accuracy : 0.5439796817498574
Precision: 0.10060739922694643
Recall   : 0.582108626198083
F1 Score : 0.17156308851224106
ROC AUC  : 0.5838047571538967

confusion_matrix:
array([[9584, 8144],
       [ 654,  911]])

Found 911 delayed orders
Missed 654 delayed orders

As ROC-AUC is .58 (low) means the model struggles to separate classes.

- Logistic Regression serves as a good baseline model but assumes a linear relationship between the predictors and the target. Delivery delays are infulenced by multiple factors such as approval time, purchase timing, and expected delivery duration. 
The relationship may be non linear and rule based.
Decision Trees can capture such complex decision boundaries and feature interactions without requiring explicit feature transformation, making them a suitable next model to evaluate.

Business process data often contains rules,
Weekend AND Long Approval AND Short delivery window.
Feature may interact with each other

# Why Decision Tree?

Logistic Regression achieved high accuracy but struggled to separate delayed and non-delayed orders effectively.
Since delivery delays may depend on non-linear relationships and feature interactions, a Decision Tree model is evaluated as the next candidate.

Without any hyperparameter tuning, I got 

Accuracy:  0.8559581195252164
Precision:  0.13921113689095127
Recall:  0.1563517915309446
F1_Score:  0.1472844430806996
ROC_AUC_Score:  0.5360118465669278

Train Score: 0.9996371552975326
Test Score:  0.8559581195252164

As the difference between the test score and the train score is too high which shows the case of overfitting.
and the result are similar to what we got using logistic regression.

As a part of the next step we will be using hyperparameter tuning to improve the model accuracy.