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
//scanf和getline交替使用的话，需要在两者之间加一个getchar()吃回车
//有些接受char[]类型的常用函数，如sscanf、printf等如果使用的对象是string，则调用.c_str()转化成char[]
//map["xx"]，map直接索引不存在的键可能会返回0，如果要判断一个键存不存在直接用find()，不存在则返回mp.end()，返回的是迭代器，用个迭代器变量来接收。。
//下面是关于该题的两个总结
//起初读题一度默认给定的字符串是固定格式的"xxx xxx"或者"xxx"这种三位一起的，所以就借助string类型的substr(0, 3),substr(4, 7)，有两个数据点因此出错
//实则忘记考虑了一个字母"tret"是4位的。。。
//另外一个则和常识有关，就是数字在转化火星文后，火星文的整数部分输出后，余数为0，要不要输出0所对应的火星文。题中没有明说也没有给出类似的样例。四分的数据点。
//实际上是不需要输，我们正常数字而言有余数则输出没有则不输出，只能先这么理解了。
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
