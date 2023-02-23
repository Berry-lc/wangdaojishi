# 王道机试笔记

## chapter1枚举和模拟

1.1

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

1.2

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

1.3

![image-20230223235729628](https://p.ipic.vip/z39wjz.png)

![image-20230224003438399](https://cdn.jsdelivr.net/gh/Berry-lc/wangdaojishi@pic/uPic/image-20230224003438399.png)
