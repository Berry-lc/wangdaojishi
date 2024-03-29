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

scanf %d %f %o   忽略空白字符

scanf %c  可以读取空白空格，若前面有空格，则忽略空白字符



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

### 队列——“公平的等待”——〉广度优先遍历

场景：“

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

##### 我的代码

```c++
#include<cstdio>
#include<queue>
using namespace std;
int main(){
    int n,p,m;
    scanf("%d %d %d",&n,&p,&m);
        queue<int> qu1;
        for(int i=1;i<=n;i++){
            qu1.push(i);
        }
        for(int i=1;i<p;i++){//让p号在最前面
            int tmp;
            tmp=qu1.front();
            qu1.pop();
            qu1.push(tmp);
        }
        while(true) {
            for (int i = 1; i < m; i++) {
                int tmp;
                tmp = qu1.front();
                qu1.pop();
                qu1.push(tmp);
            }
            printf("%d,", qu1.front());
            qu1.pop();
            if (qu1.empty())
                break;
        }
        return 0;
    }
```

![image-20230315162706075](https://s2.loli.net/2023/03/15/LSkrlaegsHN4u3f.png)

##### 参考代码

```c++
#include<cstdio>
#include<queue>
using namespace std;
int main() {
    int n, p, m;
    while (true) {//实现当输入三个0时，开始程序
        scanf("%d %d %d", &n, &p, &m);
        if (n == 0 && p == 0 && m == 0) {
            break;
        }
        queue<int> children;
        for (int i = p, j = 0; j < n; ++j) {//把队列排好队
            children.push(i);
            i++;//p->p+1->....n->1->p-1
            if (i ==n+1){
                i = 1;
            }
        }
        int num = 1;//开始喊号
        while (true) {
            int cur = children.front();
            children.pop();
            if (num == m) {
                num = 1;
                if (children.empty()) {
                    printf("%d\n", cur);
                    break;
                } else
                    printf("%d,", cur);
            } else {
                num = num + 1;
                children.push(cur);
            }
        }
    }
}
```

#### 4.3猫狗收容所

![image-20230315180636149](https://s2.loli.net/2023/03/15/zn8sxdMXbvUj72V.png)

##### 我的代码（用三个队列）

```c++
#include<cstdio>
#include<queue>
using namespace std;
struct operate{
    int op1;
    int op2;
};
int main(){
    int n,op1,op2;
    queue<operate> operates;
    queue<int> dogs,cats,all,shouyang;
    scanf("%d",&n);
    for(int i=0;i<n;i++){//输入操作序列
        scanf("%d%d",&op1,&op2);
        struct operate op;
        op.op1=op1;
        op.op2=op2;
        operates.push(op);
    }
    for(int i=0;i<n;i++) {
        struct operate op;
        op = operates.front();
        operates.pop();
        if (op.op1 == 1) {//若第一个数为1，则有动物进入
            if (op.op2 > 0) {
                dogs.push(op.op2);
                all.push(op.op2);
            }
            else if (op.op2 < 0) {
                cats.push(op.op2);
                all.push(op.op2);
            }
            else
                continue;
        }
        else if (op.op1 == 2) {//第一个数为2，有收养
            if (op.op2 == 0) {
                int tmp;
                while (true) {
                    tmp = all.front();
                    if (tmp != dogs.front()&&tmp != cats.front()) {
                        all.pop();
                    } else
                        break;
                }
                shouyang.push(tmp);
                if (tmp > 0)
                    dogs.pop();
                else
                    cats.pop();
            }
            else if (op.op2 == 1) {
                int tmp;
                tmp = dogs.front();
                dogs.pop();
                shouyang.push(tmp);
            }
            else if (op.op2 == -1) {
                int tmp;
                tmp = cats.front();
                cats.pop();
                shouyang.push(tmp);
            }
            else
                continue;
        }
        else
            continue;
    }
    for(int i=0,j=shouyang.size();i<j;i++){//在输出队列时，要先定义一个队列的大小，再执行for
        printf("%d ",shouyang.front());
        shouyang.pop();
    }
    return 0;
}
```

##### 参考代码（两个队列）

![image-20230318170503340](https://s2.loli.net/2023/03/18/lAbBsq6pvcLSotw.png)

### 栈——有优先级差别的等待

```c++
stack<typename> myStack//初始化
.size()//大小
.push()//压栈
.top()//栈顶元素
.pop()//弹出栈顶元素
.empty()
```

### 整数的数据类型

```c++
int //4B——32bit      -2^31~2^31-1
unsigned int//			0~2^32-1
long long//8B——64bit		
unsigned long long//
```



#### 4.4反转序列

![image-20230321163749608](https://s2.loli.net/2023/03/21/y1r7RdTjKwhHbiL.png)

##### 代码

```c++
#include<cstdio>
#include<stack>
using namespace std;
int main() {
    int n;
    stack<long long> stack1;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        long long j;
        scanf("%lld",&j);//读取longlong类型的十进制数
        stack1.push(j);
    }
    while(!stack1.empty()){
        printf("%lld ",stack1.top());
        stack1.pop();
    }
    printf("\n");
    return 0;
}
```

### 读取字符串的操作

```c++
//读取单词
char buf[1000];
scanf("%s",buf);//当ctrl+d时，返回EOF
//读取一行
cahr buf[1000];//当ctrl+d时，返回NULL
fgets(buf,1000,stdin);//会额外读入换行符
//string str=buf;  str.pop_back(); 
```

#### 4.5括号匹配问题

![image-20230321225743416](https://s2.loli.net/2023/03/21/uRvKInVq8lJNofd.png)

![image-20230321235908849](https://s2.loli.net/2023/03/21/CFxD4jZ2AeYTWp7.png)

##### 代码**字符串的运用

```c++
#include<cstdio>
#include<stack>
#include<string>
using namespace std;
int main() {
    char h[150];
    while(fgets(h,200,stdin)!=NULL){//fgets配合while实现未知数量的输入
        string str=h;
        str.pop_back();//去掉额外的换行符
        stack<unsigned> stack1;//存储左括号的下标
        string result;
        for(int i=0;i<str.length();i++){
            result.push_back(' ');
            if(str[i] == '('){
                stack1.push(i);
                result[i]='$';//先认为是非法
            }
            else if(str[i]==')'){
                if(!stack1.empty()) {
                    int j = stack1.top();
                    result[j] = ' ';
                    stack1.pop();
                }
                else{
                    result[i]='?';
                }
            }
        }
        printf("%s",h);
        printf("%s",result.c_str());
    }
    return 0;
}
```

### 表达式解析问题

![image-20230322143014767](https://s2.loli.net/2023/03/22/a74wdWiEksfrbJ3.png)

#### 数据结构设计

```c++
stack<char> operation;
stack<double> num;
```

数字——〉压栈

符号（低优先级）——〉压栈

符号（高优先级）——〉op弹出一个 num弹出两个，进行运算，压入栈中

#### 4.6 ***简单计算器

![image-20230322143522812](https://s2.loli.net/2023/03/22/njEsViOLJAwDcfx.png)

## Chapter5递归和分治

### 递归

#### 5.1 n的阶乘

![image-20230323182531584](https://s2.loli.net/2023/03/23/Yty2iP4ObE8ThKB.png)

##### 代码：

```c++
#include <cstdio>
using namespace std;
long long jiechen(long long n){
    if(n>1)
        return n*jiechen(n-1);
    else
        return 1;
}
int main() {
    long long n;
    scanf("%lld",&n);
    printf("%lld",jiechen(n));
}
```

#### 5.2**汉诺塔

![image-20230323201539646](https://s2.loli.net/2023/03/23/sMwkAcqPz4Vl9gr.png)

假设有解决小问题的能力

![image-20230325154716484](https://s2.loli.net/2023/03/25/7SHi5btUrufePQM.png)

##### 代码：

```c++
#include<cstdio>
long long hannuo(int n){
    if(n==1)
        return 2;
    else
        return 3*hannuo(n-1)+2;
}
int main(){
    int n;
    while(scanf("%d",&n)!=EOF){
        printf("%lld\n",hannuo(n));
    }
    return 0;
}
```

### 分治divide and conquer

从递归到分治

1. 找到大问题到小问题的转移过程（假设小问题已经解决）
2. 找到最小问题的解决方案

####  5.3

![image-20230325173610194](../../../Library/Application%20Support/typora-user-images/image-20230325173610194.png)

##### 代码：

![image-20230325174726293](https://s2.loli.net/2023/03/25/nmLgUToKzscEtBf.png)

#### 分治法的代码模版：

大问题变成小问题（假设小问题已经有解）

最小问题的解决方法

![image-20230325175320478](https://s2.loli.net/2023/03/25/9SFa28HRmklugo1.png)

#### 5.4二叉树

![image-20230325175418492](https://s2.loli.net/2023/03/25/XPetMSf4rYLkZG1.png)

##### 代码

```c++
#include<cstdio>
long long num1(long long m,long long n){
    if(m>n)
        return 0;
    else
        return 1+num1(2*m,n)+num1(2*m+1,n);
}
int main(){
    long long m,n;
    while(scanf("%lld %lld",&m,&n)!=EOF){
        printf("%lld",num1(m,n));
    }
    return 0;
}
```

## Chapter6树形数据结构

值传递 

引用传递==》函数调用完成，会修改参数问题

![image-20230325232341429](https://s2.loli.net/2023/03/25/uy1bLYqOWs94AUd.png)

自由存储空间（申请堆空间）

![image-20230325232929731](https://s2.loli.net/2023/03/25/AMxWKRwL1mJ9tzH.png)

内存泄漏（不关心）

![image-20230325233043542](https://s2.loli.net/2023/03/25/IVszLMfqmk5i2dP.png)

### 二叉树

设计一个类描述节点

```c++
struct TreeNode{
  int data;
	TreeNode * leftchild;
	TreeNode * rightchild;
};
int main(){
  TreeNode *root;
}
```

#### 层次建树

![image-20230326000607026](https://s2.loli.net/2023/03/26/uGo8Rn2HKgQhIZ4.png)

```c++
#include<cstdio>
#include<queue>
using namespace std;
struct TreeNode{
    int data;
    TreeNode *leftchild;
    TreeNode *rightchild;
};
struct QueueNode{
    TreeNode *parent;
    bool isleftin;
};
void InsertTreeNode(TreeNode *&root,queue<QueueNode*> &myQueue,char data){
    if(data!='#'){
        //创建二叉树节点,申请堆空间
        TreeNode *pTreeNode=new TreeNode;
        //(*pNode).data=data;//(*pNode).data等价于pNode->data
        pTreeNode->data=data;
        //队列操作
        QueueNode *pQueueNode=new QueueNode;
        pQueueNode->parent=pTreeNode;
        pQueueNode->isleftin=false;
        myQueue.push(pQueueNode);
        if(root==NULL){
            root=pTreeNode;
        }
        else{
            QueueNode *pparent=myQueue.front();
            if(pparent->isleftin== false){
                pparent->parent->leftchild=pTreeNode;
                pparent->isleftin= true;
            }
            else{
                pparent->parent->rightchild=pTreeNode;
                myQueue.pop();
                delete pparent;
            }
        }

        
    }
    else{
        if(root!=NULL){
            QueueNode *pparent=myQueue.front();
            if(pparent->isleftin== false){
                pparent->parent->leftchild=NULL;
                pparent->isleftin= true;
            }
            else{
                pparent->parent->rightchild=NULL;
                myQueue.pop();
                delete pparent;
            }

        }
    }
}
int main(){
    TreeNode *root=NULL;
    char charlist[]="abc##de#g##f###";
    queue<QueueNode*> myQueue;
    for(int i=0;charlist[i]!='\0';i++){
        InsertTreeNode(root,myQueue,charlist[i]);
    }
    return 0;
}
```

#### 遍历

##### 层次遍历（广度优先遍历）

辅助队列结构

```c++
void LevelOrder(TreeNode *root){
    queue<TreeNode*>pos;
    pos.push(root);
    while(pos.empty()== false){
        TreeNode *pcur=pos.front();
        pos.pop();
        printf("%c",pcur->data);
        if(pcur->leftchild!=NULL){
            pos.push(pcur->leftchild);
        }
        if(pcur->rightchild!=NULL){
            pos.push(pcur->rightchild);
        }
    }
}
```

##### 递归遍历

```c++
void NLRorder(TreeNode *root){
  	if（root==NULL）
      return;
    printf("%c",root->data);
    if(root->leftchild!=NULL)
        NLRorder(root->leftchild);
    if(root->rightchild!= NULL)
        NLRorder(root->rightchild);
}
void LNRorder(TreeNode *root){
    if（root==NULL）
      return;
    if(root->leftchild!=NULL)
        LNRorder(root->leftchild);
    printf("%c",root->data);
    if(root->rightchild!= NULL)
        LNRorder(root->rightchild);
}
void LRNorder(TreeNode *root){
    if（root==NULL）
      return;
    if(root->leftchild!=NULL)
        LRNorder(root->leftchild);
    if(root->rightchild!= NULL)
        LRNorder(root->rightchild);
    printf("%c",root->data);
}
```

#### 重建二叉树

先序+中序







