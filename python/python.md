==一切皆对象==
封装、类型、多态是面向对象的三大特征
#### 注释
>\#表示注释
>也可以“”“
>
>中间的都是注释，即单行注释
>
>”“”
# 数据
### 数据类型
>[!note]- 数据类型
字符串：str
数字：int float bool complex(4+3j)
列表(list)（有序的可变序列）
元组(tuple)（有序的不可变序列）
集合(set)（无序不重合集合）
字典()（无需Key-Value集合）
特殊的有：
None 表示无或空
布尔 bool
二进制：x=b"Hello" ; y=bytearray(5)
#### 数字
int  float complex bool
bool()函数可以返回True或False，但是绝大多数值都是True，但当bool(False)/bool(0)/bool("")/bool(())/bool(\[\])/bool({})返回的是False
可以自己定义，也可以计算得到，即运用比较运算符得来
#### 字符串string
- 定义：
```python
name=''
name=""
name""" 翟秋凯 """

```
- 对于字符串，==本身相当于一个数组==，支持索引与切片
```python
s="nihaowoshi"
print(s[3])

#切片，格式为 s[左闭索引:右开索引:步长]
s='nihao woshi'
s[:4],结果是niha
s[-4:],结果是oshi
s[::-1],获得反转字符串
```

- 要检查字符串中是否存在某个短语或字符，用关键字 in
```python
txt='The best thing is  free!'
print('free' in txt)  //返回true 或 false

if 'free' in txt:
	print("Yes! 'free' is in txt")
```
- 字符串方法：
```python
a="Hello World !  "
#index方法，查找下标
print(a.index("Wo"))
#全部大写
print(a.upper())
#全部小写
print(a.lower())
#删除前后空格
print(a.strip())
#删除指定的字符，将传入的参数按单个字符处理
print(a.strip("12"))
#替换字符
print(a.replace("H","J"))  #会有返回值
#拆分
print(a.spilt(","))#return ['Hello','World！']，即得到一个列表对象
#统计次数
a.count("a")
#统计字符串长度
a.len()
```

- 要拼接字符串
```python
name="翟秋凯"
print(name+"是"+"帅哥") #直接使用加号不能拼接数字

name="翟秋凯"
name2="小凯"
print("帅哥是%s"%name)
message="帅哥是%s"%name print(message)
message2="帅哥是%s和%s"%(name,name2)
# %表示我要占位,s表示变量变成字符串放入占位的地方
# %s是字符串  %d是整数   %f是浮点数
```
- 另一种是快速格式化
```python
#f"内容{变量}"
name="翟秋凯"
height=180
print(f"我叫{name},我的身高是{height}")
#这种不会控制或改变精度
```
- 要格式化精度控制：m.n
m规定宽度( 很少使用 )
.n就决定精度，小数点后面有n位，并==四舍五入==
```python
%5d  #输入11，输出空格空格空格11
%7.2f  #输入11.345，输出_ _ _ _11.35_
print()
```
- 对表达式进行格式化
	表达式：有明确执行结果的代码语句
```python
print(f"1*1的结果是{1*1}")
print("1*1的结果是%d"%(1*1))
print("1*1的数字类型是%s"%(type(1*1)))
```
#### 列表list
- 最常用的是列表list，用方括号分割，逗号分开
```
s=[1,2,3]
a=['a','b','c']
```
- ==列表允许重复的元素，允许不同的数据类型==
- 索引访问元素：0，1，2为正序，-1，-2，-3为倒数第一个，倒序
	嵌套列表：a\[1\[0\]\]
>[!note]+ 列表的内置函数
>1、 元素 in list 判断元素是否在列表中
2、del list\[1\]  删除元素
2、a.append( ),可以在列表最后添加元素，没有返回值
3、列表名.insert( 序数,元素 ),在列表的指定位置添加元素
4、列表名.pop( ),弹出列表的最后一个元素，返回被删除的元素.如果加上索引值，则删除指定位置的元素
而del无返回值
5、列表名.extennd(列表名),在列表后加另一个列表的所有元素，形参除了列表名，也可以是列表
6、列表名.remove( 元素 ),按值删除元素，只删除第一个出现的，若不存在则抛出错误
7、len(列表名),求列表的长度，即列表的元素个数
8、列表名.reverse(),列表原地逆置
9、sorted(列表名)，获得排序后的列表，但原来的列表并未排序，没有返回值
或者列表名.sort(),让字母数字升序排列
或者列表名.sort(reverse=True),按照降序排列
10、列表名.count(元素)，列表种元素的个数，有返回值
11、列表名.index( 元素 )，返回目标元素首次出现的索引号，若不存在则抛出错误
12、列表名.clear()，清除所有的元素

- 列表推导式
```python
newlist = [espression for item in iterable if condition == True]#返回一个列表
#等价于
iterable=[,,,]
for x in iterables:
	if(condition==True)
		newlist.append(expression())
```
- 复制列表
```python
list1=[1,2,3,4]
list2=list1.copy() // list2=list(list1)
print(list2)
```
#### 元组tuple
==有序，不可更改，只读==。元组用(括号)标识，内部元素用逗号隔开。
- 构造一个元组
```python
a=('',3,"")
a=tuple(('1',2))#！必须要有两个括号才行

#当元组只有一个元素的时候，必须要在这个元素后面加个逗号
t4=("hello",)
```
- 元组方法
```python
tuple[1]              #表示tuple这个元组里第二个元素
print(len(tuple1))    #统计元组元素个数
n=tuple1.count(1)     #查找元组中的特定元素的个数
index=tuple1.index(2) #查找元组中第一个出现的该元素的索引
```
- 更改元组
```python
#将元组改为列表，对列表进行修改后再改为元组
x = ("apple", "banana", "cherry")  
y = list(x)  
y[1] = "kiwi"
x = tuple(y)

# 而当tuole里有个list时，list的元素可以修改
```
- 解包元组
当我们船舰一个tuple时，往往会为其分配值，这称为打包元组。
要将值提取到变量中，称为  解包 
```python
fruits = ("apple", "banana", "cherry") 
(green, yellow, red) = fruits
print(green)  
print(yellow)  
print(red)
```
当变量名小于元组中元素的个数时，可以选择将一个变量加上\*，使其变为一个列表
```python
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")  
(green, yellow, *red) = fruits
print(green)  
print(yellow)  
print(red)
#red=['cherry', 'strawberry', 'raspberry']
```
- 循环元组
```python
for i in range(len(tuple)):
	print(tuple[i])
while index <len(tuple):
	print(tuple[index])
	index+=1
```
- 联接元组
```python
tuple3=tuple1+tuple2
#乘元组
fruits=("apple","banana","laji")
newtuple=fruits*2
print(newtuple)
#['apple', 'banana', 'cherry', 'apple', 'banana', 'cherry')
```
#### 集合set
==无序的集合，没有重复的成员，允许更改，但可以添加新项目==
用大括号书写
值True和1在集合中被视为相同的值
```python
#构造集合
set1=set(('apple',2,'nihao'))
set2=set()  #空集合
#求集合的元素个数
len(set1)
#添加新元素
set1={'apple',2,"nihao"}
set1.add("orange")
#移除元素
set1.remove("orange")
#随机取出一个元素
set1.pop()
#清空集合
set1.clear()
#删除集合
del set1

#返回一个新集合，仅包含了两个集合的重复项
set3=set1.intersection(set2)
#取两个集合的差集，返回值是一个新的集合，不影响到原本的两个集合
set1.difference(set2)   #1有2没有
#消除差集
set1.difference_update(set2)   #在集合1内删除集合2中相同的元素，修改集合1，集合2不变
#两个集合的合并
set2.update(set1)       #修改了set2
set3=set1.union(set1)   #未修改set2
set4=set1.union(set1,set2,set3)
set4=set1|set2|set3
```
- 循环遍历
```python
#只能for循环，因为无索引指示，不能用while
for i in set1:
	print(i)
```
#### 字典dictionary
==无序的对象集合、可更改，不重复==，字典中的元素是通过键来存取的
字典用{ }标识。字典由索引[key]和对应的值value组成
```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

my_dict = {} #定义一个名字为dict的字典
my_dict={key1:value1 , key2:value2,……}
#添加/修改键
my_dict['one'] = "This is one"
my_dict[2] = "This is two"
#输出
print dict['one']          # 输出键为'one' 的值
print dict[2]              # 输出键为 2 的值
x=my_dict.get("noe")       # 另一种方式
print tinydict             # 输出完整的字典
#字典嵌套
myfamily = {"child1":{"name" : "Emil","year":2004},  
  "child2":{"name":"Tobias","year":2007},"child3":{"name":"Linus","year":2011}  
}
#访问：
print(myfamily["cuildren1"]["name"])

#删除元素
my_dict.pop("one")   #有返回值
#清空元素
my_dict.clear()
#获取全部键
keys=my_dict.keys()
#获取全部值
print(my_dict.values())
#复制字典
newdict=dict1.copy()
newdict=dict(dict1)
```
- 输出视图
```python
print(dict.items())
```
#### 通用方法
```python
#排序
list1=[1,4,3,6]
print(f"列表list1排序后是{sorted(list1,reverse=True)}") #从大到小，返回值是列表类型
```
#### 判断数据类型
type( )可判断数据类型，有返回值，需要拿一个东西去接收。
#### 数据类型转换
int( x )  float( x ) str ( x ) 有返回值
int( x ) 将小数直接丢掉小数点的数
# 运算符
// 整除，即求商       %取余数      ** 幂运算，或者pow(a,b,mod)
+=，-=，\*= ， /=   ……
&按位与   |按位或    ^按位异或   ~按位取反   
and与   or或   not非
in在指定序列中找到  not in在指定序列中没找到
is 两个标识是不是引用自一个对象
is not 两个标识是不是引用不同的对象
# 变量
允许一行为多个变量赋值
```python
x,y,z="a","b",10;
```
还允许将列表、元组中的值提取到变量中
```python
fruits = ["apple", "banana", "cherry"]  
x, y, z = fruits  
print(x)  
print(y)  
print(z)
```
- **global**关键字，将在某个局部作用域的变量定义成全局的变量

# 基本语法
#### input
```python
input("")
# 类型转换->
int(input("请输入文本"))
```
#### print
print( )
	直接print()会换行
	不换行print，有print(……,end=' ')，单引号里决定间隔
	以及  \t  这个东西，制表符，直接写在字符串中print("hello/t翟秋凯")
	默认输出是换行的，要想实现不换行需要在变量末尾加上逗号，如
		print x,
		print y
		或者 print x,y
#### if
```python
if 条件1：
	……
elif 条件2:
	……
else：
	……
#当只有一个语句要执行时，可以将其放在与if同行上
if a>b: print("a is greater than b")

#与：and  或：or  非: not 
```
if 语句不能为空，实在没有内容的话加入pass
```python
if b>a:
	pass
```

#### match
```python
match expression:#这个expression可以是变量、字面量、表达式、复杂数据结构
	case x:
		code block1
	case y:
		code block2
	case z:
		code block3
	case _:     #使用下划线_作为最后一个case值
		code block…

或者可以合并case，使用|来进行相当于or的判断
match day:
	case 1|2|3|4|5:
		print("weekday")
	case 6|7:
		print("weekend")

或者可以在case语句中加入if 来进行更一步的判断
month=5
day=4
match day:
	case 1|2|3|4|5 if month==4：
		print("weekday in April")
……
```
#### while
```python
while condintion:
	code block
```
- break 和 continue 任然适用
- 此外，还有else 语句。当condition not true 时，运行else语块
```python
i = 1  
while i < 6:  
  print(i)  
  i += 1  
else:  
  print("i is no longer less than 6")
```
#### for
```python
for 临时变量 in 待处理数据集:
	代码
```
- range语句：
	range(5)=【0，1，2，3，4】
	range(5,10)=【5，6，7，8，9】，不包含10
	range(5,10,2)=【5，7，9】不包含10
- else同样适用
	但是，如果循环语句被( break )停止,或者循环体内出现异常，则不会执行该else语块
```python
for x in range(6):  
  if x == 3: break  
  print(x)  
else:  
  print("Finally finished!")
```

- pass 当for循环里没有内容的时候，用pass
```pyhton
for x in range(8)
	pass
```
# **==函数==**
def关键字
```python
def functionname(cnashuming):
	code block
	return 返回值
```

- 函数的说明文档
	在函数体前三个引号，换行，自动生成。需要你在注释的地方写出函数的功能，各个形参的解释
	
- 函数内部定义的局部变量不会改变外部。
	如果想要在函数内部将全局变量修改：关键字==global==
```python
num=10
def xiugai():
	global num
	num=200
xiugai()
print(num)  #此时num变为了200
```

- 默认参数
```python
def functionname(canshu=1):
	code block
```
如此，调用函数时不传参，即使用默认参数

- 返回值
```python
def add(a,b):
	return a+b,a-b
x,y=add(a,b)
```
如果一个没有返回值的函数被一个变量接受，则这个变量为None类型

- 不知传参数量时
```python
#如果传入的参数数量未知，可以在函数参数名称前加*，以表示函数接受一个参数元组
def my_function(*kids):  
  print("The youngest child is " + kids[2])  
my_function("Emil", "Tobias", "Linus")


#如果关键字参数的数量未知，在参数名称前加**,以表示接受一个字典
```python
def my_function(**kid):  
  print("His last name is " + kid["lname"])
my_function(fname = "Tobias", lname = "Refsnes")
```

- 还可以将列表作为参数传递
```python
def my_function(food):  
  for x in food:  
    print(x)
fruits = ["apple", "banana", "cherry"]  
my_function(fruits)
```

- 函数的嵌套调用->一个函数中调用另一个函数

- lambda函数：适用于编写一些简单一点的函数，但是表达式只能有一句表达式，只能使用一次
```python
x=lambda 参数1，参数2，… : 表达式
```

# 文件操作

### 文件编码
 UTF-8 -> **通用编码**
 GBK
 Big5
### 读取文件
open()函数，可以打开一个已经存在的函数，或创建一个新文件
close()函数，关闭文件
```python
open(mame,mode,encoding)
#name：文件名的字符串，可以包含文件的具体路径
#model: 设置打开文件的方式：r只读、w写入、a追加等
#encoding：编码格式，推荐UTF-8
f=open("D:/测试.txt","r",encoding="UTF-8")
f.close()
```
- 读取方法
```python
f=open("text.txt")
#read()方法
f.read(num)   #num是从文件中读取的数据的长度。不传入即表示读取所有数据
#多次使用read()函数，第二次会在第一次读取的结尾处开始读取

#readlines()方法
#按照行的方式读取所有，返回一个列表，每行数据为列表中的一个元素
#readlines()方法也会受到read()方法的影响
content=f.readlines()
print(content)

#readline方法：一次读取一行内容
content=f.readline()
print(f"第一行:{content}")
content=f.readline()
print(f"第二行:{content}")

#for循环读取文件行
for line in open("python.txt","r"):
	print(line)

#with open()方法，自动close文件以免遗忘
with open("test.txt") as f:
	for line in f:
		print(f"每一行的内容是{line}")
		
```

- 写入方法
```python
f=open("python.txt","w") #文件不存在的话会新建pyhton.txt 文件
#但是，当前文件已经存在，写入会将内容全部清空
f.write("hello world!")  #并未写入，而是更新到缓冲区
f.flush()                #内容写入文件，避免频繁操作硬盘，导致效率下降
f.close()                #f.close()内置flush功能
```

- 追加写入方法
```python
f=open("python.txt","a")
f.write("\nHello World!")  #\n是换行输入
f.flush()
f.close()
```


# 异常(bug)、模块、包
### 捕获异常：对可能出现的bug提前准备、提前处理
基本语法：
```python
#捕获异常
try:
	可能发生错误的代码
except:
	如果出现异常 执行的代码

#捕获指定的异常
try:
	balabala
except NameError as e:  #e类似于是临时变量
	print("出现了变量未定义的错误")   #只捕获NameError的异常
	print(e)

#捕获多个异常
try:
	balabala
except (NameError,ZeroDivisionError) as e:
	print("出现了变量未定义或除以0的异常")

#捕获所有的异常
try:
	balabala
except Exception as e:
	print("出现异常")

#未发生异常：else ; 无论如何都要执行：finally
try:
	bala
except:
	bala
else:
	print("未发生异常")
finally:
	print("我肯定执行了")
	f.close()
```

### 异常的传递
基于函数的调用方式，异常一级一级传递，可以在最顶级的函数中捕获异常

### 模块
#### 模块导入
模块就是一个python文件，以.py结尾。模块能定义函数、类、变量或可执行的代码
```python
[from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as 别名]
import 模块名1,模块名2     #用模块里的所有的功能
from 模块名 import 功能名  #只用一种功能
from time import *       #使用所有的功能，其在后续使用的时候不用加time.，直接sleep()就可以了

import time as t
t.sleep()
```

#### 自定义模块
```python
#my_model1.py
def test(a,b):
	print(a,b)

#test.py
import my_model1
my_model1.test(10,20)
```
- main变量—在py文件中添加一些测试信息：
```python
#model1.py
def test(a,b):
	print(a+b)

if __name__=="__main__":    #可以直接在该文件中运行函数，同时在test文件中被导入的时候不被运行下面的代码
	test(1,2)               #main后tab键补全
```
- all变量：模块文件中有“__all__”变量时，在from xxx import \*时只能导入这个列表中的元素
```python
#model1.py
__all__=["test1"]
def test1:
	balabala
def test2:
	code block
```
#### 包
包就是一个文件夹，该文件夹下有一个“\_\_init\_\_.py”的文件，还有许多模块的文件
一个文件夹，有init.py这个文件就是包
- 自定义包
```python
#创建包
右键根目录，新建软件包
#使用
import 包名.模块名
包名.模块名.目标(函数名)
#使用
from 包名 import 模块名 #不用写包名了
from 包名.模块名 import 函数名 #直接导入具体的功能，不用写模块名和包名

#init.py
__all__=["model1"]
#test.py
from 包名 import *
model1.函数()   #可以用
model2.函数()   #不可用
```
- 安装第三方包
win + r -> cmd 
pip install numpy ,回车，链接外网下载包
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名 ，回车，连国内网下载

# 数据可视化
### 折线图
#### json数据格式
json是一种轻量级的数据交互格式，可以按照json指定的格式去组织封装数据
其本质就是一个带有特定格式的字符串
是在各个编程语言中流通的数据格式，负责不同编程中的数据传递和交互
- python数据和json数据相互转换
```python
import json
#准备符合json格式要求的python数据
data=[{"name":"老王","age":"16"},{"name":"张三","age":"20"}]
#通过json.dumps(data)方法：python->json
data1=json.dumps(data,ensure_ascii=False)
#通过json.loads(data)方法：json->python
s='{"name": "翟秋凯", "age": 18}'
data2=json.loads(s)   #这个s应该是字符串
```
#### pyecharts介绍
pyecharts.org 有中文使用文档
gallery.pyecharts.org 画廊，介绍图表的代码以及简介
首先pip install安装pyecharts模块
- 构建基础的折线图
```python
#导包
from pyecharts.charts import Line
#得到折线图对象
line=Line()
#添加x轴数据
line.add_xaxis(["中国","美国","英国"])
#添加y轴数据
line.add_yaxis("GDP",[30,20,10])
#生成图表
line.render()
#在目录里有lender。html文件，打开后右上角选择浏览器打开，即可查看
```
#### 配置选项->全局配置、系列配置
- 全局配置（在上面的代码的基础上进行配置
```python
#导包  
from pyecharts.charts import Line  
from pyecharts.options import TitleOpts,LegendOpts,ToolboxOpts,VisualMapOpts  
  
#得到折线图对象  
line=Line()  
#添加x轴数据  
line.add_xaxis(["中国","美国","英国"])  
#甜腻骄傲y轴数据  
line.add_yaxis("GDP",[30,20,10])  
#全局配置  
line.set_global_opts(  
    title_opts=TitleOpts(title="GDP展示",pos_left="center",pos_bottom="1%"),  
    legend_opts=LegendOpts(is_show=True),  
    toolbox_opts=ToolboxOpts(is_show=True),  
    visualmap_opts=VisualMapOpts(is_show=True)  
)  
#生成图表  
line.render()
```
#### 数据处理：利用json模块对数据进行处理
ab173.com 数据可视化
```python
import json
#处理数据
f_us=open("D:/美国.txt","r",encoding="UTF-8")
us_data=f_us.read()
#去掉不合理的内容
us_data=us_data.replace("jsonp_1567886539779_69436("," ")
#去掉不合JSON规范的结尾
us_data=us_data[:-2]
#JSON转python字典
us_dict=json.loads(us_data)
#获取trend key
us_trend_data=us_dict['data'][0]['trend']
#获取日期，确定x轴
us_x_data=us_trend_data['updataDate'][:314]
#获取确诊数据，确定y轴
us_y_data=us_trend_data['list'][0]['data'][:314]

#生成图表
```
### 地图
#### 基础地图使用
```python
from pyecharts.charts import Map
from pyecharts.options import VisualMapOpts
#准备地图对象
map=Map()
#准备数据
data=[("北京",99),("上海",199),("湖南",299),("台湾",199),("广州",399),("河北",666)]
#添加数据
map.add("地图",data,"china")

#设置全局选项
map.set_global_opts(  
    visualmap_opts=VisualMapOpts(  
        is_show=True,  
        is_piecewise=True,  
    )  
)
#绘图
map.render()
```
### 动态柱状图
#### 基础柱状图
```python
from pyecharts.charts import Bar  
from pyecharts.options import*  
#构建柱状图对象  
bar=Bar()  
#添加x轴数据  
bar.add_xaxis(["中国","美国","英国"])  
#添加y轴数据  
bar.add_yaxis("GDP",[30,20,10],label_opts=LabelOpts(  
    position="right"  
))  
#反转x轴和y轴  
bar.reversal_axis()  
#绘图  
bar.render("基础柱状图.html") #括号内的内容是给新建的html文件的命名
```

#### 基础时间线柱状图
```python
from pyecharts.charts import Bar,Timeline  
from pyecharts.options import *  
from pyecharts.globals import ThemeType  
bar1=Bar()  
bar1.add_xaxis(["中国","美国","英国"])  
bar1.add_yaxis("GDP",[30,20,10],label_opts=LabelOpts(position="right"))  
bar1.reversal_axis()  
  
bar2=Bar()  
bar2.add_xaxis(["中国","美国","英国"])  
bar2.add_yaxis("GDP",[50,30,20],label_opts=LabelOpts(position="right"))  
bar2.reversal_axis()  
  
#创建时间线对象  
timeline=Timeline({"theme": ThemeType.LIGHT})  
  
timeline.add(bar1,"2021年GDP")  
timeline.add(bar2,"2022年GDP")  
  
timeline.add_schema(  
    play_interval=1000,  
    is_timeline_show=True,  
    is_auto_play=True,  
    is_loop_play=True,  
)  
  
timeline.render("时间线.html")
```


# 类
### 语法
python 是一种面向对象的编程语言
```python
class Student:  
    name=None  
    gender=None  
	def say(self,mesg):
		print(f"大家好，我是{self.name},{mesg}")
stu1=Student()     #和C++不同，创建类对象的语法
stu1.name="翟秋凯"  
stu1.age=31  
print(stu1.gender)
```
- 构造方法：\_\__init\_\_()函数
```python
class Person:
	def __init__(self,name,age):  #传入两个参数，self是一个指向实例本身的引用
		self.name=name
		self.age=age
p1=Person("John",36)
print(p1.name)
print(p2.age)
```
- 字符串方法：\_\_str\_\_
	把类对象转化为字符串
```python
class Student:  
    name=None  
    age=None  
    def __init__(self,age,name):  
        self.name=name  
        self.age=age  
    def __str__(self):  
        return f"类对象的名字{self.name}，年龄：{self.age}"  
stu=Student("翟秋凯",18)  
print(stu)
```
- 大于小于符号比较：\_\_lt\_\_
```python
class Student:  
    name=None  
    age=None  
    def __init__(self,age,name):  
        self.name=name  
        self.age=age  
    def __lt__(self, other):  
        return self.age<other.age  
stu1=Student("翟秋凯",18)  
stu2=Student("xyf",13)  
print(stu1>stu2)
```
- 小于等于、大于等于符号比较：\_\_le\_\_
```python
class Student:  
    name=None  
    age=None  
    def __init__(self,age,name):  
        self.name=name  
        self.age=age  
    def __le__(self, other):  
        return self.age<other.age  
stu1=Student(11,"翟秋凯")  
stu2=Student(11,"xyf")  
print(stu1>=stu2)
```
- \=\=符号比较方法：\_\_eq\_\_
- 删除对象属性
```python
del p1.age
```
- 删除对象
```python
class Person:
	def __init__(self,name,age):
		self.name=name
		self.age=age
p1=Person()
del p1
```
### 封装
>定义私有成员：
>私有成员变量：变量名以\_\_开头
>私有成员方法：方法名以\_\_开头

### 继承
**单继承**
```python
class Person:  
  def __init__(self, fname, lname):  
    self.firstname = fname  
    self.lastname = lname
  def printname(self):  
    print(self.firstname, self.lastname)#创建父类
#创建子类的时候将父类作为参数传入
class Student(Person)
```
**多继承**
```python
class One:  
    name='zqk'  
class Two:  
    age=19  
class Person(One,Two):  
    pass  
  
p1=Person()  
print(p1.name)  
print(p1.age)
```
- 按照继承的顺序，相同名字的变量按照父亲1中的来。
#### 复写父类
对父类成员不满意的时候可以对父类中的成员重新定义，且对父类的成员无影响
当复写类成员后，调用成员会调用复写后的成员，想要使用父类的成员
>调用父类成员
>使用super( ).成员方法()
#### 类型注释
ctrl+p键可以提示你参数
语法——  变量：类型
```python
var_1:int =10

class Student:
	pass
stu:Student=Student()

my_list:list=[1,2,3]  my_list:list[int]=[1,2,3]
my_tuple:tuple[str,int,bool]=('zqk',19,True)
my_dict:dict={"zqk",19}
```
或者在注释中写类型
```python
class Student:
	pass
var_1=random.randit(1,10)  #type:int
var_2=json.loads(data)     #type:dict[str,int]
```
对函数形参和返回值进行，可以对pycharm不知道数据类型的变量进行提示补全操作
```python
def 函数名(形参名:类型名,形参名:类型名)->返回值类型:
	pass
```
Union联合注释
```python
from typing import Union
mt_list:list[Union[str,int]]=[1,2,'zqk','xyf']
```
### 多态
多种状态，即完成某个行为时用不同的对象会得到不同的状态
```python
class Animal:     -------------->  #抽象类
	def speak(self):                  ↑
		pass                       #抽象方法
class Dog(Animal):
	def speak(self):
		print("wolf")
class Cat(Animal):
	def speak(self):
		print("mewo")
```

```python
def make_noise(animal:Animal):
	animal.speak()
dog=Dog()
cat=Cat()
make_noise(cat)
```

# 