[![PyPI - Version](https://img.shields.io/pypi/v/gpt-web-crawler)](https://pypi.org/project/gpt-web-crawler/) [![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/Tim-Saijun/gpt-web-crawler/python-publish.yml)](https://github.com/Tim-Saijun/gpt-web-crawler/actions/workflows/python-publish.yml)[![PyPI - License](https://img.shields.io/pypi/l/gpt-web-crawler)](https://pypi.org/project/gpt-web-crawler/)   [![Static Badge](https://img.shields.io/badge/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-8A2BE2)](README-Zh.md) [![Static Badge](https://img.shields.io/badge/English-blue)](README.md)

## 介绍
GPT-Web-Crawler是一个基于python和puppeteer的网络爬虫，可以爬取网页并从网页中提取内容（包括网页的标题，url，关键词，描述，所有文本内容，所有图片和截图）。它使用起来非常简单，只需要几行代码就可以用来爬取网页并从网页中提取内容，非常适合对网络爬取不熟悉并希望使用网络爬取从网页中提取内容的人。
![爬虫工作](images/crawler.gif)
爬虫的输出可以是一个json文件，可以很容易地转换为csv文件，导入数据库或构建一个AI代理。
![助手演示](images/assistant_demo.gif)
## 开始
步骤1. 安装包。
```bash
pip install gpt-web-crawler
```
步骤2. 复制config_template.py并将其重命名为config.py。然后，编辑config.py文件以配置openai api密钥和其他设置，如果你需要使用ProSpider帮助你从网页中提取内容。如果你不需要使用ai帮你从网页中提取内容，你可以保持config.py文件不变。

步骤3. 运行以下代码启动一个爬虫。
```python
from gpt_web_crawler import run_spider,NoobSpider
run_spider(NoobSpider, 
           max_page_count= 10 ,
           start_urls="https://www.jiecang.cn/", 
           output_file = "test_pakages.json",
           extract_rules= r'.*\.html' )
```
## 爬虫
在上面的代码中，使用了NoobSpider。 此包中共有四种爬虫，它们可以从网页中提取的内容有所不同。 下表显示了它们之间的差异。

| 爬虫类型   | 描述                                            | 返回内容                                             |
|------------|------------------------------------------------|------------------------------------------------------|
| NoobSpider | 抓取基本的网页信息                              | - title <br>- URL <br>- keywords <br>- description <br>- body ：网页的所有文本内容 |
| CatSpider  | 抓取带有截图的网页信息                          | - title <br>- URL <br>- keywords <br>- description <br>- body ：网页的所有文本内容 <br>- screenshot_path：截图路径 |
| ProSpider  | 抓取基本信息的同时使用 AI 提取内容              | - title <br>- URL <br>- keywords <br>- description <br>- body ：网页的所有文本内容 <br>- ai_extract_content：GPT 提取的正文文本 |
| LionSpider | 抓取基本信息的同时提取所有图片                  | - title <br>- URL <br>- keywords <br>- description <br>- body ：网页的所有文本内容 <br>- directory：网页上所有图片的目录     |

### Cat Spider
Cat spider是一个可以对网页进行截图的爬虫。它基于Noob spider，并使用puppeteer模拟浏览器操作对整个网页进行截图并将其保存为图像。 所以当你使用Cat spider时，你需要先安装puppeteer。可以先参照[此回答](https://github.com/Tim-Saijun/gpt-web-crawler/commit/dd4edfe83209026a0e74dae8b9b3e6d5d9b9d90c#commitcomment-146072110)安装npm后，再使用以下命令安装puppeteer：
```bash
npm install puppeteer
```
## 待办事项
- [ ] 支持无需配置config.py
