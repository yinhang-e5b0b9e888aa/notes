# deep learning

* 常用数据集：ImageNet, MNIST, COCO dataset, CIFAR, The Street View House Numbers, PASCAL VOC, Wikipedia dump, 20 Newsgroups, Penn Treebank, Kaggle
* 学习框架：TensorFlow, Caffe2, Keras, Theano, PyTorch, Chainer, DyNet, MXNet, CNTK

In certain domains, such as computer vision and natural language processing (NLP), feature engineering is challenging as they suffer from high dimensionality.

Traditional ML algorithms use handwritten feature extraction to train algorithms, while DL algorithms use modern techniques to extract these features in an automatic fashion.

large companies share algorithms trained on huge datasets, thus helping startups to build state-of-the-art systems on several use cases with little 


# word embedding
Approaches taking this view are called word embedding methods, as the goal is to “embed” the words into some vector space.

TODO 删
```
You might be thinking that we have already solved this problem in Sec- tion 2.7 when we discussed Latent Semantic Analysis. One side effect of the SVD that was performed as part of LSA was indeed the creation of a low- dimensional vector space that each word was implicitly mapped into, but it makes a particular assumption about the definition of what it means for two words to be semantically related. In particular, LSA says two words are se- mantically similar if they occur in similar documents. ESA also exhibits this property, where instead two words are similar if they occur in similar knowl- edge base articles.
But is this the right choice? An alternative definition would be one pro- posed by John Rupert Firth [17] which states:
You shall know a word by the company it keeps.
In essence, this codifies the intuition we teach our children: using “context clues,” we can infer the meaning of an unknown word by the words that surround it in some context. That context may be a window surrounding the word, the sentence it occurs in, or the paragraph that contains it. In LSA and ESA, we take perhaps the broadest possible definition of “context” as that of the entire document, but it arguably makes more sense to limit our definition of context somewhat to match how we ourselves actually learn the meaning of unknown words as we encounter them in written text. We typically do not rely on the entire document to understand a word’s meaning, instead choosing a much more restrictive context window to help our understanding.
```

# 宏观来说，rnn还是一个一个sample地处理，区别在于一个sample内部会分步处理
The state of the RNN is reset between processing two dif- ferent, independent sequences (such as two different IMDB reviews), so you still consider one sequence a sin- gle data point: a single input to the network. What changes is that this data point is no longer processed in a single step; rather, the network internally loops over sequence elements.

ReLU比sigmoid好的原因是sigmoid在左右两侧大部分点的导数为0，not learn


