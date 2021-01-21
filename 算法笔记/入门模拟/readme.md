# 第三章 入门篇（1）---- 入门模拟
```C++
//问题 A: 剩下的树
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))

using namespace std;
int main()
{
    int tree, slice;
    int a, b;
    int total = 0;
    int ls[10001] = {0};
//    printf("%d\n", ls[0]);

    while(scanf("%d %d", &tree, &slice), tree || slice){
        for(int i = 0; i <=tree; i++){
            ls[i] = 1;
        }
        for(int j = 0; j <slice; j++){
            scanf("%d %d", &a, &b);
            for(int k = a; k <=b; k++){
                ls[k] = 0;
            }
        }
        for(int z = 0; z <=tree; z++){
            if(ls[z]){
                total++;
            }
        }
        printf("%d\n", total);
        memset(ls, 0, sizeof(ls));
        total = 0;
    }

    return 0;

}



```
