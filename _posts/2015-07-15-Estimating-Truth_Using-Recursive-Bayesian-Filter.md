---
layout: post
title: Recursive Bayesian Filter
excerpt: Truth Estimation using RBF
comments: true
background: /network.jpg
---

## Introduction
----------------------------------
Whenever we make any critical decision in our life we tend to take suggestions and recommendations from different people. We try to analyze information from various sources and based on our analysis, we decide what to do.

To understand this process more intuitively let's take an example. Last week a friend recommended me to watch a movie called “Attack of the Killer Tomatoes!”. Now looking at the title of the movie I felt bit suspicious and started pondering if it is actually as good as my friend was praising it. The obvious next step was to gather more information about the movie. I checked the movie trailer on YouTube according to which it seemed like a pretty funny movie. Despite the claims made by the trailer like “perhaps the funniest film ever made” I decided to check reviews and ratings for the movie on IMDB and RotttenTomatoes, where it was rated below 5. As I trust IMDB movie ratings more than anything when it comes to watching movies, I decided to pass “Attack of the killer Tomatoes !” and watch it some other time. In real life, we mostly follow this kind of reasoning where we combine various evidence and come to a conclusion.

Now mathematically we can formulate this process as follows, we can consider that “Attack of the Killer Tomatoes!” is a binomial random variable which can either take values “Good” or “Bad”. Initially, I had a recommendation for the movie so the probability distribution was more toward the value Good i.e `P(“Attack of the Killer Tomatoes!” =Good)` was 0.7. As we start getting data from different sources, we can start inferring from it if the movie is good or bad, and start changing our initial belief. Sadly, for me at the end the `P(“Attack of the Killer Tomatoes!” =Good)` was below 0.5 so I decided to not watch the movie.
<br><br>

## Bayes Theorem
------------------------------
A very elegant mathematical framework called “Bayes Theorem” given by an English philosopher and statistician, Thomas Bayes, allows us to do precisely this kind of reasoning. According to the Bayes rule

```
P(A|B) = P(A)×P(A,B) = (P(A) × P(B|A)) / P(B)
```

where P(A)(Prior Distribution) represent our prior knowledge of the world , `P(B|A)P(B)` represent the Probability Distribution of data given our prior knowledge and `P(A|B)` represent the posterior or updated probability distribution. In simple words, you take what you know about the world (i.e your prior distribution), then take the new data and try to evaluate if this new data conforms with your prior knowledge. Multiply the 2 distribution and you get an update belief about the world, which in next iteration you can use as your new prior distribution/belief.

To help you visualize more clearly first let's take a simple example which can help you visualize this process and then we will take a toy problem and try to solve it using Bayesian estimation.

The complete code for computation and plotting can be found [here](https://gist.github.com/hmisra/f4edf5b58aedb6075fcd "Source Code").

Assume that you have a random variable A which can take values from 1 to 6. Now you want to know which value of A is the most probable value. You think that it is somewhere close to 3.5 and your belief can be described by a normal distribution around 3.5 with a variance of 0.5. This distribution can be plotted as follows

<center>
<img src="/recursive1.png"/>
</center>


Now you start getting data B from some source. To calculate `P(A|B)` we need the distribution `P(A,B)`, a joint distribution of our prior knowledge and the data. In real life getting this distribution is hard and we normally employ various assumptions and approximation techniques to get this distribution. Later in this article while solving a toy problem we would use a simple assumption to estimate this distribution. For now let's assume you already have this distribution and can be represented by the 3-D plot drawn below. Now by multiplying our prior distribution and this joint distribution so that we can get an updated distribution. But as you can see our prior is a uni-variate distribution and `P(A,B)` is bi-variate, so we can not directly multiply these 2 distribution. We would take a slice out the `P(A,B)` which is shown in graph below as conditional probability `P(B|A=3)`. Now if you are familiar with basic rules of probability theory you must already know that The sum of probability of all the events is equal to 1, i.e. `∫P(A)=1` and also `∫P(A,B)=1` or in simple words area under the surface/curve of a probability distribution must be 1. As we know that the distribution `P(A,B)` is a probability distribution and the area under the surface of distribution is 1, so if we take a slice out of this distribution, this conditional distribution `P(B|A=3)` is no more a valid probability distribution. Therefore, if we multiply this distribution with our prior we would get an invalid probability distribution. Hence we need to normalize it by dividing by `P(B)` so that we get a valid posterior probability distribution.

<center>
<img src="/recursive2.png"/>
</center>

So let's summarize what we have covered so far, we had our prior knowledge about the world, we took some data, computed the conditional distribution of data and normalized it with the distribution of data. By plugging these values in Bayes theorem, we would get a posterior distribution. Now in later iterations when we will get a new piece of data we would consider this posterior as our prior and again compute our posterior.

This recursive process is commonly known as Recursive Bayesian Filter.

Toy Problem: Helping Iron Man to locate Whiplash using Recursive Bayesian Filter
Now let's describe a toy problem and try to solve it using Recursive Bayesian Filter.

I am an ardent fan of Iron Man movies so I couldn't resist to take example in which we would help Iron Man to kill the bad guy: Whiplash. Imagine that there is a wall of height and width of 40 * 40 ft. and Whiplash is hiding behind the wall. Also, during his duel with Whiplash, Iron man got his Infra-Red sensor damaged and is left with a single bullet using which he wants to kill whiplash. Now, as the IR sensor got damaged Iron Man is getting the erroneous heat signatures on the wall. Hence, Iron Man decides to take 100 readings and sends it to Jarvis. Now as Jarvis it is our job to figure out where precisely Whiplash is hiding.

So let's see how we can help him kill “Whiplash” using Recursive Bayesian Estimation we discussed earlier.

We are performing following steps to get the graph displayed below:

1. we will create a matrix of size 41*41, representing the wall behind which whiplash is hiding.

2. we will mention the true location of whiplash which Iron Man does not know, in the plot this location is represented with Red dot.

3. we will assume that the reading from Infrared sensor is faulty and we will sample 100 readings from a normal distribution with the mean at true location and variance of 10.


<center>
<img src="/recursive3.png"/>
</center>




So as we can see the true location of Whiplash is at the red dot in the map, but after taking 100 readings from infrared sensor Iron man can only see the blue dots. Our job now is to estimate the position of the red dot by looking at these 100 dots.

Next to start using Recursive Bayesian we need a prior distribution which would represent our initial knowledge about the world. Now for this we can either assume that Iron man does not know anything about the location of Whiplash and would use a uniform distribution (i.e. he would assume that Whiplash can be anywhere with equal probability.) or if he saw Whiplash going from left side of the wall then we can create a distribution incorporating this knowledge. To keep things simple for now, I would assume that he does not know anything about the location of Whiplash.

<center>
<img src="/recursive4.png"/>
</center>

As you can see the distribution is uniform and the probability of Whiplash being at any point on this wall is equal.

Now let's take this prior distribution and start our recursive Bayesian estimation. We would perform following steps to get a posterior distribution:

1. We will take each point and create a normal distribution around this point (earlier in this article I have mentioned that estimation of joint distribution or conditional distribution is difficult in real life and we employ various assumptions and approximations. To get this distribution, here we are assuming that the conditional distribution is just a normal distribution with mean at the location of the point and a variance of 20 on each coordinate)

2. we will multiply this distribution around the data point with our prior distribution to get posterior distribution.

3. the posterior distribution which we got is not a probability distribution anymore so we will normalize this distribution.

4. make this posterior distribution prior and repeat for all the data points. The output of this part is in the form of video in which you can clearly see the results of each iteration in the form of surface plot and heat map.

At the end of iterating through 100 data points, you can clearly see that we have estimated that the location of whiplash is near 20,20 as the probability near 20,20 is maximum.

<center><iframe width="420" height="315" src="https://www.youtube.com/embed/vUFoFwtBqXU" frameborder="0" allowfullscreen></iframe>
</center>

## Real world applications

1. In application that uses geospatial data for example UBER, where there is a need to locate the precise location of an object through GPS (in case of Uber, a car), we can use this method to estimate the precise location of the car.

2. Improved methods (like Kalman Filters, Particle Based Estimation methods etc.) based on Recursive Bayesian Filters are used in Radars to track missiles. Check out this [Paper](http://down.cenet.org.cn/upfile/28/20051117121144185.pdf) for more details.
