# 晴神的算法笔记课后习题记录

![PAT甲级考纲](/image//1031614663260_.pic_hd.jpg)

### 作业比赛编号 : 100000571 - 《算法笔记》2.7小节——C/C++快速入门->指针

```C++
C语言10.16
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>



void find_smallest(int *ls){
    int* temp = ls;
    int num;
    for(int* base = ls; base <&ls[10]; base++){
        if(*temp > *base){
            temp = base;
        }
    }
    num = *ls;
    *ls = *temp;
    *temp = num;

}

void find_biggest(int *ls){
    int* temp = ls;
    int num;
    for(int* base = ls; base <&ls[10]; base++){
        if(*temp < *base){
            temp = base;
        }
    }
    num = ls[9];
    ls[9] = *temp;
    *temp = num;

}


using namespace std;
int main()
{
    int ls[11] = {0};
    int *p = ls;
    for(int i = 0; i <10; i++){
        scanf("%d", &ls[i]);
    }

    find_smallest(p);
    find_biggest(p);
    for(int* i = ls; i <&ls[10]; i++){
        printf("%d ", *i);
    }


    return 0;
}

```

### 《算法笔记》2.8小节——C/C++快速入门->结构体(struct)的使用
```C++
\\问题 A: C语言11.1
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>

struct person {
    char name[20];
    int counts;
}leader[3] = {"Li",0,"Zhang",0,"Fun",0};

using namespace std;
int main()
{
    int n = 0;
    char candidate[10];

    scanf("%d", &n);
    for(int i = 0; i <n; i++){
        scanf("%s", candidate);
        if(strcmp(candidate, "Li") == 0) leader[0].counts++;
        else if(strcmp(candidate, "Zhang") == 0) leader[1].counts++;
        else if(strcmp(candidate, "Fun") == 0) leader[2].counts++;
    }

    for(int j = 0; j <3; j++){
        printf("%s:%d\n", leader[j].name, leader[j].counts);
    }

    return 0;
}



```

```C++
\\问题 B: C语言11.2
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>

struct student {
    int num;
    char name[20];
    char sex;
    int age;
    student *pointer;
};


using namespace std;
int main()
{
    int n = 0;
    student info[3];
    student* info_pt = info;


    scanf("%d", &n);
    for(int i = 0; i <n; i++){
        info_pt = &info[i];
        scanf("%d %s %c %d", &(*info_pt).num, (*info_pt).name, &(*info_pt).sex, &(*info_pt).age);

        }
//
//
    for(int i = 0; i <n; i++){
        info_pt = &info[i];
        printf("%d %s %c %d\n", (*info_pt).num,(*info_pt).name, (*info_pt).sex, (*info_pt).age);
    }
    return 0;

}


```

```C++
\\问题 C: C语言11.4
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>

struct stu_tec{
    int num;
    char name[10];
    char sex;
    char job;
    union {
        int classes;
        char position[10];
    }category;
};


using namespace std;
int main()
{
    stu_tec ls[100];
    int n;

    scanf("%d", &n);
    for(int i = 0; i <n; i++){
        scanf("%d %s %c %c", &ls[i].num, &ls[i].name, &ls[i].sex, &ls[i].job);
        if(ls[i].job == 's') scanf("%d", &ls[i].category.classes);
        if(ls[i].job == 't') scanf("%s", &ls[i].category.position);
    }

    for(int j = 0; j <n; j++){
        printf("%d %s %c %c ", ls[j].num, ls[j].name, ls[j].sex, ls[j].job);
        if(ls[j].job == 's') printf("%d\n", ls[j].category.classes);
        if(ls[j].job == 't') printf("%s\n", ls[j].category.position);
    }

    return 0;

}

```

```C++
\\问题 D: C语言11.7
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>

struct student{
    int num;
    char name[20];
    int score_1;
    int score_2;
    int score_3;
};

void input(int n,student ls[]){
    for(int i = 0; i <n; i++){
        scanf("%d %s %d %d %d", &ls[i].num, &ls[i].name, &ls[i].score_1, &ls[i].score_2, &ls[i].score_3);
    }
}

void print(int n,student ls[]){
    for(int i = 0; i <n; i++){
        printf("%d %s %d %d %d\n", ls[i].num, ls[i].name, ls[i].score_1, ls[i].score_2, ls[i].score_3);
    }
}

using namespace std;
int main()
{
    student ls[10];
    int n = 5;

    input(n, ls);
    print(n, ls);



    return 0;

}
```

```C++
\\问题 E: C语言11.8
#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>

struct student{
    int num;
    char name[20];
    double score_1;
    double score_2;
    double score_3;
    student *pointer;
};

void input(int n,student ls[]){
    for(int i = 0; i <n; i++){
        scanf("%d %s %lf %lf %lf", &ls[i].num, &ls[i].name, &ls[i].score_1, &ls[i].score_2, &ls[i].score_3);
    }
}

void avg_class(int n, student ls[]){
    double temp_score_1 = 0, temp_score_2 = 0, temp_score_3 = 0;//这里得定义double , int 与 double 相加会出错
    for(int j = 0; j <n; j++){
        temp_score_1 += ls[j].score_1;
        temp_score_2 += ls[j].score_2;
        temp_score_3 += ls[j].score_3;
    }
    printf("%.2f %.2f %.2f\n", temp_score_1 / n, temp_score_2 / n, temp_score_3 / n);
}

void find_biggest(int n, student ls[], student *p){
    int temp_ls[100], user_score;
    int *temp_pt = temp_ls;
    int i = 0, j = 0;
    for(int j = 0; j <n; j++){
        user_score = 0;
        user_score += ls[j].score_1;
        user_score += ls[j].score_2;
        user_score += ls[j].score_3;
        temp_ls[j] = user_score / 3;
    }
    for(int k = 0; k <n - 1; k++){
        if(*temp_pt < temp_ls[k + 1]){// 寻找最大键所对应的值，只需给键和值分别一个指针，会很方便
                temp_pt = &temp_ls[k + 1];
                p = &ls[k + 1];
        }
    }
    printf("%d %s %.0f %.0f %.0f\n", p ->num, p ->name, p ->score_1, p ->score_2, p ->score_3);
}

void print(int n,student ls[]){
    for(int i = 0; i <n; i++){
        printf("%d %s %f %f %f\n", ls[i].num, ls[i].name, ls[i].score_1, ls[i].score_2, ls[i].score_3);
    }
}

using namespace std;
int main()
{
    student ls[10];
    student *pt = ls;
    int n = 10;

    input(n, ls);
    avg_class(n, ls);
    find_biggest(n, ls, pt);


    return 0;

}
```
