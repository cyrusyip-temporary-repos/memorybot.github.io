---
title: "R 学习笔记"
---

# R 学习笔记

## 入门

### 以一个数据分析实例入门

计算年龄与体重之间的相关系数

```R
age<-c(1,3,5,2,11,9,3,9,12,3)
#将年龄数据赋值给变量age，<-是赋值符号
weight<-c(4.4,5.3,7.2,5.2,8.5,7.3,6.0,10.4,10.2,6.1)
#将体重数据赋值给变量weight
cor(age,weight)
#计算age和weight的相关系数
plot(age,weight)
#绘制散点图
```

### 工作空间内容

工作空间（workingspace）是当前R的运行环境，储存着所有用户定义的对象（向量、矩阵、函数、数据框、列表）。

工作目录（working directory）：R用来读取文件和保存结果的默认目录。

```R
getwd()
#查看当前的工作目录
setwd("D:/projects/project1")
#设定当前的工作目录（此路径必须已经存在，如不存在，也不会新建一个路径，设置会失效）
#注意：英文状态下的双引号不要漏掉
```

### R packages 包

包是函数、样例数据、预编译代码以一种定义完善的格式组成的集合。我们经常需要下载安装包来实现新的功能。

```R
install.packages("ggplot2")
#知道包的名字可以使用这个函数直接通过该方式下载安装，ggplot2/tidyr/dplyr/readr/
#注意：只要不卸载R与Rstudio，正常情况下只安装一次后续都一直存在，因此无需重复运行安装代码
library(ggplot2)
#载入使用的包

help(package="ggplot2")
#查看相应包的使用方法
update.packages()
#更新已经安装的包
installed.packages()
#查看已经安装的包
```

### 创建数据集

#### 数据集的概念

数据集通常是由数据构成的一个矩形数组，行表示观测（observation），列表示变量（variable）。

#### 数据类型

R拥有许多用于存储数据的对象类型，包括标量、向量、矩阵、数组、数据框和列表。

```R
#1 向量(vector)是一维数组，用于存储数值型、字符型或逻辑型数据

a <- c(1, 2, 5, 3, 6, -2, 4)
#创建数值型向量
b <- c("one", "two", "three")
#创建字符型向量
c <- c(TRUE, TRUE, TRUE, FALSE, TRUE, FALSE)
#创建逻辑型向量
#注：标量是只含一个元素的向量

#向量元素的访问：
a <- c("k", "j", "h", "a", "c", "m")
a[3]
a[c(1, 3, 5)]
a[2:6]

#2  矩阵（matrix）是一个二维数,每个元素都拥有相同的模式（数值型、字符型或逻辑型）

#myymatrix <- matrix(vector,
#使用的matrix函数,创建一个向量
#nrow=number_of_rows,
#创建的向量的行数
#ncol=number_of_columns,
#创建的向量的列数
#byrow=logical_value,
#true代表按照每行填充；false代表按照列填充
#dimnames = list(char_vector_rownames, char_vector_colnames))
#每一行每一列赋予一个名字

#创建新矩阵：
y <- matrix(1:20, nrow=5, ncol=4)
#创建一个5×4的矩阵
cells <- c(1,26,24,68)
rnames <- c("R1", "R2")
cnames <- c("C1", "C2")
mymatrix1 <- matrix(cells, nrow=2, ncol=2, byrow=TRUE,
                    dimnames=list(rnames, cnames))
#按行填充的2×2矩阵
mymatrix2 <- matrix(cells, nrow=2, ncol=2, byrow=FALSE,
                   dimnames=list(rnames, cnames))
#按列填充的2×2矩阵

#矩阵元素的访问：
x <- matrix(1:10, nrow=2)
# 创建一个2×5的矩阵
x  # 访问整个矩阵
x[2,]  # 访问矩阵第二行
x[,2]  # 访问矩阵第二列
x[1,4]  # 访问矩阵第1行第4列
x[1, c(4,5)]  # 访问矩阵第1行第4、5列

#3  数组（array）与矩阵类似，但是维度可以大于2
# myarray <- array(vector, dimensions, dimnames)
# 向量，维度，维度名称

# 创建新数组
dim1 <- c("A1", "A2")
dim2 <- c("B1", "B2", "B3")
dim3 <- c("C1", "C2", "C3", "C4")
z <- array(1:24, c(2, 3, 4), dimnames=list(dim1, dim2, dim3))

# 数组的访问
z[1,2,3]

#4  数据框（dataframe）与矩阵类似，但是不同的列可以包含不同模式（数值型、字符型等）的数据，是R中最常处理的数据结构。
# mydata <- data.frame(col1, col2, col3,...)

# 创建一个数据框：
patientID <- c(1, 2, 3, 4)
age <- c(25, 34, 28, 52)
diabetes <- c("Type1", "Type2", "Type1", "Type1")
status <- c("Poor", "Improved", "Excellent", "Poor")
patientdata <- data.frame(patientID, age, diabetes, status)

#访问数据框中的元素：
patientdata[1:2]
#访问第一列和第二列的数据
patientdata[c("diabetes", "status")]
patientdata$age

#5  列表（list）是一些对象的有序集合（向量、矩阵、数据框，甚至其他列表），创建一个列表
#mylist <- list(object1, object2, ...)

g <- "My First List"
h <- c(25, 26, 18, 39)
j <- matrix(1:10, nrow=5)
k <- c("one", "two", "three")
mylist <- list(title=g, ages=h, j, k)

#访问列表中的元素
mylist
mylist[[2]]
mylist[["ages"]]
```

#### 数据导入

```R
# 键盘输入

mydata <- data.frame(age=numeric(0),gender=character(0), weight=numeric(0))
# （1）创建一个空数据框（或矩阵）
mydata <- edit(mydata)
# （2）针对这个数据对象调用文本编辑器
# 等价于 fix(mydata)

# 读入带分隔符的文本文件，即csv数据，可以自行检索了解cvs数据详细内容
# 下面提到的两个以外，读入数据文件的函数有很多，可以自行检索其余的函数
# 函数1：使用read.table()从带分隔符的文本文件中导入数据
# 函数用法：mydataframe <- read.table(file, options)
# 读入.csv文件
grades <- read.table("studentgrades.csv", header=TRUE,
                     row.names="StudentID", sep=",")
str(grades)
# 指定每列变量类型
grades <- read.table("studentgrades.csv", header=TRUE,
                     row.names="StudentID", sep=",",
                     colClasses=c("character", "character", "character",
                                  "numeric", "numeric", "numeric"))
str(grades)

# 函数2：read.csv()，自学

# 导入SPSS 数据
install.packages("Hmisc")
library(Hmisc)
mydataframe <- spss.get("mydata.sav", use.value.labels=TRUE)

# 导入SAS 数据
library(Hmisc)
datadir <- "C:/mydata"
sasexe <- "C:/Program Files/SASHome/SASFoundation/9.4/sas.exe"
mydata <- sas.get(libraryName=datadir, member="clients", sasprog=sasexe)

# 导入Stata 数据
library(foreign)
mydataframe <- read.dta("mydata.dta")
```

#### 数据集的标注

```R
# 变量标签
names(patientdata)[2] <- "Age at hospitalization (in years)"
# 给变量patientdata标记为Age at hospitalization (in years)

# 值标签
patientdata$gender <- factor(patientdata$gender,
                             levels = c(1,2),
                             labels = c("male", "female"))
# 给变量patientdata中一些的值做标记标签
```

## R基本数据管理

### 变量处理（创建，重编码，重命名)

```R
# 创建数据集leadership
manager <- c(1,2,3,4,5)
date <- c("10/24/08","10/28/08","10/1/08","10/12/08","5/1/09")
gender <- c("M","F","F","M","F")
age <- c(32,45,25,39,99)
q1 <- c(5,3,3,3,2)
q2 <- c(4,5,5,3,2)
q3 <- c(5,2,5,4,1)
q4 <- c(5,5,5,NA,2)
q5 <- c(5,5,2,NA,1)
leadership <- data.frame(manager,date,gender,age,q1,q2,q3,q4,q5,
                         stringsAsFactors=FALSE)
leadership

## 3-1-1-Creating new variables 创建新变量

#创建新变量q6
leadership$q6 <- c(2,3,5,4,1)
leadership

#创建新变量sum
leadership$sum <- leadership$q1+leadership$q2+leadership$q3+
  leadership$q4+leadership$q5+leadership$q6
leadership

#创建新变量sum
leadership <- transform(leadership,sum = q1+q2+q3+q4+q5+q6)
leadership

## 3-1-2-Recoding variables  重编码变量

#将连续型年龄变量age重编码为类别型变量agecat（Young、 Middle Aged、 Elder）
leadership$agecat[leadership$age > 60] <- "Elder"
leadership$agecat[leadership$age >= 30 &
                    leadership$age <= 60] <- "Middle Aged"
leadership$agecat[leadership$age < 30] <- "Young"
leadership

# 3-1-3-Renaming variables with the plyr package 变量重命名
names(leadership) #获取数据集内的变量名
names(leadership)[2] <- "testDate"
leadership
```

### 数据预处理（缺失值，类型转换，数据排序）

```R
## 3-2-1 缺失值
#检测是否有缺失值
is.na(leadership)

#忽略缺失值的计算分析
x <- c(1, 2, NA, 3) #有缺失值的变量是无法直接计算的
sum(x) #结果为缺失值
sum(x, na.rm=TRUE)#

#na.omit() 删除数据集中有缺失值的观测
leadership
newdata <- na.omit(leadership)
newdata

## 3-2-2转换变量类型
leadership$q1

is.numeric(leadership$q1)

as.character(leadership$q1)

## 3-2-3排序
#按照年龄排序(默认升序)
leadership[order(age),]

leadership[order(-age),] #降序

#按照性别、年龄排序
leadership[order(gender, age),]
```

### 数据集处理（合并，取子集）

```R
## 3-3-1 合并数据集

#原始数据集
manager <- c(1,2,3,4,5)
date <- c("10/24/08","10/28/08","10/1/08","10/12/08","5/1/09")
gender <- c("M","F","F","M","F")
age <- c(32,45,25,39,99)
q1 <- c(5,3,3,3,2)
q2 <- c(4,5,5,3,2)
q3 <- c(5,2,5,4,1)
q4 <- c(5,5,5,NA,2)
q5 <- c(5,5,2,NA,1)
leadership <- data.frame(manager,date,gender,age,q1,q2,q3,q4,q5,
                         stringsAsFactors=FALSE)
#新增数据集1
manager <- c(1,2,3,4,5)
q6 <- c(5,3,3,3,2)
q7 <- c(4,5,5,3,2)
q8 <- c(1,3,4,5,2)
dataframe1 <- data.frame(manager,q6,q7,q8,
                          stringsAsFactors=FALSE)
#横向合并
cbind(leadership,dataframe1) #两个数据集行数相同，顺序相同

merge(leadership,dataframe1, by=c("manager"))

#新增数据集2
manager <- c(6,7,8,9,10)
date <- c("10/12/08","10/21/08","10/11/08","10/17/08","10/1/09")
gender <- c("F","F","M","M","F")
age <- c(32,45,25,39,99)
q1 <- c(1,3,4,3,2)
q2 <- c(4,2,5,3,2)
q3 <- c(3,2,4,4,1)
q4 <- c(5,5,2,4,2)
q5 <- c(3,2,5,2,1)
dataframe2 <- data.frame(manager,gender,date,q1,q2,q3,q4,q5,age,
                          stringsAsFactors=FALSE)

#纵向合并
rbind(leadership,dataframe2)#两个数据框必须拥有相同的变量，顺序不必相同。

#3-3-2 选取子集
#按行取
subset(leadership, age > 35) #选取年龄大于35的数据

subset(leadership, manager != 1) #剔除1号被试

#按列取
subset(leadership, select=q1:q5) #选取特定变量

#综合
newdata <- subset(leadership, gender=="M" & age > 25, select=q1:q5)
```

## R高级数据管理

```R
#-----------------------------------#
# R in Action (2nd ed): Chapter 5   #
# Advanced data management          #
# requires that the reshape2        #
# package has been installed        #
# install.packages("reshape2")      #
#-----------------------------------#
```

### 函数

4.1.1 数值函数

```R
#计算平方根值,log值,取整
a <- 5
sqrt(a)
log(a)
b <- c(1.243, 5.654, 2.99)
round(b)

#计算均值和标准差
x <- c(1, 2, 3, 4, 5, 6, 7, 8)
mean(x)
sd(x)

# 生成服从均匀分布的伪随机数
runif(5)

# 将函数应用于数据对象
c <- matrix(runif(12), nrow=3)
c
log(c)
mean(c)

# 将一个函数应用到矩阵的所有行（列）
#apply(x, MARGIN, FUN, ...)
mydata <- matrix(rnorm(30), nrow=6)
mydata
apply(mydata, 1, mean) #1表示行，2表示列
apply(mydata, 2, mean)

#length 和 nchar
x<-'dddd'
length(x)
nchar(x)

#cat和paste
a<-c(1,2,3,4)
b<-c(4,5,6,7)
c<-c('hi','hello')
paste(a,b,c)
cat(a,b,c)
```

4.1.2 统计函数

{{<figure src="/contents/wiki/20210610r-learning-1.png" caption="Figure 1">}}

4.1.3 概率函数

```R
概率函数的使用方法： [dpqr]distribution_abbreviation() 举例：  runif(5)
d = 密度函数（density）p = 分布函数（distribution function）q = 分位数函数（quantile function）r = 生成随机数（随机偏差）
```

4.1.4 字符处理函数

{{<figure src="/contents/wiki/20210610r-learning-2.png" caption="Figure 2">}}

4.1.5 其他函数

{{<figure src="/contents/wiki/20210610r-learning-3.png" caption="Figure 3">}}

### 解决具体问题

```R
# 解决具体问题
#1.输入数据
options(digits=2)#限定了输出小数点后数字的位数
Student <- c("John Davis", "Angela Williams", "Bullwinkle Moose",
             "David Jones", "Janice Markhammer", "Cheryl Cushing",
             "Reuven Ytzrhak", "Greg Knox", "Joel England",
             "Mary Rayburn")
Math <- c(502, 600, 412, 358, 495, 512, 410, 625, 573, 522)
Science <- c(95, 99, 80, 82, 75, 85, 80, 95, 89, 86)
English <- c(25, 22, 18, 15, 20, 28, 15, 30, 27, 18)

roster <- data.frame(Student, Math, Science, English,
                     stringsAsFactors=FALSE)
roster
#2.标准化的过程，将每个科目的成绩用单位标准差来表示
z <- scale(roster[,2:4])
z
#3.利用mean函数计算每位同学的成绩均值，即综合得分
score <- apply(z, 1, mean)
score
roster <- cbind(roster, score)
roster
#4.quantile函数得到综合得分的百分位数
y <- quantile(score, c(.8,.6,.4,.2))
y
#5.根据百分位成绩，重新编码等级A,B,C,D,F
roster$grade[score >= y[1]] <- "A"
roster$grade[score < y[1] & score >= y[2]] <- "B"
roster$grade[score < y[2] & score >= y[3]] <- "C"
roster$grade[score < y[3] & score >= y[4]] <- "D"
roster$grade[score < y[4]] <- "F"
roster
#6.使用strsplit函数以空格为界把学生姓名拆分为姓氏和名字
name <- strsplit((roster$Student), " ")
name
#7.使用sapply函数提取列表中每个成分的某个元素
Lastname <- sapply(name, "[", 2)
Firstname <- sapply(name, "[", 1)
roster <- cbind(Firstname,Lastname, roster[,-1])
roster
#8.按照姓氏和名字对数据集进行排序
roster <- roster[order(Lastname,Firstname),]
roster
```

### 循环和条件执行

for结构 for循环重复地执行一个语句，直到某个变量的值不再包含在序列seq中为止。语法为：for (var in seq) statement for (i in 1:10) print("HELLO")

2.while 结构 while循环重复地执行一个语句，直到条件不为真为止。语法为：while (cond) statement i<- 10 while(i > 0) {print("HELLO");i<-i-1}

if-else结构 if (cond) statementif (cond) statement1 else statement2 ifelse结构 if else(cond, statement1, statement2)

switch结构switch(expr, ...) ...表示与expr的各种可能输出值绑定的语句

```R
#重复语句
for (i in 1:10) print("HELLO")

i<- 10
while(i > 0) {print("HELLO");i<-i-1}

#条件语句
i<-8
if(i<10) print("i<10")

i<-99
if(i<10) print("i<10") else print("i>10")

ifelse(score > 0.5, print("Passed"), print("Failed"))

i <- "sad"
switch(i,
       happy  = "I am glad you are happy",
       afraid = "There is nothing to fear",
       sad    = "Cheer up",
       angry  = "Calm down now"
)
switch(3, 3+5, 3*5, 3-5, 35)
switch(2*2, mean(1:10), sum(1:10), max(1:10), min(1:10), sqrt(1:10))
```

### 自编函数

```R
# 自编函数
stat = function(x){
  n = length(x)
  m = sum(x)/n
  s = sqrt(sum((x-m)^2/n))
  return(c(m,s))
}

x<-runif(10)
x
stat(x)
stat(1:10)

# 转置
cars <- mtcars[1:5, 1:4]
cars
t(cars)
```

### 数据整合与重塑

{{<figure src="/contents/wiki/20210610r-learning-4.png" caption="Figure 4">}}

```R
# 转置
t(x)

# 整合数据
aggregate(x, by, FUN)

# x是输入的数据对象
# by是要根据哪个变量进行分组
# FUN则是指对每组数据用什么函数进行分析
# 指定函数可以是任何的内建函数也可以是自编函数
# 整合数据
options(digits=3)
attach(mtcars)#绑定数据集，把mtcars的列变量名称加入到变量搜索范围内
aggdata <-aggregate(mtcars, by=list(cyl),
                    FUN=mean, na.rm=TRUE)
#根据气缸数量来整合数据
aggdata

# 加载reshape2 package
library(reshape2)

# 数据输入
mydata <- read.table(header=TRUE, sep=" ", text="
ID Time X1 X2
1 1 5 6
1 2 3 5
2 1 6 1
2 2 2 4
")
mydata
# 融合数据
md <- melt(mydata, id=c("ID", "Time"))
md

# 不执行整合
dcast(md, ID+Time~variable)
dcast(md, ID+variable~Time)
dcast(md, ID~variable+Time)

# 执行整合
acast(md, ID~variable,mean)
dcast(md, Time~variable,mean)
dcast(md, ID~Time,mean)
```

## 验证性因素分析(Confirmatory Factor Analysis, CFA)

验证性因素分析是结构方程模型中的一个环节，用于探讨观察指标与潜在变数之间的关系，以下将详细说明其原理。

### 一、使用情形与说明

结构方程模型(SEM)基本上由两个部分所构成，一是测量模型(measurementmodel)，另一个则是结构模型(structuralmodel)。本次要探讨的观念与实作就是测量模型的部分：也就是观察指标与潜在变数间的关系，一般我们是以验证性因素分析(CFA)来处理这方面的分析。

跟医科学所关注与测量的变数几乎皆为可观察的变数(例如血压或体脂肪)不同，在行为科学，尤其是心理学，政治或社会学等领域，常常会要测量一些比较抽象的概念。举例而言，心理学家可能想测量个体的「自我效能感」(self-efficacy)。但这个构念人人都在谈，却人人没见过，因为其本身较为抽象。这时候，心理学家就想fit了一种方法:藉由测量许多关于自我效能感的行为、认知或态度等相对可明确表征的指标，从中来萃取并架构该抽象构念存在的合理性。这种方法就称为因素分析。

### 二、理论介绍

#### (一)因素分析

因素分析分为两种，一为探索性因素分析(EFA)，一则为验证性因素分析(CFA)。探索性因素分析( EFA)多为发展或编制量表时所用，用来理解那些指标(题目)该被选入或删除，以及一个构念(潜在变数)底下分别具有那些向度(或可称为分量表)等。验证性因素分析(CFA)则多用于一个量表发展完以后，用以检验是否特定的指标(题目)都归到理论预期的各向度底下，主要的目的是理论验证。

举例而言，如果研究者开发了一个量表测量「工作伦理」该潜在变数，而依照EFA的结果，其下又可分为工作态度与工作意义感两个向度，并且分别有X1~X3 ，以及X4~X6这六题分别在该两向度底下。那么我们在进行CFA时，就会依照理论设定模型，然后看整个数据适配的结果如何？简言之，就是看理论与实证数据是否贴近，以为验证。典型的验证性因素分析(在SEM中或称为测量模型)如下例图：

{{<figure src="/contents/wiki/20210610r-learning-5.png" caption="Figure 5">}}

#### (二)信度分析

此外，在古典测量理论中，有所谓信度(reliability)的概念，简单来说，我们利用量表或测验测得的分数可以拆解为两个部分：图中的E1与E2分别代表两个潜在变数(构念)，其下分别被X1-X3，以及X4-X8这些可观察的指标(observedindicator)所测量。而λ则是因素负荷量(factorloading)，绝对值介于0-1之间，表示该指标与特定潜在变数之间的关联强度，其平方则表示「潜在变数能解释该观察指标变异的百分比」。

根据Hair等人(2006)的观点，λ大于等于.71时，就算是一个相当理想的指标，而一个指标(题目)的因素负荷量至少要大于等于.55，才算是可以接受的一个标准，在那数值以下的题目可能就不算很理想，需要予以斟酌。但这些判准并没有这么强硬，端赖于各个科学领域对于测量的品质需求到什么程度。一个量表呈现的公式为：

{{<figure src="/contents/wiki/20210610r-learning-6.png" caption="Figure 6" width="200">}}

公式中下标为X的的变异数为观察分数，而下标为T的部分为真分数，而下标E的部分则为误差分数。由于许多的测量或多或少都有误差，故将真实分数的变异最大化，或将误差分数的变异最小化就是测量的理想目标。这代表着我们真正测量到我们所测量的构念的比例是愈高的，而其他不相干的因素所占的比例是相对愈低的。信度的公式也非常直观，就是1（总变异）减去误差分数的变异部份：

{{<figure src="/contents/wiki/20210610r-learning-7.png" caption="Figure 7" width="100">}}

#### (三)结构方程模型

在结构方程模型(SEM)中，也有学者(Fornell&Larker,1981)提出类似的概念。

组合信度(compositereliability,CR)，计算公式如下：(factorloading的总和)*2/((factorloading的总和)*2+残差变异数之和)

可以上面该公式理解到，组合信度意味着这些观察指标的总变异可以被该潜在变数所以解释的比例究竟有多高。而该两名学者(1981)也提了平均变异萃取量(average variance extracted, AVE)此一量数，公式跟组合信度很类似，但差别在于AVE是将factor loading先各自平方后，再加总起来。一般而言AVE大于.50时，测量模型的表现算相当理想。

## 参考资料

- R语言入门——Rstudio的界面与设置（一）
  
    [R语言入门--Rstudio的界面与设置（一）_从零开始的R世界-Lambda在线](https://vlambda.com/wz_wD0HHQfsPu.html)
    
- R语言入门_ZJU心橙园自制
  
    [R语言入门*ZJU心橙园自制*哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1S7411K7LR/?spm_id_from=333.880.my_history.page.click&vd_source=fc4264415d4564fe87b9d9921989718a)
