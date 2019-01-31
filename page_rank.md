# page rank

transition matrix, mij = 1/k, 如果j节点有k个向外的边，并且其中一个边连接i节点
一个随机的网虫出于节点j的概率，1...n, 组成一个向量，节点j的概率就是节点j的page rank

sparse matrix，表示用
source degree destinations 的表
A 3 B,C,D
B 2 A,D
C 1 A
D 2 B,C

处理dead end的方法
- recursively delete dead ends, dead end的page rank等于直接predecessor的page rank的加权平均
- taxation, 允许网虫下一步跳转到随机页面，而不一定完全按照out link跳转，beta参数一般为0.8到0.9， v' = beta * M * v + (1-beta)*e/n

topic sensitive
v' = beta * M * v + (1-beta)*e*s/|S|    s中元素节点属于S时为1，否则为0   S: teleport set

解决link spam的方法
1. 发现spam farm, 但是变种太多
2. trust rank，使用topic sensitive，teleport set为高信誉的页面
3. spam mass, 县算普通的page rank r，再算trust rank t，spam mass的值为(r-t)/r，越接近1，说明越可能是spam

If I is a set of items, the support for I is the number of baskets for which I is a subset
association rule is that if all of the items in I appear in some basket, then j is “likely” to appear in that basket as well.
confidence of the rule I→jtobetheratioofthesupportforI∪{j}tothesupportforI. Thatis, the confidence of the rule is the fraction of the baskets with all of I that also contain j.

define the interest of an association rule I → j to be the difference between its confidence and the fraction of baskets that contain j

It is the job of the A-Priori Algorithm and related algorithms to avoid counting many triples or larger sets, and they are, as we shall see, effective in doing so
The A-Priori Algorithm is designed to reduce the number of pairs that must be counted, at the expense of performing two passes over data, rather than one pass


One manifestation of the “curse” is that in high dimensions, almost all pairs of points are equally far away from one another. Another manifestation is that almost any two vectors are almost orthogonal.
