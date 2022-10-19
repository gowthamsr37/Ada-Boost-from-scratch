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

alpha it the loss function=the weight assigned to the entire model
h(x) is the Decision Stump classifier used in this case.
T is the number of base models used in this ensemble method. The number of base models to be used in AdaBoost depends highly on the data provided to us.
Thus we find out the weighted sum of the classifiers in order to predict the final answer or better to say to find out H(x).

Let's see the step by step process involved here:

Step-1: We first assign the same sample weight to each of the data points. So we apply 1/(number of samples) to all the data points.

![image](https://user-images.githubusercontent.com/94861619/196598959-e267163a-b317-472f-bda3-1488b417fb16.png)



Step-2: We create a decision stump and classify entire data on the basis of the threshold. We select the best feature by a greedy search algorithm and also find the threshold and split the entire data on the basis of that. We identify the best feature by calculating the error. Moreover, we use the weak learner to give us predictions.


Step-3: We find the weight of the entire model. In other words, we find the value of alpha. Experimentally it was found that with the increase of error rate the weight decreases. Plotting a graph we get

![image](https://user-images.githubusercontent.com/94861619/196599015-11ad33dc-baf5-44e3-9f8f-1a432f199a41.png)

Now the error was found out

ε=(misinterpretations)/samples=( Misclassifications)/N
ε=Σ weights of misclassified samples

If the error > 0.5 we have to just flip the decision and error=1-error.(As we have seen that in case of a weak learner the error cannot be greater than 0.5 as the weak learner will always be better than the chance.)

Now we find out the weight(alpha) or loss function of the model using the formula

![image](https://user-images.githubusercontent.com/94861619/196599120-7cc60c7d-6ace-44b5-bceb-ae0efc3af3a5.png)

Step-4: Now we have to update the weight of all the data points. We give more importance to those data points that had been labeled incorrectly and increase their weights. This is done to penalize the errors more than the correct predictions. On the other hand, less importance is given to those data points that were predicted correctly and their weights are decreased according to the formula:

![image](https://user-images.githubusercontent.com/94861619/196599169-7c909f01-8d8c-44a2-88e9-ad7fb2eb09c3.png)


The positive sign is for wrongly predicted data points and the negative sign is for rightly predicted data points. Where omega(i) is the updated weight and omega(i-1) was the previous weight.

Step-5: We normalize the updated weights so that the updated weights lie between 0 and 1 and add up to one by the formula:

w(new)=w(i)/sum of all the weights

We just have to follow the steps mentioned above iteratively for each base model. The number of iterations or the number of base models required depends highly upon the data provided.

If our label is Multiclass, it works in a similar manner to bi-class Adaboost with minor changes. If a multiclass classification involves k classes then instead of being a single variable between {-1,1}, y becomes a k dimensional vector. Similarly, f(x) also outputs a k dimensional vector. So in the error function instead of doing


We take the dot product of y and f(x) vector


Then we try to minimize this new error function.


Note: The source of the content is https://medium.com/swlh/developing-the-right-intuition-for-adaboost-from-scratch-771749f36ce9
