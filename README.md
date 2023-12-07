# 0-9
<h1>动漫花园爬虫</h1>
<pre>
    <code>
          import requests
from bs4 import BeautifulSoup
from lxml import etree

inp = input('输入搜索动漫内容')
cout = input('数量')

header = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/53'
}
url = 'https://dmhy.iwiki.icu/topics/list?keyword={}'.format(inp)
resp = requests.get(url,headers=header)

tree = etree.HTML(resp.text)
a = tree.xpath('//td[@class="title"]/a/@href')
f = []
for i in a:
    b = 'https://dmhy.iwiki.icu'+i
    f.append(b)
    # print(b)
if int(cout) <= len(f):
    for n in f[0:int(cout)]:
        res = requests.get(n)
        tree2 = etree.HTML(res.text)
        c = tree2.xpath("//div[@id='tabs-1']/p/a/@href")
        d = tree2.xpath("//div[@class='topic-title box ui-corner-all']/h3/text()")
        s = 7
        for r in c:
            if s%7 == 0:
                print(d)
            print(r)
            s += 1
        print('=========================================')
        print('=========================================')
else:
    print('爬取数量太大')
        # for u in range(min(len(d),len(c))):
        #     try:
        #         print(d[u])
        #         print(c[u])
        #     except:
        #         print('')
