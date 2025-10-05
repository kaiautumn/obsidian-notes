## 运行
选择好代码后ctrl+enter运行
按下tab键可以自动补齐
ctrl+清屏
ctrl+↑↓可以看历史代码记录
header=TRUE就是把列名称拿出来作为名称，FALSE就是列名也作为表格中的

## 四区
- 左上：代码区
- 左下：终端
- 右上：Environment环境变量
		History历史代码
- 右下：Files查看文件所在位置
		Plots看绘图
		Packages查看系统已有的软件包
## 函数
**getwd()** 获取默认路径
**setwd(dir="C:/Users/19220/Desktop/R代码")** 更改默认路径
**list.files()** 查看路径下包含的文件
```R
x<-3   #赋值符号
mean(1,2,3,4,5)    #求平均值
runif(geshu,zuixiao,zuida)  #求随机数
round()  #取整

num<-1:100
cut(num,c(seq(0,100,10)))   #将连续变量转换为离散因子，分割为不同区间，每个区间是一个因子


ls()   #看都有什么变量
ls.str()   #看变量的同时也给出数据
rm()   #删除一个或多个对象
rm(list=ls())   #删除所有的对象

save.image()   #定期保存
install.packages("vcd")   #下载vcd包
library()  #查看下载好的包
library(vcd)   #使用包
detach("package:vcd")   #不再使用vcd这个包
```

## 内置数据集
存在datasets包中，收集了美国欧洲的数据

## 数据结构
**相互之间数据元素的集合**
1. 数据类型：数值型、字符串型、逻辑型、日期型、对象……对象是指可以赋值给变量的任何事物，包括常量、数据结构、函数，甚至图形
2. 数据结构：向量、标量；矩阵；数组；列表；数据框；因子；时间序列；
#### 向量：用于存储数值型、字符型或逻辑型数据的一个数组
1. 用函数c创建向量
```R
x<-c(1,2,3,4,5)
y<-c("one","two","three")  #对于字符串变量要加引号
							#逻辑型就是TRUE,False,T,F等
lebgth(x)                   #求向量的长度	
```
2. 一些快捷方式创建向量
```R
x<-c(1:5)

seq(from=1,to=100,by=2)#从1到100，步长为2
rep(2,5)                      #重复函数，重复5次2
rep(x,3)                  #123451234512345
rep(x,each=5)             #1111122222333334444455555
```
向量中的数据必须是同一类型

3. 向量索引
```R
x<-c(1,100)
x[1]   #向量索引从1开始，用中括号
x[-19] #输出除了第19个元素外的其他所有元素
x[c(1,2,3,56)] #访问第1、2、3、56个元素
#使用逻辑值访问
y<-c(1:10)
y[c(T,T,F,F,T,F,F,T,T,F)]#只访问逻辑值为真的元素
y[c(T,F)] #相当于TFTFTFTFTF
#直接法
y[y>5] #访问y中大于5的数字
```
   当向量中的数据是字符串时
```R
x=c("one","two","three")
"one" %in% x

#给向量添加名称
names(x)<-c()  #在x中每个元素前加一个名字，可以通过名字进行访问此数
```

```R
#添加向量
x<-c(1:100)
x[101]<-101
x[c(102,103,104)]<-c(102,103,104)
#插入元素
append(x,5.5,5)   #表示在5后加一个5.5
#删除
rm(x)  #删除整个向量
```
4. 向量的运算
```R
x<-c(1:5)
y<-seq(1,100,length.out=10)
x+1  #每个元素都加1，相当于x<-x+1
x+y,x*y  #对应的元素相加相乘
**  #幂乘
%%  #求余
%/% #整除

x>5 / x>y #直接返回逻辑型判断
%in%  #判断是否存在，不必使用循环。判断是以标量形式比较的

x==y #x与y是否有一样的数

# 运算函数
abs(x) #返回绝对值
sqrt()  #返回平方根
log( 指数,底数 )  log(e)=1  log10(100)=2
exp(x)   #x的自然指数
ceiling()  #返回大于数的最小数
floor()    #返回小于数的最大数
trunc()    #返回整数部分
round(,digits=)    #四舍五入,后面输保留小数点位数
sinif()

#统计函数
vec=c(1:100)
sum(vec)=100
max(vec)   #返回100 
min(vec)   #返回1
range(vec) #同时返回最小最大值
mean(vec)  #返回平均值
var(vec)   #方差
sd(vec)    #标准差
prod(vec)  #连续积
median()   #中位数
quantile(vec,c(0.4,0.5,0.7)) #p分位数，c()中为第几几分位数
which.max(vec) #返回最大值的索引值
which.min(vec)
which(x==100)  #返回100的索引

```
#### 矩阵
所有元素的数据类型都应该相同
```R
m<-matrix(x,hangshu,lieshu)  #x为一个向量，有20个元素。
m<-matrix(x,hangshu,lieshu,byrow=T)  #按行分
m<-matrix(x,hangshu,lieshu,byrow=F)  #按列分

rnames<-c("R1","R2","R3","R4")
cnames<-c("C1","C2","C3","C4","C5")
dimnames(m)<- list(rnames,cnames)    #给m矩阵每一行每一列都起名字

dim(m) #显示 维数，即4行5列
dim(x) #显示NULL
dim(x)<-c(4,5)  #可以将x变成矩阵
```
- 矩阵索引
```R
m<-matrix(1:20,4,5,byrow=T)
m[1,2] 
m[c(1,2,3),c(4,5)]
m[2,]     #第2行
m[-1,2]   #出去第一行后的第二列
m["R1","C2"]
```
- 矩阵运算
```R
m+1   m*2   m+m
colSums(m)  #计算每一行的和
rowSums(m)  #计算每一列的和
colMeans(m)   rowMeans(m)

m*n  #对应位置元素相乘，即内积
m%*%n #矩阵相乘，即外积

diag(m)  #返回对角线位置的值
```
#### 列表
列表可以存储不同类型的数据，甚至可以存列表本身
```R
a<-1:20
b<-matrix(1:20,4)
c<-mtcars
d<-"This is a list."

mlist<-list(a,b,c,d)

#访问
mlist[1]       #输出结果还是列表形式
mlist[[1]]     #输出结果时数据本身的类型
#按照第一种，返回结果是列表，不能直接赋值，所以赋值要两个中括号
mlist[c(1,4)]  #一次访问多个列表元素时要将其变成向量形式

x<-list(name="zqk",age=18,matrix=mylist)
x$name         #用$可以通过访问名称的方式来进行访问元素

#修改列表
#赋值: milst[[2]]=list1
#删除: mlist
```
#### 数据框
表格式的数据结构，形状上像矩阵，实际是一个列表，列表的元素是向量，构成列，每一列的长度必须相同。
每个列元素的所有数据类型必须相同，行可以不同
Excel类似于一个数据框
```R
#创建：data.frame
state<-data.frame(, , ,)
#访问
state[1]#输出数据框的第一列
state[-1]#输出除了第一列的数据
state[,"Murder"]#输出Murder这一列
state["Alaabama",]#输出这一行

state$Murder #直接输出这一列

attach(state)
Murder       #直接访问列
detach(state)#取消访问

with(state,{Income})#直接访问
```
#### 因子
- 变量分类
	名义型：北京、上海、西安……
	有序型：good, better, best……
	连续型：身高
- 名义型变量和有序型变量称为因子factor，这些分类变量的可能值称为水平level。这些由水平值构成的向量就称为因子。
- 因子本身就是向量
```R
f<-factor(c("red","blue","green","black"))
week<-factor(c("Mon","Fri","Thu:","Sun"),ordered=T,levels=c("Mon","Tue","Wed","Thu","Fri","Sat","Sun"))

#将向量变为因子
first<-c(1,2,4,5,2,1,6,4)
first_factor<-factor(first)
```
#### 缺失数据
NA表示缺失值，用来存储缺失信息
```R
a<-c(NA,1:49)
sum(a)  #直接写是NA
is.na(a) #判断a中是否有NA，有的话在对应位置返回TRUE，or返回FALSE
sum(a,na.rm=TRUE)  #忽略NA值

ilbrary(VIM)   #处理缺失值

NAN #不可能的值，如1/0
is.nan()  #判断是否是不存在的值，返回逻辑值

Inf #无穷
is.infinite() #判断是否是无穷的数，返回逻辑值
```
#### 字符串
字符串一定加引号
```R
nach("Hello World") #统计字符串的长度，空格也算一个字符，即返回11
	#如果插入的是数字的话，会将数字按照字符串处理
length()            #统计向量或列表中元素的个数
paste("Everybody","loves","me")  #合并字符串为一个字符串，默认用空格分隔
paste("Everybody","loves","me",sep="-") #自定义分隔符

name<-c("zqk","xyf")
paste(names,"loves","you")     #将向量中的每个元素分别与paste中的字符串相连，返回值是一个向量
paste(name,name)               #向量中的每个元素与相应位置的元素相连

substr(x,start,stop)           #提取x中从start开始到stop结束的字符

toupper(x)                     #将字符串大写
tolower(x)                     #将字符串小写
gsub("^(\\w","\\U\\1",tolower(temp),perl=T) #首字母大写 
gsub("^(\\w","\\L\\1",toupper(temp),perl=T) #首字母小写

x<-c("b","A+","AC")
grep("A+",x,fixed=T)           #字符中查找内容，严格与“A+”匹配
grep("A+",x,fixed=F)           #不是很严格地查找，只要有“A+”就行

strsplit(str,fengefu)          #在字符串中依据分隔符分割，返回一个列表

face<-1:13
suit<-c("spades","clubs","hearts","diamonds")
outer(suit,face,FUN=paste)     #将两个向量所有的组合排列出来
outer(suit,face,FUN-paste,sep="-")  #设置连接符号
```
#### 日期和时间
```R
Sys.Date()  #返回当下的时间

a<-"2025-07-04"
a<-as.Date(a,format="%Y-%m-%d")  #将a的字符串变为日期型变量

seq(asa.Date("2025-07-04"),as.Date("2025-09-17"),by=5) #每隔5天输出一个日期，从7-5到9-17

ts(data,start,end,frequency) #生成时间序列，data为向量或者矩阵，start是起始时间，为一两个数字组成的向量，frequency是频率，1为年，4为季度，12为月
```

## 常见错误
- 定义向量用c
- 路径，应为/，或者\\\。一个\是转义字符的意思
## 获取数据与文件读取
1. 键盘输入
edit()函数能编辑一个对象，比如数据框、函数等等
```R
d <- c(1,2,3,4)
e <- c("red","blue","purple","black")
f<-c(T,T,T,F)
mydata<-data.frame(d,e,f)
mydata<-edit(mydata)    #一定要有mydata<-
```
fix()函数也可以
```R
mydata<-data.frame(d,e,f)
fix(mydata)
```
2. 通过哦访问数据库来获取数据
ODBC是开放数据库连接的简称
```R
install.packages("RODBC")
```
3. 通过读取存储在外部文件上的数据
```R
#读取纯文本文件
x<-read.table("yaodudewenjain.txt",header=FALSE,sep="",quote="",nrows,skip)
#file为文件路径，header为是否将第一行作为列名，sep为字段分隔符，默认是空格，quote是用于分割包含特殊字符的字符串的字符，nrows为要读取的行数，skip开始读取的时候跳过的行数
x<-read.table("C:/Users/19220/Desktop")
x    #显示内容
head(x)
tail(x，n=10)#显示文件中头或尾,默认6行，可以更改行数
```

```R
#读取网络文件
install.packages(XML)
library(XML)
readHTMLTable
```
#### 写入文件
```R
x
write.table(x,file="C:/Users/19220/Desktop/newfile.txt")
```
#### 读写Excel文件
```R
#将表格改为csv格式后
x<-read.csv("duqu.csv",header=TRUE)
#将表格内容复制后
x<-read.table("clipboard",sep="\t",header=T)
```
用包
```R
install.packages("readxl")
library("readxl")
data<-read_excel(file.choose())#交互式选择文件
data<-read_excel("name",sheet="sheetname")
```
#### 读写R格式文件
```R
saveRDS(x,file="newfile.RDS")  #存储为RDS文件,RDS是二进制文件格式，用于保存单个R对象，灵活，高效
y<-readRDS("newfile.RDS")
=
load(".RData")

save()  #函数
```

## 数据转换
```R
#矩阵转换为数据框
state.x77 #是一个矩阵
dstate.x77<-as.data.frame(state.x77) #dstate.x77就是数据框了
```

## R语音的函数（精髓）
### 选项参数
输入控制部分
输出控制部分
调节部分
### 数学统计函数
##### 概率论
d 概率密度函数
p 分布函数
q 分布函数的反函数
r 产生相同分布的随机数

| β分布  | 二项分布  | 柯西分布   | 卡方分布  | 指数分布 | F分布 | 几何分布 | 超几何分布 | Logistic分布 | 泊松分布 |
| ---- | ----- | ------ | ----- | ---- | --- | ---- | ----- | ---------- | ---- |
| beta | binom | cauchy | chisp | exp  | f   | gemo | hyper | logis      | pois |
在每个分布前加d p q r就是对应的函数
##### 随机数
runif(n,min=min,max=max)  生成( min , max )间n个随机数
set.seed( seed )  会设置一个种子，根据种子来生成随机数

### 描述性统计函数
summary( ) 给出最小值、最大值、四分位数、数值型变量的均值，以及因子向量和逻辑向量的频数统计
fivenum( ) 返回 最小值，3个四分位数，最大值

### 频数统计函数
split( x , factor )  按照因子把x中的数据分组
### 独立性检验函数
卡方检验 
Fisher检验
Cochran-Mantel-Haenszel检验
 
原假设：没有发生，什么都没变
备择假设：发生了

p值：p<0.05 拒绝原假设；p>0.05 不拒绝原假设（α可以变，要求非常严格时α要小）
```R
library(vcd)
mytable<-tabe(Arthritis$Treatment,Arthritis$mproved)
chisp.test(mytable)
```
### 相关性分析函数
衡量指标：Pearson相关系数、Spearman相关系数、Kendall相关系数
```R
cor  #三种相关性都用一个函数，只是method参数不同
cor(state.x77)
cov(state.x77)
```
### 相关性检验函数
```R

```

### 绘图函数
数据可视化
1. 基础绘图系统：
	1. 高级绘图：直接出图
	2. 低级绘图：在高级绘图的基础上对图形进行进一步的调整，比如加一条线、加上标题文字等
```R
plot()函数
```
2. lattice包
3. ggplot2包
4. grid包
### 自定义函数->减少重复代码的书写
函数名称、声明、参数、函数体
```R
myfun<-function( 选项参数 ){
	函数体
}
```
函数内部的向量化操作
if、for、while、switch
### 线性回归
```R
lm()   #
```
### 多元线性回归
### 方差分析
### 广义线性模型
### Logistic回归
### 主成分分析
### 因子分析