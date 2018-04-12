# Word2vec研究

## [自然語言處理入門- Word2vec小實作](https://medium.com/pyladies-taiwan/%E8%87%AA%E7%84%B6%E8%AA%9E%E8%A8%80%E8%99%95%E7%90%86%E5%85%A5%E9%96%80-word2vec%E5%B0%8F%E5%AF%A6%E4%BD%9C-f8832d9677c8)


利用Python实现wiki中文语料的word2vec模型构建

https://www.jianshu.com/p/ec27062bd453

http://blog.fukuball.com/ru-he-shi-yong-jieba-jie-ba-zhong-wen-fen-ci-cheng-shi/

hanziconv 0.3.2

https://pypi.python.org/pypi/hanziconv


# 將文字資料轉成文字檔
python3 wiki_to_txt.py zhwiki-20180401-pages-articles-multistream.xml.bz2


## [OpenCC軟體](https://bintray.com/package/files/byvoid/opencc/OpenCC)

## [opencc文字轉換]https://xubodoublelife.blogspot.tw/2017/08/google-wored2vec.html

cmd 到opencc軟體目錄下

簡體中文轉繁體中文，大概十分鐘就可以簡轉繁體字OK

opencc -i wiki_texts.txt -o wiki_zh_tw.txt -c s2tw.json

![image](https://github.com/Jackmyth/TensorFlowAI/blob/master/pic/Word2vec/1.jpg)

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
