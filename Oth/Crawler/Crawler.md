

# 第一章 初识爬虫

## 3. 第一个爬虫程序

```python {.line-numbers}
from urllib.request import urlopen

url = "http://www.baidu.com"
resp = urlopen(url)

##print(resp.read().decode("utf-8"))

with open("mybaidu.html",mode='w') as f:
    f.write(resp.read().decode("utf-8"))
print("over!")

```



## 4. Web 请求解析

1. 服务器渲染：在服务器那边直接把数据和html整合在一起，统一返回给浏览器在页面源代码中能看到数据
2. 客户端渲染：第一次请求只要一个html骨架，第二次请求拿到数据，进行数据展示在页面代码中，看不到数据

熟练使用浏览器抓包工具

---

## 5. HTTP协议

![](2021-11-24-16-56-23.png)


![](2021-11-24-16-55-06.png)


请求方式：

    GET:显示提交（查询东西）
    POST：隐示提交（输入、修改东西）


---

## 6. Requests入门

安装requests
pip install requests

### Requests 01 案例 搜狗浏览器

```python {.line-numbers}
import requests

url = 'https://www.sogou.com/web?query=周杰伦'

headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36"    
}

resp = requests.get(url, headers = headers) #处理一个小小的反爬

print(resp)
print(resp.text) #拿到网页源代码

```


```python {.line-numbers}
import requests

query = input("输入一个你喜欢的明星")
url = f'https://www.sogou.com/web?query={query}' #f 在一段字符中插入

headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36"    
}

resp = requests.get(url, headers = headers) #处理一个小小的反爬

print(resp)
print(resp.text) #拿到网页源代码

```

### Requests 02 案例 百度翻译

```python {.line-numbers}
import request 

url = "https://fanyi.baidu.com/sug"

s = input("请输入你要翻译的英文单词")
data = {
    "kw": s
}

# 发送post请求， 发送的数据必须放在字典中，通过data参数进行传递
resp = requests.post(url, data=data)
print(resp.json())  # 将服务器返回的内容直接处理成json() => dict

```

### Requests 03 案例 豆瓣排行榜

```python {.line-numbers}
import requests

url = "https://movie.douban.com/j/chart/top_list"

header = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36"
}

# 重新封装参数
params = {

    "type": "24",
    "interval_id": "100:90",
    "action":"",
    "start": 0,
    "limit": 20,
}

resp = requests.get(url ,headers= header, params= params)

#print(resp.text)
#print(resp.json())
#print(resp.request.headers)

resp.close() # 使用完之后关掉resp 否则会被服务器拒绝访问

```

---


# 第二章 数据解析与提取

## 1.数据解析概述

在上一章中，我们基本上掌握了抓取整个网页的基本技能。但是大多数情况下，我们并不需要整个网页的内容，只是需要那么一小部分，怎么办呢？ 这就涉及到了数据提取的问题。

本课程中，提供三种解析方式：

1. re解析
2. bs4解析
3. xpath解析

这三种方式可以混合进行使用，完全以结果做导向，只要能拿到你想要的数据，用什么方案并不重要。当你掌握了这些之后，再考虑性能的问题。

---

## 2.正则表达式

Regular Expression 正则表达式，一种使用表达式的方式对字符串进行匹配的语法规则

我们抓取到的网页源代码本质上就是一个超长的字符串，想从里面提取内容。用正则再合适不过了。

正则的优点：速度快，效率高，准确性高
正则的缺点：新手上手难度有点儿高。

不过只要掌握了正则编写的逻辑关系，写出一个提取页面内容的正则其实并不复杂

正则的语法：使用元字符进行排列组合用来匹配字符串 在线测试正则表达式https://tool.oschina.net/regex/

元字符：具有固定含义的特殊符号
常用元字符：



>1 $\quad$. $\quad\;$ 匹配除换行符以外的任意字符
>2 $\quad$\w $\quad$匹配字母或数字或下划线
>3 $\quad$\s $\quad$匹配任意的空白符
>4 $\quad$\d $\quad$匹配数字
>5 $\quad$\n $\quad$匹配一个换行符
>6 $\quad$\t $\quad$匹配一个制表符
>7
>8 $\quad$^ $\quad$匹配字符串的开始
>9 $\quad$\$ $\quad$匹配字符串的结尾
>10 $\quad$
>11 $\quad$ \W $\quad$匹配非字母或数字或下划线
>12 $\quad$ \D $\quad$匹配非数字
>13 $\quad$ \S $\quad$匹配非空白符
>14 $\quad$ a|b $\quad$匹配字符a或字符b
>15 $\quad$ () $\quad$匹配括号内的表达式，也表示一个组
>16 $\quad$ [...]$\quad$匹配字符组中的字符
>17 $\quad$ [^...]$\quad$匹配除了字符组中字符的所有字符

量词：控制前面的元字符出现的次数

>1$\quad$*$\quad$重复零次或更多次
>2$\quad$+$\quad$重复一次或更多次
>3$\quad$？$\quad$重复一次或更多次
>4$\quad${n}$\quad$重复n次
>5$\quad${n,}$\quad$重复n次或更多次
>6$\quad${n,m}$\quad$重复n到m次

贪婪匹配和惰性匹配

>1$\quad$.\*$\quad$贪婪匹配（与惰性相反）
>2$\quad$.\*?$\quad$惰性匹配（匹配某俩表达式最短距离）

爬虫用的最多的就是惰性匹配。

惰性匹配：
![](2021-11-24-19-43-49.png)
贪婪匹配：
![](2021-11-24-19-44-18.png)

---

## 3.re模块

那么接下来的问题是，正则我会写了，怎么在python程序中使用正则呢？答案是re模块

re模块中我们只需要记住这么几个功能就足够我们使用了。

1. findall 查找所有. 返回list
   > 1 lst = re.findall("m","mai le fo len, mai ni mei!")
   2 print(lst) # ['m', 'm', 'm']
   3 lst = re.findall(r"\d+", "5点之前. 你要给我5000万")
   4 print(lst) # ['5', '5000']

2. search 会进行匹配. 但是如果匹配到了第一个结果. 就会返回这个结果. 如果匹配不上search返回的则是None
   ```python {.line-numbers}
   ret = re.search(r'\d', '5点之前. 你要给我5000万').group()
   print(ret)   #5
   ```

3. match 只能从字符串的开头进行匹配
   ```python {.line-numbers}
   ret = re.match('a', 'abc').group()
   print(ret)   # a
   ```

4. finditer, 和findall差不多. 只不过这时返回的是迭代器(重点)
   ```python {.line-numbers}
   it = re.finditer("m", "mai le fo len, mai ni mei!")

   for el in it:
       print(el.group())    # 依然需要分组
   ```

5. compile() 可以将一个长长的正则进行预加载. 方便后面的使用
   ```python {.line-numbers}
   obj = re.compile(r'\d{3}')   # 将正则表达式编译成为一个 正则表达式对象，规则要匹配的是3个数字
   ret = obj.search('abc123eeee')   # 正则表达式对象调用search，参数为待匹配的字符串
   print(ret.group())   # 结果：123
   ```

6. 正则中的内容如何单独提取？
    单独获取到正则中的具体内容可以给分组起名字
    ```python {.line-numbers}
    s="""
    <div class='西游记'><span id='10010;'>中国联通</span></div>
    """
    obj = re.compile(r"<span id='(?P<id>\d+)'>(?P<name>\w+)</span>",re.S) # re.S 让. 能匹配换行符/?P<xx>组名 把\d+匹配到的值赋予它
    # (?P<分组名字>正则) 可以单独从正则匹配的内容中进一步提取内容

    result = obj.search(s)
    print(result.group())   # 结果：<span id='10010'>中国联通</span>
    print(result.group("id"))   # 结果：10010 # 获取id组的内容
    print(result.group("name")) # 结果：中国联通 # 获取name组的内容
    ```
    这里可以看到我们可以通过使用分组. 来对正则匹配到的内容进一步的进行筛选.

关于正则. 还有一个重要的小点也非常的简单，在本节中就不继续扩展了，下一借的案例中会把这个小点进行简单的介绍。

 
















