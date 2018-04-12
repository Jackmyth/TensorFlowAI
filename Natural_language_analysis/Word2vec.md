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



