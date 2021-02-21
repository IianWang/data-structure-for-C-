# 第六章 C++标准模板库（STL）介绍
## 6.4 map的常见用法详解
关于使用map，首先要导入 #include < map>
using namespace std;

**数组是不可以作为”键“或"值"被映射的**

**1.定义及访问**

定义eg.

map <string int> mp; //第一个type为键类型，第二个是值类型，map里只接受string类型，char[]不可以

访问：两种方式

下标：mp["a"] //访问名为键a的值

迭代器：
```C++
map <string int>::iterator it = mp.find("a") //find返回的类型是迭代器

for(map <string int>::iterator it = mp.begin(); it != mp.end(); it++){
  printf("%s %d\n", it -> first, it -> second);//first 访问键，second访问值
}
```


**2.常用函数**
- find(key)
- erase()两种
  - mp.erase(it) //it为欲删除的映射的迭代器
  - mp.erase(key) //key为欲删除的映射的键
  - mp.erase(first, last)//first起始迭代器，last末尾迭代器，[fast, last)左闭右开
- size()
- clear()


**3.用途**

(1). 一些涉及到映射的题，可以减少代码量，尤其是字符串作为"键"的
(2). 判断大整数或其它类型的数据是否存在


PAT

```C++
//1100 Mars Numbers (20 分)
//一言难尽的一道题，一上午+半个中午各种调试，几点有用的信息
//getline(cin, strname) 可以读入带有空格的字符串
//scanf和getline交替使用的话，需要在两者之间加一个getchar()吃回车
//有些接受char[]类型的常用函数，如sscanf、printf等如果使用的对象是string，则调用.c_str()转化成char[]
//map["xx"]，map直接索引不存在的键可能会返回0，如果要判断一个键存不存在直接用find()，不存在则返回mp.end()，返回的是迭代器，用个迭代器变量来接收。。
//下面是关于该题的两个总结
//起初读题一度默认给定的字符串是固定格式的"xxx xxx"或者"xxx"这种三位一起的，所以就借助string类型的substr(0, 3),substr(4, 7)，有两个数据点因此出错
//实则忘记考虑了一个字母"tret"是4位的。。。
//另外一个则和常识有关，就是数字在转化火星文后，火星文的整数部分输出后，余数为0，要不要输出0所对应的火星文。题中没有明说也没有给出类似的样例。四分的数据点。
//实际上是不需要输，我们正常数字而言有余数则输出没有则不输出，只能先这么理解了。
//复习+重做
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <math.h>
#include <vector>
#include <set>
#define maxn 100100

using namespace std;

char str1[14][5] = {"tret", "jan", "feb", "mar", "apr", "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};
char str2[14][5] = {"xx", "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo", "syy", "lok", "mer", "jou"};

void trans_print(int n){
    int mod = n % 13;
    int dvd = n / 13;
    if (mod == 0 && dvd == 0) printf("%s\n", str1[dvd]);
    else if (dvd > 0){
        if (mod == 0) {
            printf("%s\n", str2[dvd]);
        }
        else printf("%s %s\n", str2[dvd], str1[mod]);
    }
    else if(mod != 0 && dvd == 0) printf("%s\n", str1[mod]);
    
}

int main(){
    map<string, int> mp1, mp2;
    for (int i = 0; i < 13; i++) {
        mp1[str1[i]] = i;
        mp2[str2[i]] = i;
    }
    int N;
    scanf("%d", &N);
    getchar();
    while (N--) {
        string temp;
        getline(cin, temp);
//        cin >> temp;
        if ('0' <= temp[0] && temp[0] <= '9') {
            int temp_int;
            sscanf(temp.c_str(), "%d", &temp_int);
            trans_print(temp_int);
        }
        else{
            string fir, sec;
            if (temp.find(' ') == -1) {
                map<string, int>::iterator it = mp1.find(temp);
                if (mp1.end() != it) {
                    printf("%d\n", mp1[temp]);
                }
                else printf("%d\n", mp2[temp] * 13);
            }
            else{
                int pos = temp.find(' ');
                fir = temp.substr(0, pos);
                sec = temp.substr(pos + 1, temp.length());
                printf("%d\n", mp2[fir] * 13 + mp1[sec]);
            }
        }
    }

    return 0;
};
```


```C++
//1054 The Dominant Color (20 分)
//通过率超高的一道题0.51
//只考察了map的用法，应该不会在考试中出现
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <math.h>
#include <vector>
#include <set>
#define maxn 100100

using namespace std;

map<int, int> mp;



int main(){
    int M, N;
    scanf("%d %d", &M, &N);
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            int temp;
            scanf("%d", &temp);
            if (mp.find(temp) == mp.end()) {
                mp[temp] = 1;
            }
            else mp[temp]++;
        }
    }
    for (map<int, int>::iterator it = mp.begin(); it != mp.end(); it++) {
//        printf("key = %d, value = %d\n", it -> first, it -> second);
        if (it -> second > M * N / 2) {
            printf("%d\n", it -> first);
        }
    }

    return 0;
};
```

```C++
//1071 Speech Patterns (25 分)
//该题考察字符串分割，再利用map存储为键与值
//目前使用空格进行字符串分割掌握不是很顺畅，尤其是使用string时，错误百出，string末尾添加字符直接+就好了，令末尾等于某字符（char[]的方式）string会出bug，不知道是不是我操作问题
//这道题花费了1个半小时有个4分的数据点没过
//时间大多花费在字符串处理的索引确定上，比如find(str, pos)pos传入的是当前还是下一位？find会从pos这个位置开始找起
//再比如string.substr(pos, len)，len的长度是从pos开始算还是从pos的下一位开始算？len会从pos位置开始算，算len位
//再就是上面提到的bug，总之遇到了就用+吧，先避开
//总结：string系列还是用的不熟
//复习+重做！
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <math.h>
#include <vector>
#include <set>
#define maxn 100100

using namespace std;

map<string, int> mp;

int main(){
    string str;
    getline(cin, str);
    int start = (int)str.find('"');
    int over = (int)str.find('"', start + 1);
    str = str.substr(start + 1, over - start - 1);
    
    for (int i = 0; i <= str.length(); i++) {
        if (str[i] >= 'A' && str[i] <= 'Z') {
            str[i] = str[i] + 32;
        }
        else if(str[i] >= 'a' && str[i] <= 'z'){
            continue;
        }
        else if(str[i] >= '0' && str[i] <= '9'){
            continue;
        }
        else if(str[i] == ' '){
            continue;
        }
        else{
            str.erase(i, 1);
        }
    }
    
//    string temp_str;
    char temp_str[100];
//    printf("%s\n", str.c_str());
    
    int ind = 0;
//    printf("str = %s\n", str.c_str());
    for (int i = 0; i < str.length(); i++) {
        if (str[i] != ' ') {
            temp_str[ind++] = str[i];
        }
        else{
            temp_str[ind] = '\0';
//            printf("temp = %s\n", temp_str);
            if (strcmp(temp_str, "") != 0) {
                
                if (mp.find(temp_str) == mp.end()) {
                    mp[temp_str] = 1;
                }
                else mp[temp_str]++;
                
                ind = 0;
                strcpy(temp_str, "");
            }
        }
//        printf("\n");
    }
    temp_str[ind] = '\0';
    if (strcmp(temp_str, "") != 0) {
        if (mp.find(temp_str) == mp.end()) {
            mp[temp_str] = 1;
        }
        else mp[temp_str] = mp[temp_str] + 1;
        
        ind = 0;
        strcpy(temp_str, "");
    }
    
    string max_name;
    int mx = 0;
    for (map<string, int>::iterator it = mp.begin(); it != mp.end(); it++) {
        if ((it -> second) > mx) {
            mx = it -> second;
            max_name = it -> first;
        }
    }
    printf("%s %d\n", max_name.c_str(), mx);

    return 0;
};

```
