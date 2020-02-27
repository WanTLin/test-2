## xpath语法和lxml模块  
### Xpath语法  
- **选取节点**  
1. nodename:选取所有的节点  
2. /：最前面为根节点，否则就是从这个节点的下一个节点  
3. //：从全局节点中选取节点，随便哪一个节点  
4. @：选取某个节点的属性  
- **谓语**  
1. /bookstore/book[1]:选取book的第一个元素  
2. ........../book[last()]:倒数第二个元素  
3. ........../book[position()>3]:前面两个元素  
4. ........../book[@price]:有某个属性 
5. ........../book[@price=10]:有某个属性有特定值  
6. 模糊匹配：//body//div[contains(@class,"lg_tbar")]  
- **通配符**  
1.*：匹配任意节点
2. @*：匹配任意属性  
- **选取多个路径**
例子：//a[@class="weibo"]|//a[@class="wechat"]  
- **运算符**  
- **lxml库**  
一个html/xml的解析器，解析和提取  
1.基本使用：  
1）解析字符串：  
```python
from lxml import etree
html = etree.HTML(text)
result = etree.tostring(html,encoding='utf-8').decode('utf-8')   
```  
2)解析文件html：  ('lxml.etree.parse'方法默认的解释器是xml的，解析html可能会出错，这时候就要自己构造一个html解释器）
```python
    parser =  etree.HTMLParser(encoding='utf-8') 
    html = etree.parse('wanzhihu.html',parser=parser)
    result = etree.tostring(html,encoding='utf-8').decode('utf-8')
    print(result) 
```  
-**在lxml中使用xpath语法**  
```python
    html = etree.parse('tencent.html')
    uls=html.xpath("//ul") #返回一个列表
    for ul in uls:
        print(etree.tostring(ul,encoding='utf-8').decode('utf-8'))
```  




 
