# map reduce

The Map function takes an input element as its argument and produces zero or more key-value pairs
The associative property is closely related to the commutative property. The associative property of an expression containing two or more occurrences of the same operator states that the order operations are performed in does not affect the final result, as long as the order of terms doesn't change. In contrast, the commutative property states that the order of the terms does not affect the final result.

As soon as the Map tasks have all completed successfully, the key-value pairs are grouped by key, and the values associated with each key are formed into a list of values.
Each key that is output by a Map task is hashed and its key-value pair is put in one of r local files. Each file is destined for one of the Reduce tasks.1

The Reduce function’s argument is a pair consisting of a key and its list of associated values.

matrix-vector and matrix-matrix calculations fit nicely into the MapReduce style of computing. Another important class of operations that can use MapRe- duce effectively are the relational-algebra operations.


 we can divide the matrix into vertical stripes of equal width and divide the vector into an equal number of horizontal stripes, of the same height. Our goal is to use enough stripes so that the portion of the vector in one stripe can fit conveniently into main memory at a compute node.
 
 
 
# map reduce 机制
1. 输入到map的数据可以看作k，v（即使某些时候用不上k），reduce的输出数据也是k，v。
   这样做的原因是多个map reduce process的流水组合
   
2. map的输出是k,v的list： (w1, 1), (w2, 1), (w3, 1) ...  wi可能等于wj
3. 当所有的map任务完成之后，grouping is performed by the system.（master controller）
   相同wi的数据分配给一个reduce function。具体怎么分配，可以由用户指定hash function （0..r-1），把某个
   key hash到某个reducer。
4. reduce的输入是 (wi, [v1,v2,...,vn]) v1到vn是对应与wi的所有value
