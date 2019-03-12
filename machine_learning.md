# machine learning

# 评估classification
- accuracy
- confusion matrix 混淆矩阵 (多分类问题直接从图可以看出，类似于热图，个数多的颜色深，不在对角线的有问题)
  https://scikit-learn.org/stable/auto_examples/model_selection/plot_confusion_matrix.html
  The rows of the matrix correspond to ground truth labels, and the columns represent the prediction.
- per class accuracy 不平衡时有用
- Log-loss
  is a “soft” measurement of accuracy that incorporates this idea of probabilistic confidence. 例如0.51的+1 预测为-1 并没有那么糟糕
  Cross entropy incorporates the entropy of the true distribution, plus the extra unpredictability when one assumes a different distribution than the true distribution. So log-loss is an information-theoretic measure to gauge the “extra noise” that comes from using a predic‐ tor as opposed to the true labels. By minimizing the cross entropy, we maximize the accuracy of the classifier.
- auc
  The ROC curve shows the sensitivity of the classifier by plotting the rate of true positives to the rate of false positives
  It shows you how many correct positive classifications can be gained as you allow for more and more false positives.
- precision-recall curve is to fix k and combine precision and recall （返回前k个结果） [搜索页可以看作classification, 结果相关分数]
  f1值就是p，r的调和平均数
  缺点是前k个结果重要性视一样，NDCG 考虑到 the positioning of the returned items is important.
  
# 评估regression

- recommender可以看作regression，预测item rating
- RMSE 缺点：个别的outlier会有很大影响
- MAPE median absolute percentage  
  For example, the percent of estimates within 10% of the true values would be computed by per‐ cent of |(yi – ŷi)/yi| < 0.1.
  
It is always better to train the model to directly optimize for the metric it will be evaluated on. But for certain met‐ rics, this may be very difficult or impossible. (For instance, it’s very hard to directly optimize the AUC.) Always think about what is the right evaluation metric, and see if the training procedure can opti‐ mize it directly.



Bootstrap, on the other hand, resamples the data with replacement.
empirical distribu‐ tion of data. Bootstrap simulates new samples by drawing from the empirical distribution. The data point must be put back, because otherwise the empirical distribution would change after each draw.

Both bootstrapping and cross-validation can provide not only an estimate of model quality, but also a variance or quan‐ tiles of that estimate

# regularization的作用

A regularization hyperparameter controls the capacity of the model, i.e., how flexible the model is, how many degrees of freedom it has in fitting the data. Proper control of model capacity can prevent overfitting, which happens when the model is too flexible, and the training process adapts too much to the training data, thereby losing predictive accuracy on new test data. So a proper setting of the hyperparameters is important.

# hyper tuning

grid search and random search 需要list of params 作为输入
random search区别： Instead of searching over the entire grid, random search only evaluates a random sample of points on the grid. This makes random search a lot cheaper than grid search.
if at least 5% of the points on the grid yield a close-to-optimal solution, then random search with 60 trials will find that region with high probability. 

# A/B test
- 最好先做A/A test，只有通过A/A test之后才做A/B test   do some A/A testing to make sure that your testing framework is sound
- 选择metric，business metric多半不同，需要和evaluation metric有直接相关性
- 确定多大的改变是真的改变
- two-sided test. 既要测试是否更好，也要测试是否更差
- 能够忍受多少false positive
 A statistical hypothesis test allows you to control the probability of false positives by setting the significance level, and false negatives via the power of the test. If you pick a false positive rate of 0.05, then out of every 20 new models that don’t improve the baseline, on aver‐ age 1 of them will be falsely identified by the test as an improve‐ ment. 
 
 in addition to running the hypothesis test and com‐ puting the p-value, one should always check the confidence interval of the two population mean estimates. If the distribution is close to being Gaussian, then the usual standard error estimation applies. Otherwise, compute a bootstrap estimate
 
如果是选择模型，A/B test适用。如果目标是最大化reward，那么可以适用MAB (multiarmed bandit)


# tf transformation
term weight 个数 通过 sub linear function 转换，越大越缩减影响，例如 bm25, log(1+x)

# 词袋模型
the bag of words representation is generally quite effective for tasks involving topic discrimination (notably information retrieval, text categorization and text clustering)

短语 或者 frequent pattern （例如词语的集合，在某个window中出现，不管集合中词语的顺序）larger units may be regarded as supple- mentary with the bag of words representation

# precision 和 recall 在 IR 和 classification 中有不同的意义：
https://en.wikipedia.org/wiki/Precision_and_recall


chain rule: The general rule is to sum over all possible paths from one node to the other, multiplying the derivatives on each edge of the path together.

efficiently computing the sum by factoring the paths. Instead of summing over all of the paths explicitly, they compute the same sum more efficiently by merging paths back together at every node. In fact, both algorithms touch each edge exactly once!
