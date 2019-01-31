# descison tree


CART gini index
The Gini impurity is simply the probability of obtaining two different outputs, which is an "impurity measure". In the other direction, if we have a j⋆ such that p(j⋆|t)=1 (and thus the other p(j|t)=0) we have a Gini impurity i(t)=0 and we will always get two identical outputs of category j⋆, which is a "pure" situation!.


决策树支持连续变量的处理，**怎样找到一个连续变量feature的最佳分割点**：
1. 按照feature的值排序，v1,v2,v3,...vn
2. 取各相邻分割点的平均值作为可选分割点，例如(v1+v2)/2, (v2+v3)/2, 从这些分割点中选择最佳分割点
