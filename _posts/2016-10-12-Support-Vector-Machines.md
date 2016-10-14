---
layout: post
type: blog
title: Support Vector Machine
excerpt: Description of inner workings of SVM [In Progress]
comments: true
background: /svm-1.png
published: true
authorname: Himanshu Misra
authordesignation: Data Scientist @ Legacy.com
authorimage: /himanshu.jpg
authorlinkedin: https://www.linkedin.com/in/hmisra
authorfacebook: https://www.facebook.com/himanshumisra1990
authorgithub: https://github.com/hmisra
authortwitter: https://twitter.com/himanshumisra
---

## Introduction
------------------------------
Support Vector Machines were introduced in 1962 as non-probabilistic binary linear classifiers by Vladimir Vapnik and Alexey Ya. Chervonenkis. Later, in 1992, Bernhard E. Boser, Isabelle M. Guyon and Vladimir Vapnik proposed a way to learn non-linear decision boundaries using SVM.

In this post I intend to provide my understanding of SVM's with as little mathematics as possible.


## Mathematical Pre-requisite
------------------------------
I understand that toward the end of previous section I mentioned that there would be very little mathematics, but these mathematical concepts are bare minimum requirements for understanding how does a SVM does what it does.

1. **Dot Product**: $ \vec {u} . \vec{v} $ is an operation which computes projection of vector $ \vec {u} $ on vector $ \vec {v} $ . The result of dot product of 2 vectors is a scalar quantity which can be interpreted as the magnitude of the similarity between 2 vectors with range {-1, 1} where the result of 1 means they point in the same direction, -1 means they point in opposite direction and 0 means they are orthogonal to each other.



## The binary classification problem

The binary classification problem can be defined as assigning one out of 2 classes to n dimensional points. Lets consider an example so that we can visualize it much better.
<center>
<img src="/svm-2.png" width="400" height ="400"/>
</center>
Here the $ {x_1} $ and $ {x_2} $ are the input dimensions and the label of the data points $ {y} $ is the target dimension. Hence the binary classification problem can be defined as learning a classifier (can also be read as a function) which can predict the label $ {y} $ for unseen data points. SVM falls into a class of classifiers which does so by learning a decision boundary. You can imagine this as a line or hyperplane for higher dimensional data points which tries to separate the 2 classes and the equation of this line or hyperplane can then be used to check which side of the line or hyperplane the new data point falls. In the diagram above you can see that line 1 which is separating the positive and negative classes can be a decision boundary. After learning the parameters of this line once you get a new point you can check which side of the line the point falls into by putting the x into the equation and by checking the sign of the result. Most of the linear classifiers like logistic regression tries to learn the decision boundaries in a similar way.

SVM goes a step further. You can see in the diagram above that there can be multiple lines which can divide the 2 classes. But out of all the possible line one line would be best which would allow classifier to generalize well. For example line 2 might misclassify the positive data points present on the upper left side of the point close to the line 2. This over fitting would restrict the classifier to generalize with new points. To restrict this Logistic Regression uses regularization (restricts the weights of the classifier) but SVM uses a different mathematical solution to find an optimum decision boundary.


## Support Vector Machine

Lets first intutively try to formalize the notion of optimum decision boundary. Consider the 2 points $ {a} $ and $ {b} $ which falls into negative and positive class respectivily (see the diagram below). What can you notice special about these points ? You can notice that these points are closest to the points of the other class, or to put it in other words you can say that they are the last points in their classes if we consider the dotted lines as our decision boundries. There can be multiple such points which falls close to the dotted decision boundries. Now try to think how can you define an optimal decision boundry with the help of dotted lines. Intutively you can see that the best line you can put would be at the center of the zone between 2 dotted lines.

<center>
<img src="/svm-1.png" width="400" height ="400"/>
</center>

Now lets formalize this notion mathematically, We can clearly see that the line that we can consider best decision boundary would be at maximum distance from the 2 dotted line. In other words the line would be at maximum distance from $ {a} $ and $  {b} $ . This distance is called the margin. Now we need to find a line which maximizes this margin and that would be our optimal decision boundary. Here we would make an assumption that all the decision boundaries, line 1, 2 and 3 are parallel to each other, the reason for this assumption would be clear very soon.

Lets consider that the optimum line is line 1 which can be defined by the equation (in vector form) :

$$

{y}={W}^T {x} + {c}

$$

If we substitute point a and b into this equation we would get:

$$

{W}^T {a} + {c} = {1}

$$


$$

{W}^T {b} + {c} = {-1}

$$


Now to compute the margin we would need to find the difference between $ {a} $ and $ {b} $ which we can do by subtracting the 2 equations above and we get:


$$

{W}^T ({a} - {b}) = 2

$$

Now recall from the linear algebra class that the weight vector $ {W} $ is orthogonal to the line, so to compute the margin we find the difference between $ {a} $ and $ {b} $ in direction of W. For this we would divide both sides with norm of W and it would give us the margin $  {m} $.

 {% raw %}
$$

\dfrac{W^T ({a} - {b})}{||W||} = \dfrac{2}{||W||} = {m}


$$
 {% endraw %}


> So first lets review what we have done so far and then proceed further, we selected an arbitrary line as our decision boundary assuming that it is our optimal decision boundary. They we took 2 points on the dotted lines which are parallel to the decision boundary we selected. We substituted both of these points in the equation of line and then computed the difference between them. We projected that difference on the unit weight vector which we called our margin. 

Now recall that we decided that the optimum line would be the one which maximises the margin. So we will now create an optimization problem which would give us a weight vector which can maximize this margin.

Also, this would be an constrained optimization problem as we need the $ {W} $ which maximizes the margin but also classifies the points correctly. 


$$

maximize \dfrac{2}{||W||}

$$

<center> constrained by:  </center>

$$

{y_i}({W}^T {x_i} + {c}) \geq 1

$$


To solve this optimization problem we would translate into a form which we can solve. Lets's first convert this to a equivalent minimization problem, for which we would reciprocate the margin and square the weight:

$$

minimize \dfrac{||W||^2}{2} 

$$

<center> constrained by:  </center>

$$

{y_i}({W}^T {x_i} + {c}) \geq 1

$$


Now this form of optimization problem can be solved using quardatic programming. Here in this post I would not go into Quardatic Programming much but you can take my word for the steps to follow.

Using quardatic programming we can translate the minimization problem mentioned above into a standard form 

$$

F(\alpha) = \sum_{i} \alpha_i - \dfrac{1}{2} \sum_{ij} \alpha_i \alpha_j y_i y_j x_i^T x_j

$$






