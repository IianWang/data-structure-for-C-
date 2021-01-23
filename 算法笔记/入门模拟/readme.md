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

```C++
//A+B和C (15)
//题中说明输入在[-2^31, 2^31]之间
//int 类型可承受的范围在-2^31 ~ 2^31 - 1，两个边缘的数求和必然是超出2^31，故结束类型需要定义long long（格式符为  "%lld"）
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
    long long A, B, C;//int 最大范围是2^31 -1
    int T, n = 1;
    scanf("%d", &T);
    while(T--){
        scanf("%lld %lld %lld", &A, &B, &C);
        printf("Case #%d: %s\n", n, A + B > C? "true":"false");
        n++;
    }
    return 0;
}

```
```C++
// 数字分类 (20)
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 100001

void compute(int ls[], int N){
    int sum_a = 0;
    int ls_b[1001], b = -1, sum_b = 0, n2 = 0;
    int c = 0;
    double d = 0, sum_d = 0;
    float avg_d;
    int f1 = 0, f2;
    for(int i = 0; i <N; i++){
        if((ls[i] % 5 == 0) && (ls[i] % 2 == 0)) sum_a += ls[i];
        if(ls[i] % 5 == 1){
            b *= -1;
            sum_b += ls[i] * b;
            n2 += 1;
        }
        if(ls[i] % 5 == 2) c++;
        if(ls[i] % 5 == 3){
            sum_d += ls[i];
            d++;
        }
        if(ls[i] % 5 == 4){
            if(f1 < ls[i]) f1 = ls[i];
        }
    }

    if(sum_a == 0) printf("N ");
    else printf("%d ", sum_a);
    if(n2 == 0) printf("N ");
    else printf("%d ", sum_b);
    if(c == 0) printf("N ");
    else printf("%d ", c);
    if(d == 0) printf("N ");
    else printf("%.1f ", sum_d / d);
    if(f1 == 0) printf("N\n");
    else printf("%d\n", f1);

}

using namespace std;
int main()
{
    int ls[1001];
    int N;
    while(scanf("%d", &N) != EOF){
        for(int i = 0; i <N; i++){
            scanf("%d", &ls[i]);
        }
        compute(ls, N);
    }
    return 0;
}

```

```C++
//部分A+B (15)
//pow返回的其实是double型,有的时候会偏差那么一丢丢精度，需要适当取整；
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

    long long A, B;
    int a, b;
    while(scanf("%d %d %d %d", &A, &a, &B, &b) != EOF){

        char ls_a[15], ls_b[15];
        char str_a, str_b;
        int n1 = 0, n2 = 0;
        int sum_a = 0, sum_b = 0;

        sprintf(ls_a, "%d", A);
        sprintf(ls_b, "%d", B);
        str_a = a + '0';
        str_b = b + '0';
        for(int i = 0; i <strlen(ls_a); i++){
            if(str_a == ls_a[i]) n1++;
        }
        for(int i = 0; i <strlen(ls_b); i++){
            if(str_b == ls_b[i]) n2++;
        }
        for(int i = 0; i <n1; i++){
            sum_a += a * ceil(pow(10, i));
        }
        for(int i = 0; i <n2; i++){
            sum_b += b * ceil(pow(10, i));
        }
        printf("%d\n", sum_a + sum_b);
    }
    return 0;
}

```
```C++
//该题核心在于将B、C、J三者转化为数字之后，通过简单运算数字比大小从而判断输赢，亮点在(k1 + 1) % 3 == k2成立恰好说明选手a赢选手b
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
const double eps = 1e-8;
const double pi = acos(-1);
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 100001

int trans(char p){
    if(p == 'B') return 0;
    if(p == 'C') return 1;
    if(p == 'J') return 2;

}

using namespace std;
int main()
{

    int N;
    char A, B;
    int n_a = 0, n_b = 0, n = 0;
    char ls_info[4] = {'B', 'C', 'J'}, ls_copy_a[4], ls_copy_b[4];
    int a_ls[4] = {0}, b_ls[4] = {0};
    int k1, k2;
    scanf("%d", &N);
    for(int i = 0; i <N; i++){
        getchar();
        scanf("%c %c", &A, &B);
        k1 = trans(A);
        k2 = trans(B);
        if((k1 + 1) % 3 == k2){
            n_a++;
            a_ls[k1]++;
        }
        else if(k1 == k2){
            n++;
        }
        else{
            n_b++;
            b_ls[k2]++;
        }
    }
    printf("%d %d %d\n", n_a, n, n_b);
    printf("%d %d %d\n", n_b, n, n_a);
    // 下段语句可作为寻找数组种最大元素的位置的通用语句，比冒泡排序复杂度低，更易于理解
    int id1 = 0, id2 = 0;
    for(int i = 0; i <3; i++){
        if(a_ls[id1] < a_ls[i]) id1 = i;
        if(b_ls[id2] < b_ls[i]) id2 = i;
    }
    printf("%c %c", ls_info[id1], ls_info[id2]);

    return 0;
}

```
## 练习册上的题
```C++

```
