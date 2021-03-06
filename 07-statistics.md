# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.

    def CohenEffectSize(group1, group2):
        """Computes Cohen's effect size for two groups.

        group1: Series or DataFrame
        group2: Series or DataFrame

        returns: float if the arguments are Series;
                 Series if the arguments are DataFrames
        """
        diff = group1.mean() - group2.mean()

        var1 = group1.var()
        var2 = group2.var()
        n1, n2 = len(group1), len(group2)

        pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
        d = diff / np.sqrt(pooled_var)
        return d
        print(CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)) #-0.0886729270726
>The effect size is higher for weight than pregnancy length. First born babies are likelier to be lighter than other babies


### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

    resp = nsfg.ReadFemResp()
    kid_pmf = thinkstats2.Pmf(resp.numkdhh, label = 'observed')
    thinkplot.Pmf(kid_pmf)
    thinkplot.Show(xlabel = 'Kids')
    biased_pmf = BiasPmf(kid_pmf, label='biased')
    thinkplot.PrePlot(2)
    thinkplot.Pmfs([kid_pmf, biased_pmf])
    thinkplot.Config(xlabel='Kids', ylabel='PMF')
    kid_pmf.Mean() #1.0242051550438309
    biased_pmf.Mean() # 2.4036791006642821

### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  
    
    import numpy
    ran = numpy.random.random(1000)
    pmf = thinkstats2.Pmf(ran, label = 'random numbers')
    thinkplot.Pmf(pmf)
    cdf = thinkstats2.Cdf(ran, label = 'random numbers')
    thinkplot.Cdf(cdf)
    
> It looks random because the pmf is uniformly distributed and the cdf is fairly linear

### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic. 

    (dist.cdf(185.4)- dist.cdf(177.8))*100 #34.21%

### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

>> To compare the odds of being a fraternal twin vs identical twin vs neither, we find the lowest common denominator for the probabilities i.e. 1500. This is equivalent to 12/1500, 5/1500, and 1483/1500 respectively. Knowing that Elvis was a twin, we can eliminate the odds of him being neither (1483/1500) according to Bayes Theorem. 
>> This leads to 17 remaining possibilities for twins = 12 for fraternal and 5 for identical. The odds of Elvis being an identical twin is 5/17.
---

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

>> Frequentist statistics is the traditional stats you learn in class. It basically assumes an overarching representative statistical model, built off of a large set of data, that a scenario can apply holistically into as a sample. 
>> Bayesian stats takes this one step further by incorporating prior knowledge in as an input to this model.
>> For example, if I'm trying to find a vintage record in the cty, the frequentist might use a model focusing on the distribution of record stores in the city. The Bayesian would build upon this model by using their previous experiences in record stores and their rare record inventory to focus on a neighborhood or area first. 

---

## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.    

    thinkplot.Scatter(live.agepreg, live.totalwgt_lb)
    thinkplot.Show(xlabel = 'Years', ylabel = 'LBs', alpha = .2)
    bins = np.arange(15,40,4)
    indices = np.digitize(live.agepreg, bins)
    groups = live.groupby(indices)

    mean_age = [group.agepreg.mean() for x, group in groups]
    cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for x, group in groups]

    for percent in [25,50,75]:
        weights = [cdf.Percentile(percent) for cdf in cdfs]
        label = '%dth' %percent
        thinkplot.Plot(mean_age, weights, label = label)

    thinkstats2.Corr(live.agepreg, live.totalwgt_lb) #0.068833970354109084
    SpearmanCorr(live.agepreg, live.totalwgt_lb) #0.094610041096582262

>> There's basically no correlation between mother's age and birth weight

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

    def expestimator(n, lamb, iterations):
        mean = []
        for x in range(iterations):
            xs = np.random.exponential(1.0/lamb, n)
            mean.append(1/np.mean(xs))
        return mean
    def test1():
        mean = expestimator(10, 2, 1000)  
        cdf = thinkstats2.Cdf(mean)
        rmse = RMSE(mean, 2)
        thinkplot.Cdf(cdf)
        print('Standard Error:', rmse)
        print('90% Confidence Interval:', cdf.Percentile(5), cdf.Percentile(95))

    test1()
    
    def test2(lamb):
        n = [20, 30, 40, 50, 60, 70, 80, 90, 500, 1000]
        rmse = []
        for x in n:
            rmse.append(RMSE(expestimator(x, lamb, 1000), lamb))
        thinkplot.Plot(n, rmse)
        thinkplot.Config(xlabel = 'samples', ylabel = 'Standard Error')
    test2(2)
>> You can see that as N increases, the RMSE decreases closer to 0. 
    
### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)
    mean = Mean(sample) 
    median = Median(sample)
    skewness = Skewness(sample)
    pearson = PearsonMedianSkewness(sample)
    print (mean, median) #(74278.707531187392, 51226.454478940461)
    print (skewness, pearson) #(1.054840012109306, 0.26436733816180391)
    cdf.Prob(mean) #0.66; 
>>The upper bounds highly skew the results as seen from the skewness rating (1.05). It seems like there are a lot of right outliers in the dataset dragging up the mean. The skew would increase if we increased the upper bound as it would add additional outliers. However, the Pearson Median Skewness may decrease since it would also increase the standard dev of the data set 

### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)

    def game(lam):
        goals = 0
        t = 0
        while True:
            t2 = random.expovariate(lam)
            t+=t2
            if t>1:
                break
            goals+=1
        return goals
    def game_simulator(num, lam):
        goals = []
        for x in range(num):
            goals.append(game(lam))
        print('Mean Error:', MeanError(goals, lam))
        print('RMSE:', RMSE(goals, lam))
    game_simulator(10000, 2)
>> The estimate is not biased since Mean Error decreases as the number of simulations increase. 

### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
