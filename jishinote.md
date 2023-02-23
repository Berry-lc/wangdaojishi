# 王道机试笔记

## chapter1枚举和模拟

1.1

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

