# Word2vec研究

## [自然語言處理入門- Word2vec小實作](https://medium.com/pyladies-taiwan/%E8%87%AA%E7%84%B6%E8%AA%9E%E8%A8%80%E8%99%95%E7%90%86%E5%85%A5%E9%96%80-word2vec%E5%B0%8F%E5%AF%A6%E4%BD%9C-f8832d9677c8)


利用Python实现wiki中文语料的word2vec模型构建

https://www.jianshu.com/p/ec27062bd453

http://blog.fukuball.com/ru-he-shi-yong-jieba-jie-ba-zhong-wen-fen-ci-cheng-shi/


# 將文字資料轉成文字檔
python3 wiki_to_txt.py zhwiki-20180401-pages-articles-multistream.xml.bz2


## [OpenCC軟體](https://bintray.com/package/files/byvoid/opencc/OpenCC)

## [opencc文字轉換](https://xubodoublelife.blogspot.tw/2017/08/google-wored2vec.html)

cmd 到opencc軟體目錄下

簡體中文轉繁體中文，大概十分鐘就可以簡轉繁體字OK

opencc -i wiki_texts.txt -o wiki_zh_tw.txt -c s2tw.json

![image](https://github.com/Jackmyth/TensorFlowAI/blob/master/pic/Word2vec/1.jpg)

segment.py
```
# -*- coding: utf-8 -*-

import jieba
import logging

def main():

    logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

    # jieba custom setting.
    jieba.set_dictionary('jieba_dict/dict.txt.big')

    # load stopwords set
    stopword_set = set()
    with open('jieba_dict/stopwords.txt','r', encoding='utf-8') as stopwords:
        for stopword in stopwords:
            stopword_set.add(stopword.strip('\n'))

    output = open('wiki_seg.txt', 'w', encoding='utf-8')
    with open('wiki_zh_tw.txt', 'r', encoding='utf-8') as content :
        for texts_num, line in enumerate(content):
            line = line.strip('\n')
            words = jieba.cut(line, cut_all=False)
            for word in words:
                if word not in stopword_set:
                    output.write(word + ' ')
            output.write('\n')

            if (texts_num + 1) % 10000 == 0:
                logging.info("已完成前 %d 行的斷詞" % (texts_num + 1))
    output.close()

if __name__ == '__main__':
    main()

```

jieba詞句分類訓練完，會放在C:\Users\user\AppData\Local\Temp\目錄下

Dumping model to file cache

C:\Users\user\AppData\Local\Temp\jieba.u66390701b34e88b423504063f6edd622.cache

```
Building prefix dict from E:\Jack Program\Python\Word2Vec\zake7749\word2vec-tutorial-master\jieba_dict\dict.txt.big ...
2018-04-12 19:09:04,746 : DEBUG : Building prefix dict from E:\Jack Program\Python\Word2Vec\zake7749\word2vec-tutorial-master\jieba_dict\dict.txt.big ...
Dumping model to file cache C:\Users\user\AppData\Local\Temp\jieba.u66390701b34e88b423504063f6edd622.cache
2018-04-12 19:09:06,163 : DEBUG : Dumping model to file cache C:\Users\user\AppData\Local\Temp\jieba.u66390701b34e88b423504063f6edd622.cache
Loading model cost 1.553 seconds.
2018-04-12 19:09:06,307 : DEBUG : Loading model cost 1.553 seconds.
Prefix dict has been built succesfully.
2018-04-12 19:09:06,311 : DEBUG : Prefix dict has been built succesfully.
2018-04-12 19:11:24,579 : INFO : 已完成前 10000 行的斷詞
2018-04-12 19:13:10,795 : INFO : 已完成前 20000 行的斷詞
2018-04-12 19:14:45,776 : INFO : 已完成前 30000 行的斷詞
2018-04-12 19:16:10,655 : INFO : 已完成前 40000 行的斷詞
2018-04-12 19:17:33,636 : INFO : 已完成前 50000 行的斷詞
2018-04-12 19:18:53,623 : INFO : 已完成前 60000 行的斷詞
2018-04-12 19:20:14,800 : INFO : 已完成前 70000 行的斷詞
2018-04-12 19:21:35,767 : INFO : 已完成前 80000 行的斷詞
2018-04-12 19:22:48,834 : INFO : 已完成前 90000 行的斷詞
2018-04-12 19:24:04,740 : INFO : 已完成前 100000 行的斷詞
2018-04-12 19:25:14,925 : INFO : 已完成前 110000 行的斷詞
2018-04-12 19:26:19,368 : INFO : 已完成前 120000 行的斷詞
2018-04-12 19:27:33,116 : INFO : 已完成前 130000 行的斷詞
```
![image](https://github.com/Jackmyth/TensorFlowAI/blob/master/pic/Word2vec/2.jpg)

train.py

```
# -*- coding: utf-8 -*-

import logging

from gensim.models import word2vec

def main():

    logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
    sentences = word2vec.LineSentence("wiki_seg.txt")
    model = word2vec.Word2Vec(sentences, size=250)

    #保存模型，供日後使用
    model.save("word2vec.model")

    #模型讀取方式
    # model = word2vec.Word2Vec.load("your_model_name")

if __name__ == "__main__":
    main()

```

```
2018-04-12 20:20:24,827 : INFO : EPOCH 5 - PROGRESS: at 81.65% examples, 523616 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:25,864 : INFO : EPOCH 5 - PROGRESS: at 82.31% examples, 522715 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:26,869 : INFO : EPOCH 5 - PROGRESS: at 83.26% examples, 522095 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:27,874 : INFO : EPOCH 5 - PROGRESS: at 84.21% examples, 522292 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:28,866 : INFO : EPOCH 5 - PROGRESS: at 85.18% examples, 522418 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:29,905 : INFO : EPOCH 5 - PROGRESS: at 86.11% examples, 522390 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:30,901 : INFO : EPOCH 5 - PROGRESS: at 86.93% examples, 521987 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:31,913 : INFO : EPOCH 5 - PROGRESS: at 87.73% examples, 522151 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:32,915 : INFO : EPOCH 5 - PROGRESS: at 88.62% examples, 522525 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:33,929 : INFO : EPOCH 5 - PROGRESS: at 89.38% examples, 522647 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:34,921 : INFO : EPOCH 5 - PROGRESS: at 90.12% examples, 522469 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:35,937 : INFO : EPOCH 5 - PROGRESS: at 90.81% examples, 522133 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:36,958 : INFO : EPOCH 5 - PROGRESS: at 91.59% examples, 521720 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:37,966 : INFO : EPOCH 5 - PROGRESS: at 92.34% examples, 521548 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:38,972 : INFO : EPOCH 5 - PROGRESS: at 93.25% examples, 521382 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:40,024 : INFO : EPOCH 5 - PROGRESS: at 94.01% examples, 520895 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:41,030 : INFO : EPOCH 5 - PROGRESS: at 94.78% examples, 520839 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:42,044 : INFO : EPOCH 5 - PROGRESS: at 95.61% examples, 521011 words/s, in_qsize 6, out_qsize 0
2018-04-12 20:20:43,040 : INFO : EPOCH 5 - PROGRESS: at 96.46% examples, 521063 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:44,053 : INFO : EPOCH 5 - PROGRESS: at 97.45% examples, 521194 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:45,065 : INFO : EPOCH 5 - PROGRESS: at 98.31% examples, 521059 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:46,073 : INFO : EPOCH 5 - PROGRESS: at 99.29% examples, 521289 words/s, in_qsize 5, out_qsize 0
2018-04-12 20:20:46,823 : INFO : worker thread finished; awaiting finish of 2 more threads
2018-04-12 20:20:46,838 : INFO : worker thread finished; awaiting finish of 1 more threads
2018-04-12 20:20:46,854 : INFO : worker thread finished; awaiting finish of 0 more threads
2018-04-12 20:20:46,854 : INFO : EPOCH - 5 : training on 78381132 raw words (75356128 effective words) took 144.5s, 521596 effective words/s
2018-04-12 20:20:46,854 : INFO : training on a 391905660 raw words (376781688 effective words) took 842.7s, 447135 effective words/s
2018-04-12 20:20:46,854 : INFO : saving Word2Vec object under word2vec.model, separately None
2018-04-12 20:20:46,854 : INFO : storing np array 'vectors' to word2vec.model.wv.vectors.npy
2018-04-12 20:20:53,034 : INFO : not storing attribute vectors_norm
2018-04-12 20:20:53,034 : INFO : storing np array 'syn1neg' to word2vec.model.trainables.syn1neg.npy
2018-04-12 20:20:58,000 : INFO : not storing attribute cum_table
2018-04-12 20:20:59,523 : INFO : saved word2vec.model

```
![image](https://github.com/Jackmyth/TensorFlowAI/blob/master/pic/Word2vec/3.jpg)

demo.py

```
# -*- coding: utf-8 -*-

from gensim.models import word2vec
from gensim import models
import logging

def main():
	logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)
	model = models.Word2Vec.load('word2vec.model')

	print("提供 3 種測試模式\n")
	print("輸入一個詞，則去尋找前一百個該詞的相似詞")
	print("輸入兩個詞，則去計算兩個詞的餘弦相似度")
	print("輸入三個詞，進行類比推理")

	while True:
		try:
			query = input()
			q_list = query.split()

			if len(q_list) == 1:
				print("相似詞前 100 排序")
				res = model.most_similar(q_list[0],topn = 100)
				for item in res:
					print(item[0]+","+str(item[1]))

			elif len(q_list) == 2:
				print("計算 Cosine 相似度")
				res = model.similarity(q_list[0],q_list[1])
				print(res)
			else:
				print("%s之於%s，如%s之於" % (q_list[0],q_list[2],q_list[1]))
				res = model.most_similar([q_list[0],q_list[1]], [q_list[2]], topn= 100)
				for item in res:
					print(item[0]+","+str(item[1]))
			print("----------------------------")
		except Exception as e:
			print(repr(e))

if __name__ == "__main__":
	main()

```

