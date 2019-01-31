# feature engineering

# 特征工程

Feature engineering is the process of formulating the most appropriate features given the data, the model, and the task.

k-means clustering, nearest neighbors methods, radial basis function (RBF) kernels, and anything that uses the Euclidean distance. For these models and modeling components, it is often a good idea to normalize the features so that the output stays on an expected scale.

For instance, the training process of a linear regression model assumes that prediction errors are distributed like a Gaussian. This is usually fine, except when the prediction target spreads out over sev‐ eral orders of magnitude. In this case, the Gaussian error assumption likely no longer holds. 

In addition to features tailoring to the assumptions of the model or training process, multiple features can be composed together into more complex features. The hope is that complex features can more succinctly capture important information in raw data. Making the input features more “eloquent” allows the model itself to be simpler, easier to train and evaluate, and to make better predictions.


engineer the target variable of the model. Strictly speak‐ ing, the target is not a feature because it’s not the input. But on occasion we do need to modify the target in order to solve the right problem


boxcox  # By default, the scipy implementation of Box-Cox transform finds the lambda # parameter that will make the output the closest to a normal distribution
probplot  检验是否符合某一分布，如果时，那么可线性拟合 theoretical quantiles

unlike the log transform, feature scaling doesn’t change the shape of the distribution; only the scale of the data changes.

# boxplot
The middle line in the box marks the median accuracy, the box itself marks the region between the first and third quartiles, and the whiskers extend to the rest of the distribution.

# 类型变量取值过多的解决办法
- feature hashing 也用于降维
- bin counting
