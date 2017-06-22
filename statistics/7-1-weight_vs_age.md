[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)
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
