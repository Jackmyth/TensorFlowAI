# Scrapy專案
安裝 Twisted-17.9.0-cp35-cp35m-win_amd64.whl，就可以安裝scrapy

http://nukc.listenlite.com/2017/04/19/install-scrapy-VC-14-0-is-required/

https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted

在裝完Twisted-17.9.0-cp35-cp35m-win_amd64之後Python3也可以執行Python Scrapy

pip3 install Twisted-17.9.0-cp35-cp35m-win_amd64.whl

pip3 install scrapy

pip3 install beautifulsoup4

pip3 install pypiwin32

首先建立專案：

scrapy startproject ptt

scrapy crawl ptt

最後執行以下指令，就可以把文章存成 JSON 或Excel 檔案：

scrapy crawl ptt -o ptt.json

scrapy crawl ptt -o ptt.csv
