- 发送GET请求:  
1.发送一个简单的get请求:  
```python
response = requests.get("http://baidu.com")
```  
2.添加headers和查询参数  
```python
import requests
headers = {"User-Agent":"***"}
kw={"wd":"中国"}
response = requests.get("http://www.baidu.com/s",params=kw,headers=headers)
print(type(response.text))#返回str类型，requests自动解码，可能乱码
print(response.text)
print(type(response.content))#返回byte类型
print(response.content.decode('utf-8'))
print(response.url)
print(response.encoding)
print(response.status_code)
```  
- **发送POST请求**  
1.基本方法：
```python
response = requests.post(url,data=data)
```
2.实例：  
```python
import requests
url = "***"
data={
    "first": "true",
    "pn": "1",
    "kd": "python"
}
headers = {
    'Referer':'***',
    'User-Agent': '***',
    'Host': 'www.lagou.com'
}
response = requests.post(url,data=data,headers=headers)
print(response.json())#可以将数据转换为json形式
print(response.text)
```  
- 使用代理proxies  
```python 
import requests
url = "http://httpbin.org/ip"
proxy = {
    'http':'http://222.95.240.164:3000'
}
response = requests.post(url,proxies=proxy)
print(response.text)
```
