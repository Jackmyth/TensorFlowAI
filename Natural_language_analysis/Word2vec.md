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

