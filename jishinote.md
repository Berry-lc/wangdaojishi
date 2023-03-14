# 王道机试笔记

## Chapter1枚举和模拟

### 枚举

#### 1.1

![image-20230224005300363](https://s2.loli.net/2023/02/24/aMhOkyjt497G1Uq.png)

```c
#include <stdio.h>

int main(void) {
    int i,j,k;
    for(i=0;i<=9;i++)
    {
        for(j=0;j<=9;j++)
        {
            for(k=0;k<=9;k++)
            {
                if(i*100+j*10+k+j*100+11*k==532)
                    printf("%d %d %d\n",i,j,k);
            }
        }
    }
    printf("Hello World\n");
    return 0;
}
```

#### 1.2

![image-20230223235640807](https://cdn.jsdelivr.net/gh/Berry-lc/wangdaojishi@pic/uPic/epnys8.png)

我的算法

```c
#include<stdio.h>
int main()
{
    int i=1000,j,a,b,c,d;
    while(i<=9999)
    {
        j=1;
        while(j!=0)
        {
            d=i%10;
            j=i/10;
            c=j%10;
            j=j/10;
            b=j%10;
            j=j/10;
            a=j%10;
            j=j-a;
            if(i*9==d*1000+c*100+b*10+a)
                printf("%d%d%d%d\n result",a,b,c,d);
        }
        i++;
    }
    return 0;
}
```

参考算法

```c
#include<stdio.h>
#include <stdbool.h>

int Reverse(int n)
{
    int reverse=0;
    int remain;//每次的余数
    while(true)
    {
        remain=n%10;
        reverse=remain+reverse*10;
        n=n/10;
        if(n==0)
        {
            break;
        }
    }
    return reverse;
}
int main()
{
    int n,j;
    for(n=1001;n<=9999;n++)
    {
        j= Reverse(n);
        if(n*9==j)
            printf("%d\n",n);
    }
    return 0;
}
```

#### 1.3(求逆序数,同1.2)

![image-20230224023620517](https://s2.loli.net/2023/02/24/oNMbIHAvDQGaYXz.png)

我的代码

```c
#include<stdio.h>
int Reverse(int n)
{
    int reverse=0;
    int remain;
    while(n!=0)
    {
        remain=n%10;
        n=n/10;
        reverse=reverse*10+remain;
    }
    return reverse;
}
int main()
{
    int i;
    for(i=0;i<=256;i++)
    {
        if(i*i==Reverse(i*i))
        {
            printf("%d\n",i);
        }
    }
    return 0;
}
```

### 避免出错的规范

1.判断语句的书写

![image-20230224115012441](https://s2.loli.net/2023/02/24/OLrB5kEUiGz3sCQ.png)

2.永远不省略花括号

### 模拟

场景——〉代码

东西——〉数据结构(数组、二维数组)——〉交互

题型:图形打印,日期问题、其他模拟

#### 1.4 输出梯形

![image-20230224180902693](https://s2.loli.net/2023/02/24/n7SrBvtzaHcfGMT.png)

我的代码

```c
#include<stdio.h>

int main()
{
    int h,i,j;
    scanf("%d",&h);
    for(i=1;i<=h;i++)
    {
        j=1;
        while(j<=3*h-2)
        {
            if(j<=2*h-2-2*(i-1))
            {
                printf(" ");
                j++;
            }
            else
            {
                printf("*");
                j++;
            }
        }
        printf("\n");
    }
    return 0;
}
```

参考代码

```c
#include "stdio.h"
int main()
{
    int h;
    scanf("%d",&h);
    for(int i=0;i<h;i++)
    {
        for(int j=0;j<2*h-2-2*i;j++) {
            printf(" ");
        }
        for(int j=0;j<h+2*i;j++)
        {
                printf("*");
        }
        printf("\n");
    }
    return 0;
}
```

#####  实现不确定数量的输入(使用while循环scanf)

```c
while(scanf("%d",&h)!=EOF){}
```

![image-20230224183633915](https://s2.loli.net/2023/02/24/a3T7Bs2PqjuERUZ.png)

##### scanf

1.scanf的返回值是一个int,返回读取内容的个数

2.ctrl+D 文件终止符(ctrl+Z)

##### 通用方法——使用二维数组解决打印图案的问题

<img src="https://s2.loli.net/2023/02/24/cXxlnLw7vKEaOY4.png" alt="image-20230224193542351" style="zoom:150%;" />

1.定二维数组的范围

下底边长——3h-2

高——h

上底边长——h

数组范围arr\[0][0]——arr\[h-1][3h-3]

2.先全部填上空格,再从下往上填*

代码:

```c
#include<stdio.h>
char arr[1000][3000];//定义一个全局的数组
int main()
{
    int h;
    while(scanf("%d",&h)!=EOF)
    {
        for(int i=0;i<h;i++) {//区域全部填上空格
            for (int j = 0; j < 3 * h - 2; j++) {
                arr[i][j] = ' ';//一个字符要用单引号！！！
            }
        }
        for(int i=h-1;i>=0;i--){
            for(int j=2*((h-1)-i);j<3*h-2;j++){
                arr[i][j]='*';//一个字符要用单引号！！！
            }
        }
        for(int i=0;i<h;i++){//输出数组
            for(int j=0;j<3*h-2;j++){
                printf("%c",arr[i][j]);
            }
            printf("\n");
        }
    }
    return 0;
}
```

##### 函数的作用域

```c
int i;//作用于全部
```

```c
for(int i=;;){}//只作用于循环内
```

##### C风格的字符串设计

c语言中,用字符数组来处理字符串

![image-20230225153333156](https://s2.loli.net/2023/02/25/eic5wYlLhCnxQp1.png)

char二维数组——〉数组的数组

```c
//读取一个字符串
char str[];
scanf("%s",str)
//输出一个字符串
printf("%s",str)
```

代码的改进

```c
arr[i][3*h-2]="\0";//用来指示每一行字符串的结束
//打印代码
for(int i=0;i<3*h-2;i++){
printf("%s",arr[i])
}
```

图案打印问题的一般思路

1.申请二维数组(固定大小,可以放在全局变量上)

2.根据条件,从任意方向开始,设置二维数组

3.把二维数组每一行的边界最后一个位置,使用"\0"赋值(可以在第一步将所有位置设为"\0")

4.使用printf(%s),配合循环,打印每一行 

#### 1.5叠筐

![image-20230225161013428](https://s2.loli.net/2023/02/25/maXTGdPfHtozsDv.png)

<img src="https://s2.loli.net/2023/02/25/H6b9qCwL4JgEviy.png" alt="image-20230225161035856" style="zoom: 67%;" />





## Charpter2排序和查找

### 排序

使用库函数  sort   c++引入

```c++
#include<algorithm>
using namespace std;
```

#### 2.1

![image-20230225170333518](https://s2.loli.net/2023/02/25/7H8ZL2I5wQqXnSO.png)

代码:

```c++
#include<cstdio>
#include<algorithm>
using namespace std;
int main(){
    int n;
    int arr[101];
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    sort(arr,arr+n);//排序
    for(int i=0;i<n;i++){
        printf("%d ",arr[i]);
    }
}
```

##### 库函数sort

```c++
sort(begin,end)\\起点和终点
```

![image-20230225170933551](https://s2.loli.net/2023/02/25/youVFJMgXzR196W.png)

```c++
int arr[]//定义
arr[0] arr[1]//元素
arr   //0号元素的地址
arr+i  //i号元素的地址
```

默认结果:升序排序





改变排序的结果——〉设计排序的规则——〉设计比较和交换的条件

```c++
sort(left,right,comp) //函数重载:不同参数的函数,可以有相同的名字
//left——第一个元素 right——尾后   comp——比较和交换的条件
```

目标:降序排序——〉设计交换条件:lhs〉rhs 不交换

代码:

```c++
bool comp(int lhs,int rhs){//但返回值为true时,则不进行交换,当为false时,交换
	if(lhs>rhs){
		return true;
	}
	else{
		return false;
	}
}
sort(arr,arr+n,comp)
```

#### 2.2整数奇偶排序

![image-20230225175853354](https://s2.loli.net/2023/02/25/4F8cwPC3GgY6HE1.png)

#####  我的代码:

```c++
#include "cstdio"
#include"algorithm"
using namespace std;
int comp(int l,int r){
    if(l>r){
        return true;
    }
    else{
        return false;
    }
}

int main(){
    int arr[10];
    int arrji[10];
    int arrou[10];
    for(int i=0;i<10;i++){
        scanf("%d",&arr[i]);
    }
    int numji=0,numou=0;
    for(int i=0;i<10;i++) {
        if (arr[i] % 2 == 0) {
            arrou[numou] = arr[i];
            numou++;
        } else {
            arrji[numji] = arr[i];
            numji++;
        }
    }
    sort(arrji,arrji+numji,comp);
    sort(arrou,arrou+numou);
    for(int i=0;i<numji;i++){
        printf("%d ",arrji[i]);
    }
    for(int i=0;i<numou;i++){
        printf("%d ",arrou[i]);
    }
}
```

什么情况下不发生交换?

1左边奇数右边是偶数

2左边奇数大右边奇数小

3左边偶数小右边偶数大

##### 运用comp函数的代码

```c++
#include "cstdio"
#include"algorithm"
using namespace std;
bool comp(int l,int r){
    if(l%2!=0&&r%2==0 ||
    l%2!=0&&r%2!=0&&l>r ||
    l%2==0&&r%2==0&&l<r){
        return true;
    }
    else{
        return false;
    }
}

int main(){
    int arr[10];
    for(int i=0;i<10;i++){
        scanf("%d",&arr[i]);
    }
    sort(arr,arr+10,comp);
    for(int i=0;i<10;i++){
        printf("%d ",arr[i]);
    }
}
```

#### 2.3成绩排序(使用结构体)

![image-20230226131320481](https://s2.loli.net/2023/02/26/gxP4ibaw15G2MKR.png)

##### 自定义类型

```c++
struct Student{
	\\成员

};
```

我的代码:

```c++
#include<cstdio>
#include<algorithm>
using namespace std;
struct Student{
    int num;
    int point;
};
bool comp(Student lhs,Student rhs){
    if(lhs.point>rhs.point ||
    lhs.point==rhs.point &&lhs.num>rhs.num ){
        return false;
    }
    else
        return true;
}
int main(){
    int n;
    scanf("%d",&n);
    Student arr[n];
    for(int i=0;i<n;i++){
        scanf("%d %d",&arr[i].num,&arr[i].point);
    }
    sort(arr,arr+n,comp);
    for (int i=0;i<n;i++) {
        printf("%d %d\n", arr[i].num, arr[i].point);
    }
    return 0;
}
```

#### 2.4成绩排序(printf的格式控制)

![image-20230226132007916](https://s2.loli.net/2023/02/26/GX7PMtldNKFewvr.png)



### 查找

#### 2.5 顺序查找

![image-20230301171420513](https://s2.loli.net/2023/03/01/pa78bRdAJuV5vwl.png)

##### 代码：

```c
#include<cstdio>
int main(){
    int n;
    scanf("%d",&n);
    int arr[200];
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    int x;
    scanf("%d",&x);
  	int i;
    for(i=0;i<n;i++){ //查找
        if(arr[i]==x){
            printf("%d\n",i);
          	break;
        }
    }
  	if(i==n){
      printf("-1\n"); 
    }
    return 0;
}
```

##### 顺序查找问题

有多个x需要查找时——效率不高

二分查找

注意：1.有序数组 2.迭代和边界情况



## Charpter3字符串的基本使用

### c风格的字符串进行输入和输出：

字符数组 以“\0”作为正文结束的标志（要占空间）

使用```printf```和```scanf```

### c风格转化为c++风格

```c++
#include<string>
using namespace std;
string var=str;
```

### 将c++风格转化为c方便输入输出

```c++
printf("%s",var,var.c_str());
```

### 字符串的相关操作：

```c++
scanf("%s",buf); //只能读取一个单词
fget(buf,100,stdin);//读取一整行，包括末尾的换行符
```

### c++风格的字符串

#### 求字符串长度

```c++
printf("lenth of str =%u\n",str.size());//也可以用lenth()
```

#### 访问字符串中每一个字符

##### 循环

```c++
for(unsigned int i=0;i<str.size();i++){
printf("%c\n",str[i]);
}
```

##### 迭代器

```c++
for(string::iterator it=str.begin();it!=str.end();it++){
printf("%c\n",*it);//*it 通过地址访问元素
}
```

#### 操作字符串的内容

##### 连接：+（只针对c++风格的字符串）

```c++
str=str+"world";//+在c++风格的字符串中表示连接操作
```

##### 删除：erase

```c++
str.erase();//括号里面写删除元素的下表
str.erase(str.size()-1);//删除最后一个元素
```

##### 清空：clear

```c++
str.clear();
```

##### 查找：string的find方法

find的返回值：找到了——〉匹配内容的起点的下标

​                          没有找到——〉返回strin::npos

```c++
#include<cstdio>
#include<string>
using namespace std;
int main(){
string str ="howareyou";
int pos =str.find("are");//
if(pos!=string::npos){
	printf("FIND,pos=%d\n",pos);
}
else{
	printf("NOT FIND\n");
}
}
```

## Charpter4线性数据结构

### 数组

#### 限制：

1. 数组定义时，就要指定大小（一般为常量，机试就只用常量大小）
2. 函数内部定义的数组，不能太长！过长的数组定义在函数外面，作为全局变量

### 向量Vector

动态数组——〉在内存中顺序存储，线性表

c++风格的容器

```c++
#include<vector>
using namespace std;
vector<int> vec1；//<>中写元素类型  默认长度是零 
vec1.push_back(1);//尾部扩容
vector<int> vec2 {1,2,3};//vector的初始化
vector<int> vec3 (10000);//初始化一个指定大小的向量,[0]-[9999]都是0
```

#### 访问、修改、调整vector

```c++
.push_back //扩容，效率最高
.pop_back() //弹出最后一个元素
vec[i] //i从0开始 i>=n会越界
//迭代器
```

#### 随机位置的插入和删除

![image-20230314174137029](https://s2.loli.net/2023/03/14/OZDoRKjlrLM5h4N.png)

insert     在指定位置的前面插入   

#### 4.1完数和盈数

![image-20230314174531390](https://s2.loli.net/2023/03/14/Q21LqSzPBTRuy7s.png)

##### 代码

```c++
#include <iostream>
#include<cstdio>
#include<vector>
using namespace std;
int shifouyingshuhuowanshu(int n){
    vector<int> yinzi;
    for(int i=1;i<n;i++){     //除法要从1开始，否则会出现浮点错误
        if(n%i==0){
            yinzi.push_back(i);//可以不用建立因子的数组，直接加在sum中
        }
    }
    int sum=0;
    for(int i=0;i<yinzi.size();i++){
        sum=sum+yinzi[i];
    }
    if(sum==n)
        return 0;
    else if(sum>n)
        return 1;
    else
        return 2;
}
int main() {
    vector<int> wanshu,yingshu;
    for(int i=2;i<=60;i++){
        int j;
        j=shifouyingshuhuowanshu(i);
        if(j==0)
            wanshu.push_back(i);
        else if(j==1)
            yingshu.push_back(i);
    }
    printf("E:");
    for(int i=0;i<wanshu.size();i++){
        printf(" %d",wanshu[i]);
    }
    printf("\nG:");
    for(int i=0;i<yingshu.size();i++){
        printf(" %d",yingshu[i]);
    }
    return 0;
}
```

#### Vector的原理

#### Vector的扩容机制

size逐渐增大到capacity——〉申请内存2*capacity——〉拷贝——〉释放内存

push_back n个元素，时间复杂度：O(N)

### 队列

场景：“公平的等待”——〉广度优先遍历

#### 队列的实现

```c++
#include<queue>
using namespace std;
queu e<int> q;
q.push(i) //入队，从队尾
q.pop()  //出队
q.empty()  //判断队列是否为空
q.front()  //队头
```

#### 4.2约瑟夫问题

![image-20230315014312564](https://s2.loli.net/2023/03/15/LbCKtkNdwW742Ei.png)



