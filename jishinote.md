# 王道机试笔记

## chapter1枚举和模拟

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

 

