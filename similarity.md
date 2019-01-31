# similarity

Jaccard similarities need not be very high to be significant. 集合相似度，交集元素个数除以并集元素个数

3.4.3 Combining the Techniques
We can now give an approach to finding the set of candidate pairs for similar documents and then discovering the truly similar documents among them. It must be emphasized that this approach can produce false negatives – pairs of similar documents that are not identified as such because they never become a candidate pair. There will also be false positives – candidate pairs that are evaluated, but are found not to be sufficiently similar.
1. Pick a value of k and construct from each document the set of k-shingles. Optionally, hash the k-shingles to shorter bucket numbers.
2. Sort the document-shingle pairs to order them by shingle.
3. Pick a length n for the minhash signatures. Feed the sorted list to the algorithm of Section 3.3.5 to compute the minhash signatures for all the documents.
4. Choose a threshold t that defines how similar documents have to be in order for them to be regarded as a desired “similar pair.” Pick a number of bands b and a number of rows r such that br = n, and the threshold t is approximately (1/b)1/r. If avoidance of false negatives is important, you may wish to select b and r to produce a threshold lower than t; if speed is important and you wish to limit false positives, select b and r to produce a higher threshold.
5. Construct candidate pairs by applying the LSH technique of Section 3.4.1.
6. Examine each candidate pair’s signatures and determine whether the frac-
tion of components in which they agree is at least t.
7. Optionally, if the signatures are sufficiently similar, go to the documents themselves and check that they are truly similar, rather than documents that, by luck, had similar signatures.


# bloom filter

判断一个元素是否在一个很大的set里面
这个set大到以至于不能直接常驻内存，则用bit array，每一个bit为一个bucket，把实际的一个元素通过hash映射到一个bit里面，set的元素个数接近（有可能hash冲突）于为1的bit数。
要检查一个元素是否在set里面，那么就hash这个元素，看对应的bit是否为1。
使用多个hash函数，要所有hash结果对应bit都为1，才认为通过。这样可以降低fasle postive的概率。


# 大数据 找相似
Once we have a distance measure, either Jaccard or cosine, we can use minhashing (for Jaccard) or random hyperplanes (for cosine distance; see Section 3.7.2) 
feeding data to an LSH algorithm to find the pairs of documents that are similar in the sense of sharing many common keyword


# UV decomposition 估计矩阵空值 RMSE

In general, we can measure the similarity of users by their cosine distance in concept space.

初始化w全0，然后
perceptron训练步骤

Consider each training example t = (x, y) in turn.
(a) Let y′ = w.x.
(b) If y′ and y have the same sign, then do nothing; t is properly classi- fied.
(c) However, if y′ and y have different signs, or y′ = 0, replace w by w + ηyx. That is, adjust w slightly in the direction of x.


How do we compute similarity to an unseen document (queries)? We can leverage the matrix T to create a mapping from the term vector for the un- seen document to the k-dimensional document space. Let q be the |V | vector representation for the unseen document. Then, we can compute
qˆ = q T T
and compute dot products against the elements of DTS. This effectively amounts to placing q at the centroid of the factor vectors for its terms ex- tracted from T.



