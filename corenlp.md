# corenlp

# corenlp 安装
export CLASSPATH=/Users/yinhang/dev/tools/stanford-corenlp-full-2018-10-05/stanford-corenlp-3.9.2.jar:/Users/yinhang/dev/tools/stanford-corenlp-full-2018-10-05/stanford-corenlp-3.9.2-models.jar:/Users/yinhang/dev/tools/stanford-corenlp-full-2018-10-05/stanford-chinese-corenlp-2018-10-05-models.jar
echo "the quick brown fox jumped over the lazy dog" > input.txt
java -Xmx3g edu.stanford.nlp.pipeline.StanfordCoreNLP -outputFormat json -file input.txt

大多数问题都可以通过java -Xmx16g edu.stanford.nlp.pipeline.StanfordCoreNLP -annotators tokenize -file input.txt或java -Xmx16g edu.stanford.nlp.pipeline.StanfordCoreNLP -props StanfordCoreNLP-chinese.properties -annotators tokenize-file input.txt解决，前一个是英文，后一个是中文。不同的问题在-annotators后面添加标注器的名字就可以，比如中文命名体识别，可以用java -Xmx16g edu.stanford.nlp.pipeline.StanfordCoreNLP -props StanfordCoreNLP-chinese.properties -annotators tokenize,ssplit,pos,lemma,ner -file input.txt，注释器有依赖，ner前面必须先有tokenize,ssplit,pos,lemma。

https://stanfordnlp.github.io/CoreNLP/cmdline.html

https://blog.csdn.net/thriving_fcl/article/details/76595253

