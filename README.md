# econ3916-lab04-anomaly-detection
# Robust Statistics -- Automated Anomaly Detection

## Objective

This project compares robust and non-robust statistical measures on housing data to show how contamination in a dataset can silently distort standard summary statistics while leaving robust alternatives largely unaffected.

## Methodology

- Computed both robust and non-robust summary statistics, mean, median, trimmed mean, standard deviation, IQR, and MAD, on California Housing data covering 20,640 observations
- Implemented Tukey Fences manually from scratch to flag price outliers using the interquartile range
- Applied scikit-learn's Isolation Forest to detect multivariate anomalies across multiple features at once
- Compared the outliers flagged by Tukey Fences against those flagged by Isolation Forest and found that the two methods frequently disagree, flagging different observations
- Ran a contamination experiment, deliberately injecting corrupted values into the data to test how each statistic responds
- Built an interactive explorer with adjustable Tukey k and Isolation Forest contamination sliders to compare the two outlier-detection methods side by side

## Key Findings

- The mean shifted by 67.1% after contamination, while the median shifted by only 3.6%, showing just how dramatically a handful of extreme values can distort an average while barely affecting the middle value of a sorted dataset
- Tukey Fences and Isolation Forest flag meaningfully different rows, which makes sense since Tukey Fences only ever look at one column at a time, while Isolation Forest can catch anomalies that only show up when multiple features are considered together
- The trimmed mean, which discards the most extreme 10% of values on each tail before averaging, held up well against contamination levels below that threshold, but would be expected to start shifting once contamination on a single tail approaches or exceeds 10%
- Together, these results show that choosing a statistic is not a neutral decision: the same dataset can tell a very different story depending on whether the measure used is sensitive to extreme values or resistant to them
