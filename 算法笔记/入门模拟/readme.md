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


```C++
//问题 B: A+B
//该题一开始就想复杂了，在复杂的基础上修改bug过于浪费时间
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))

void trans(char ls[]){
    char temp[20] = {0};
    int n = 0;
    for(int i = 0; i <strlen(ls); i++){
        if(ls[i] != ','){
            temp[n++] = ls[i];
        }
    }
    memset(ls, 0, sizeof(ls));
    strcpy(ls, temp); // temp 在定义的时候要初始化为0，不然ls结尾有乱码
}

using namespace std;
int main()
{
    int b = 0;
    char ls_str[2][20];

    while(scanf("%s %s", ls_str[0], ls_str[1]) != EOF){
        char str[20];
        int a = 0;
        for(int i = 0; i <2; i++){
            strcpy(str, ls_str[i]);
            trans(str);
            sscanf(str, "%d", &b);
            a += b;
        }
        printf("%d\n", a);
    }

    return 0;
}

```

```C++
//比较奇偶数个数
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
    int N;
    int a = 0, b = 0;
    int ls[1001];


    while(scanf("%d", &N) != EOF){
        for(int i = 0; i <N; i++){
            scanf("%d", &ls[i]);
            if(ls[i] % 2 == 1){
                a++;
            }
            else b++;
        }
        if(a > b) printf("YES\n");
        else printf("NO\n");

    }
    return 0;
}

```

```C++
//Shortest Distance (20)
//该题要求时间复杂度不能大于10e7，如果是嵌套循环的话复杂度达到10e9，后续每道题需首先确定清楚题中有没有明确要求复杂度
//该题中心思想，求一条直线上任意两点距离，只需求得这两点分别到零点的距离之差（加绝对值），故制作一个"累加"数组可以替代遍历求和
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 100001

using namespace std;
int main()
{
    int N, n, a, b, sum = 0, dest_acc, dest_dev;
    int big, smal;
    int ls[maxn];
    int ls_acc[maxn];//优化后添加个记录累加的数组ls_acc:正向累加
    scanf("%d", &N);
    for(int i = 0; i <N; i++){
        ls_acc[i] = sum;
        scanf("%d", &ls[i]);
        sum += ls[i];
    }

    scanf("%d", &n);

    while(n--){
        scanf("%d %d", &a, &b);
        //删掉传统的嵌套遍历
        dest_acc = fabs(ls_acc[a - 1] - ls_acc[b - 1]);
        if(dest_acc > sum - dest_acc) printf("%d\n", sum - dest_acc);
        else printf("%d\n", dest_acc);

    }
    return 0;
}

```
