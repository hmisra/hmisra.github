---
layout: post
type: notes
title: Introduction to Spark
excerpt: Note 1
comments: true
background: /network.jpg
published: true
authorname: Himanshu Misra
authordesignation: Data Scientist @ Legacy.com
authorimage: /himanshu.jpg
authorlinkedin: https://www.linkedin.com/in/hmisra
authorfacebook: https://www.facebook.com/himanshumisra1990
authorgithub: https://github.com/hmisra
authortwitter: https://twitter.com/himanshumisra
---




### Introduction

* Apache Spark is large scale data processing engine which allows fast and scalable computation.
* It is commonly used for ETL, Analytics and Visualization on Big Data.
* Spark can infer the schema from the data or we can manually define the schema.
* Spark architecture has 2 component:
    - Driver : Runs on the client machine
    - Worker : Can run on same machine or as a cluster.


### How do you write a spark job

* Create a spark context (in most of the environment like pyspark or any other spark only platform this step is already done for you, but if you are writing your own python code in ipython or some python IDE you must define a spark context). Using Master parameter you can specify which type of cluster to use
* Create a SQL Context.
* Then use SQL Context to create a DataFrame.

### Data Frames

Data Frames are spark abstraction which allows spark to perform parallel processing on them.

* Data frames are immutable, once created.
* Track lineage information to recompile lost data, so fault tolerant.
* Enable operations on collection of elements in parallel.

#### How to create Data Frames

We can create data frames in 3 main ways:
* by parallelizing exisiting python collection.
* by transforming existing Data Frame or Pandas Data Frame.
* by files on HDFS or File System

#### More on Data Frames

* each row in a data frame is a Row() object.
* columns can be accessed as attributes of data frames.

### Operations on Spark DataFrames

There are 2 types of operations we can perform on Spark DataFrame:
1. Transformations 
2. Actions

#### Transformations

* Transformations are primarily slicing and dicing operations on Data Frames.
* Lazy Evaluation: these operations are not actually performed on Data Frames untill a Action operation is performed on the Data Frame. For this Spark keeps track of all the transformation actions to be performed on the Data Frame.
* You can persist a Data Frame on Disk to avoid Recomputation.
* Spark performs transformations on Worker Nodes.

#### Actions

* Actions are operations where you try to get information out of the data frame. 
* When you try to execute and Action then Spark performs all the transformation actions on DataFrame and then gives you results
* Spark perform actions on both worker and driver nodes.

### Examples

#### Creating Data Frames

``` python
# create data frame from SQL Context

data = [('Name1', 21), ('Name2', 24)]
df = sqlContext.createDataFrame(data, ['name', 'age'])

# data could be a pandas data frame too !!

df = sqlContext.createDataFrame(pandasDF)

# You can create a pandas DF from a text file in HDFS, each row of the file would be a Row() object in the Spark Data Frame

df = sqlContext.read.text('filename.txt')

```


#### Transformations


```python

# create people data frame

people = sqlContext.createDataFrame(data, ['name', 'age'])

# select age and store it in new DF, remember DFs are immutable

ageCol = people.age

# Transformation Operations

    people.select('*') # Select all rows and cols

    people.select('name', 'age') # Select name and age from DF

    # to drop a column

    people.drop(people.age)
    
    # To apply a user defined function you can create user defined function to be applied on Data Frames using UDF. it accepts function definition and return type as argument
    
    slen = udf(lambda s: len(s), IntegerType())
                                         
    # here we apply slen function on name col of people DF and return a new DF where the results are under column named slen                                            
    lendf = people.select(slen(people.name).alias('slen'))
    
    
    # Some other Transformations
    
    filter(*function) # returns rows where function returns true
    where(*function) # alias for where
    distinct() # returns dataframe with only distinct rows
    orderby(*cols) # order the columns
    sort(*cols) # sorts the columns
    explode(col) # returns a new row for each element in a given array
    


```

#### Actions

``` python

#Show returns n rows as DF
df.show(n, truncate) 

#take returns n rows as list of Row() objects
df.take(n)

#returns all records, be cautious in running collect as collect tries to return all the results and fits result in memory. If you have data which is more than size of your memory running collect would crash your program.
df.collect()

# Count returns number of rows in the DF, count also can appear after a group by operations as an aggregation, in that case count acts as a transformation.
df.count()

# describe provides summary statistics for all the numerical columns in the dataframe
df.describe()

```

### Best Programming practices for Spark

1. Use predefined transformations and actions whereever possible. Check spark Data Frame API referece.
2. Never use collect() in production, it may crash your system, instead use take(n) to perform select operations on your data frame.
3. use cache() function to persist your data frame to avoid recomputation.
