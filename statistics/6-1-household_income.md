[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

    mean = Mean(sample) 
    median = Median(sample)
    skewness = Skewness(sample)
    pearson = PearsonMedianSkewness(sample)
    print (mean, median) #(74278.707531187392, 51226.454478940461)
    print (skewness, pearson) #(1.054840012109306, 0.26436733816180391)
    cdf.Prob(mean) #0.66; 
>>The upper bounds highly skew the results as seen from the skewness rating (1.05). It seems like there are a lot of right outliers in the dataset dragging up the mean. The skew would increase if we increased the upper bound as it would add additional outliers. However, the Pearson Median Skewness may decrease since it would also increase the standard dev of the data set 
