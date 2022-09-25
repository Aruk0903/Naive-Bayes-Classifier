# Naive-Bayes-Classifier
# What is a Naive Bayes Classifier？
Naive Bayes Classifier is a classification algorithm based on the Bayes' theorem and the class-conditional independence assumption. It is one of the most successful algorithms in solving natural language processing (NLP) problems, especially in spam email filtering.
![image](https://user-images.githubusercontent.com/89111546/192164788-8b6998e1-78de-408a-976c-fb672f3e13d5.png)

# How does a Naive Bayes Classifier work?
For models like Logistic Regression, they are trying to learn the probability of getting a specific class of the output variable Y when given a set of input variables X using functions like the sigmoid function. This type of models are called discriminative learning algorithms.

Naive Bayes Classifer, on the other hand, is a generative learning algorithm. It learns the what are the input variables X like for a given class of output variable Y. Let me show you what this means:
![image](https://user-images.githubusercontent.com/89111546/192165015-e73808cb-ca74-44ce-aaac-942ce5549dac.png)

As demonstrated above, a discriminative algorithm like logistic regression will try to seperate the data points of different classes with a straight line, while a generative algorithm like naive bayes classifier will do the oppoisite.

To formulate this, we have:
![image](https://user-images.githubusercontent.com/89111546/192165025-6dd7aa06-299e-4f81-85e3-3913f31d9f45.png)

As shown above, the naive bayes classifier will first learn the probability that a set of input variables X will occur given a class of output variable Y, that is P(X|Y). It then computes the desired probability P(Y|X) through the bayes' theorem.

# How does it apply the Bayes' Theorem?
# Bayes' Theorem
Bayes' theorem states that the probability of getting Y (output variable) equals to specific class given a specific set of X (input variables) can be computed as the following:
![image](https://user-images.githubusercontent.com/89111546/192165101-e85400ca-3709-4c9e-bbe4-c5dde542b9e5.png)

In the above formula, the posterior probability is the desired output. It is called posterior because it is the adjusted probability calculated based on our initial guess P(Y=c), simple the percentage of the class within the training data. According to the theorem, this posterior probability is directly proportional to the product of the likelihood and prior probability.

The marginial likelihood does not need to be calculated because it is a common denominator for all the probabilities P(Y=c|X) and therefore can be ignored. (We only have to compare the numerators)

However, there is a big problem with finding the likelihood P(X|Y=c): with many input variables X (X1, X2, X3...), there will be a huge number of combinations which makes the calculation of the likelihood nearly impossible. How does the naive bayes classifer deal with this?

# The Class-Conditional Independence Assumption
To find the posterior probability P(X|Y=c), we need to make a big assumption first. This is also the key assumption made by the naive bayes classifier: the class-conditional independence assumption.

Class-conditional independence assumes that the overall likelihood P(X1,X2,X3...|Y) is equal to the product of the individual likelihoods. In other words, it assumes no relationships among the input variables:
![image](https://user-images.githubusercontent.com/89111546/192165129-deae2a8e-7e2c-4544-aa65-adb09dd237d0.png)

This assumption reduces the variance of the naive bayes classifier in the cost of an additional bias. For example, in natural language processing, there are always relationships among the words (input variable) that form a sentence. Therefore, the assumption will introduce a bias that lower the classification performance because of the omitted relationships.

At the mean time, the assumption also decrease the variance of the model. Without the assumption, a large training dataset will be needed to find the likelihood and therefore making the model highly dependent on the training data (high variance).

But how do we actually calculate these probabilities when given a training dataset?

# Multinomial Naive Bayes Classifier
In general, there are 2 different ways to calculate the probabilities needed for the bayes' theorem:

Discrete variables: find the frequencies
Continuous variables: use a gaussian curve
When the input variables are discrete (e.g. words in an email), we can directly use the frequency of a specific event happening within the training data as our probability. This type of naive bayes classifier called the Multinomial Naive Bayes Classifier.

Lets have a look at an example of spam email classification:
![image](https://user-images.githubusercontent.com/89111546/192165153-32f745e5-b80f-4f0d-be42-3e3e31b364f2.png)

Here, we are trying to classify spam and non-spam emails depending on whether they contain the word viagra. From the above table, we can compute the probabilities as:

Likelihood: P(X=viagra|Y=spam) = 4/20 = 0.2
Likelihoods for other words can be calculated similarly as above
Prior probability: P(Y=spam) = 20/100 = 0.2
Then, we find the product of the individual likelihoods as our overall likelihood under the class-conditional independence assumption. Finally, the posterior probability is directly proportional to the product of the overall likelihood and the prior probability.

This posterior probability we calculated corresponds to the class of spam emails. We can do the same for the class of non-spam emails. We then compare the posterior probabilities of the 2 classes and go for the higher one.

# Why all these troubles?
Looking at the above table, some may ask why don't we just find the individual posteriror probabilities and calculate the product to get the final result instead of going through the calculations of bayes' theorem?

Let me show you with an example why the assumption can only be applied to the likelihood but not the posteriror probability:
![image](https://user-images.githubusercontent.com/89111546/192165168-c02852e3-0d01-4a1c-a252-9ecb1be60790.png)

As you can see, the assumption will result in a non-realistic result and therefore cannot not be applied to the posterior probability directly.

# Gaussian Naive Bayes Classifier
Now, let's talk about the naive bayes classifier that deals with continuous input variables: the Gaussian Naive Bayes Classifier.

The gaussian naive bayes classifier makes an additional assumption: it assumes that each of the input variables follows a normal distribution. Therefore, the classifier finds the likelihood using a gaussian curve (the probability curve for a normal distribution) instead of calculating the frequencies.

Let me show you how this is done with an example of classifying gender using age:
![image](https://user-images.githubusercontent.com/89111546/192165184-4ef6ca73-91ce-470c-b6f0-c62ed006ab58.png)

With the mean and standard deviation, we can draw a gaussian curve for the age feature. Then, the likelihood of having a specific age given the new data point represents a male can be find using the curve as demonstrated above.

Similar to the multinomial naive bayes classifier, the gaussian naive bayes classifier first calculates the individual likelihood. Then, it computes the overall likelihood by applying the class-conditional independence assumption. Finally, it finds the posterior probability for each class and compare them to reach a classification result.





