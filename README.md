## 第二章 网络请求
### urllib库
- urllib库  
向指定的浏览器发送一个请求，可以返回数据
- **urlopen函数**  
在urllib.request模块  
``` 
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
```
from urllib import request
request.urlretrieve('http://www.baidu.com/','baidu.html')
## 第二个参数是文件下载到那个路径
```  
- **urlencode函数**  
编码函数  
```  
from urllib import parse
params = {'name':'张三','age':10,'great':'hello,world'}
result=parse.urlencode(params)
print(result)
```  
- **parse_qs函数**  
解码函数  
```  
result2 = parse.parse_qs(result)
```  
- **urlparse 和 urlsplit**  
有时候拿到一个url，可将url中各个部分进行分割  
```
from urllib import parse
url = 'htttp://www.baidu.com/s?wd=hfihhfis'
result = parse.urlparse(url)
print(result.scheme/netloc/path/params/query/fragment)
```
**urlsplit和上面基本一样，只是返回没有params**  
- **request.Request类**  
可以添加请求头

