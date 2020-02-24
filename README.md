## 第二章 网络请求
### urllib库
- urllib库  
向指定的浏览器发送一个请求，可以返回数据
- **urlopen函数**  
在urllib.request模块  
``` python
from urllib import request  
res = request.urlopen("http://www.baidu.com")
print(res.read())
```  
参数：  
&ensp;url:请求的url  
&ensp;data:默认为None，GET方式，设置变为POST方式  
返回值:是一个http.client.HTTPResponse对象  
返回值方法:read(size),readline,rendlines,getcode  

-----  
- **urlretrieve函数**  
下载网页中的文件  
```python
from urllib import request
request.urlretrieve('http://www.baidu.com/','baidu.html')
## 第二个参数是文件下载到那个路径
```  
- **urlencode函数**  
编码函数  
```python  
from urllib import parse
params = {'name':'张三','age':10,'great':'hello,world'}
result=parse.urlencode(params)
print(result)
```  
- **parse_qs函数**  
解码函数  
```python  
result2 = parse.parse_qs(result)
```  
- **urlparse 和 urlsplit**  
有时候拿到一个url，可将url中各个部分进行分割  
```python
from urllib import parse
url = 'htttp://www.baidu.com/s?wd=hfihhfis'
result = parse.urlparse(url)
print(result.scheme/netloc/path/params/query/fragment)
```
**urlsplit和上面基本一样，只是返回没有params**  
-------  
- **request.Request类**  
可以添加请求头  
```python
from urllib import request
headers = {
'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36'
}
req = request.Request("http://www.baidu.com/",headers=headers)
resp = request.urlopen(req)
print(resp.read())
```
------  
- **ProxyHandler处理器（代理设置）  
太多次访问一个网址，可能会被禁止这个IP的访问，就是一个防反爬虫
1.代理的原理：在请求目的服务器之前，先请求代理服务器，然后让代理服务器去请求目的网站，代理服务器拿到目的网站的数据，再转发给我们的代码  
2.http://httpbin.org/io 可以方便我们查看http请求的一些参数  
3.在代码中使用代理    
```python  
from urllib import request
handler = request.ProxyHandler({"http":"218.66.161.88(ip地址):31769(端口)})
opener = request.build_opener(handler)
req = request.Request("http://httpbin.org/io")
resq = opener.open(req)
print(resp.read())
```   
- **cookie**  
1.http是无状态：第一次和服务器连接后并且登陆成功后，第二次请求服务器不知道当前请求是哪个用户  
2.第一次服务器发送一些cookie数据浏览器，第二次发送浏览器会查找相应的cookie给服务器  
3.**cookie的格式：**  
```
Set-Cookie: NAME=VALUE；Expires/Max-age=DATE；Path=PATH；Domain=DOMAIN_NAME；SECURE
```
4.**参数意义**  
 - NAME：cookie的名字。
 - VALUE：cookie的值。
 - Expires：cookie的过期时间。
 - Path：cookie作用的路径。
 - Domain：cookie作用的域名。
 - SECURE：是否只在https协议下起作用。  
------  
- **cookielib和HTTPCookieProcessor模拟登录**  
```python
from urllib import request
wan_url='https://github.com/WanTLin'
headers={
    'User-Agent':"***",
    "Cookie":"***"
}
resp=request.Request(wan_url,headers=headers)
req = request.urlopen(resp)
with open('wangit.html','w',encoding='utf-8') as fp:
    fp.write(req.read().decode('utf-8'))
```
-------  
- **http.cookiejar模块**  
```python
from urllib import request
from urllib import parse
from http.cookiejar import CookieJar

headers = {
    'User-Agent':"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
}
def get_opener():
    #1.登录
    #1.1 创建一个cookiejar对象
    cookiejar = CookieJar()
    #1.2 使用cookiejar创建一个HTTPCookieProcessor对象
    handler = request.HTTPCookieProcessor(cookiejar)
    #1.3 使用上一步创建的handler创建一个opener
    opener = request.build_opener(handler)
    return opener


def login(opener):
    #1.4 使用opener发送登录的请求（邮箱和密码）
    data = {
    "phone_num": '15521301448',
    "password": 'lin123456'
    }
    login_url='https://www.zhihu.com/signin?next=%2F'
    req = request.Request(login_url,headers=headers,data=parse.urlencode(data).encode('utf-8'))
    opener.open(req)
def visit(opener):
    #2.访问个人主页
    wan_url='https://www.zhihu.com/people/xiao-ji-30-70-25'
    # 获取个人主页的页面时候，不要新建一个opener,而应该使用原来的opener,里面包含cookjar
    req = request.Request(wan_url,headers=headers)
    resp = opener.open(req)
    with open('gitwan.html','w',encoding='utf-8') as fp:
        fp.write(resp.read().decode('utf-8'))
if __name__ == '__main__':
    opener = get_opener()
    login(opener)
    visit(opener)
```
