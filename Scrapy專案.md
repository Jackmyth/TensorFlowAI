# Scrapy專案

首先建立專案：

scrapy startproject ptt

scrapy crawl ptt

最後執行以下指令，就可以把文章存成 JSON 或Excel 檔案：

scrapy crawl ptt -o ptt.json

scrapy crawl ptt -o ptt.csv
