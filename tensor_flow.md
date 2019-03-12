# tensor flow

# tensorflow服务器报错ImportError: /lib64/libc.so.6: version `GLIBC_2.XX' not found
wget https://ftp.gnu.org/gnu/glibc/glibc-2.17.tar.gz
tar -xzvf glibc-2.17.tar.gz
cd glib-2.17
mkdir build
cd build
../configure --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin
make
make install
ldd --version


# keras加载之后 predict 报错 tensor is not an element of this graph

```python
def load_model():
	global model
	model = ResNet50(weights="imagenet")
            # this is key : save the graph after loading the model
	global graph
	graph = tf.get_default_graph()

# While predicting, use the same graph

    with graph.as_default():
	preds = model.predict(image)
	#... etc
    
    
    
    
    
from keras.models import load_model
import tensorflow as tf

global graph
graph = tf.get_default_graph()

global symptom_model
global diagnosis_model

symptom_model = load_model("data/symptom.bin")
diagnosis_model = load_model("data/diagnosis.bin")

```

# 注意，keras的target要从0开始编码，使用sparse_categorical_crossentropy，
可用 keras.utils.to_categorical 试验


# framework
```python
with tf.name_scope("placeholders"):
  ...
  ...
  
with tf.name_scope("model_inner"):
  ...
  
with tf.name_scope("output"):
  ...
  
with tf.name_scope("loss"):
  ...
  
with tf.name_scope("optim"):
  train_op = tf.train....minimize(l)
  
with.tf.name_scope("summaries"):
  tf.summary.scalar("loss", l)
  merged = tf.summary.merge_all()
  

train_writer = tf.summary.FileWriter("", tf.get_default_graph())

with tf.Session() as sess:
  sess.run(tf.global_variables_initializer())
  for epoch in ...:
    feed_dict = {...}
    _, summary, loss = sess.run([train_op, merged, l])
    train_writer.add_summary(summary, step)
    
  pred = sess.run(y_pred, feed_dict={...})
```
