# Ada-Boost-from-scratch

There are three major properties of Adaboost:

* The base models of the algorithm are weak learners known as Decision Stump.
* All the base models do not have an equal say in the final prediction. The priority given to the model depends on the weight assigned to it.
* The base models are dependent on each other. One base model is created depending upon the errors of the previous model.

![image](https://user-images.githubusercontent.com/94861619/196597746-68073e31-284e-4b05-a98d-78e599ac7d7b.png)

The base models or the weak learners in the case of Adaboost are known as Decision stump. Like Random Forest, Adaboost can be called a forest of stumps. We apply a greedy search algorithm for each feature provides to us and find the best splitting feature and its threshold and we split the entire data based on that. Then this split data is used for predictions. In other words, we are creating a Decision tree with a single node.

![image](https://user-images.githubusercontent.com/94861619/196597807-f2696f12-02ae-4a54-adc3-9be1907e6c22.png)

## The Decision stump is thus a weak learner which means that no matter what the distribution over the training data is, it will always do better than chance when it tries to label the data. Doing better than chance means we are always going to have an error rate which is less than 1/2.

These decision stumps are High Biased High Variance models as they perform weakly on both training and testing data(it is quite obvious when the entire data is being classified based on a single feature). But combining the decision stumps we arrive at a low biased low variance model which works well on both training and testing data.


![image](https://user-images.githubusercontent.com/94861619/196597864-7d53eec9-3479-48aa-b732-483596bbfd42.png)
