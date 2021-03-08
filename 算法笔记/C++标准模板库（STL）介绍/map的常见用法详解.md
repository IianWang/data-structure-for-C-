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

//二刷代码，map<string, int>字符串遍历很方便，不过还是在第三个数据点报错，看其他的教程发现原因在于我将key入map的是读到' '作为触发条件，从样例来看显然是这样
//不过巧的是如：aaa///bbb，空格为条件则会出现aaabbb连在一起，但实际上aaa、bbb两个，故将空格为触发条件改为不为数字、小写、大写字母之外的所有字符，都写在了judge里
#include <iostream>
#include<bits/stdc++.h>
const double eps = 1e-8;
const double odds = 0.65;
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 51
const int INF = 100000000;
using namespace std;
map<string, int> mp;

bool judge(char s){
    if('0' <= s && s <= '9') return true;
    if('a' <= s && s <= 'z') return true;
    if('A' <= s && s <= 'Z') return true;
    return false;
}

int main()
{
    string str, temp = "";
    getline(cin, str);
    for(int i = 0; i < str.length(); i++){
        if(judge(str[i]) == false && temp.length() > 0){
            if(mp.find(temp) != mp.end()){
                mp[temp]++;
            }
            else mp[temp] = 1;
            temp = "";
            continue;
        }
        else if(('0' <= str[i] && str[i] <= '9') || ('a' <= str[i] && str[i] <= 'z')) temp += str[i];
        else if('A' <= str[i] && str[i] <= 'Z') temp += (str[i] + 32);
    }

    if(temp.length() > 0){
        if(mp.find(temp) != mp.end()){
            mp[temp]++;
        }
        else mp[temp] = 1;
    }
    int MAX = 0;
    string temp2 = "";
    for(map<string, int>::iterator it = mp.begin(); it != mp.end(); it++){
        if(it -> second > MAX) {
            MAX = it -> second;
            temp2 = it -> first;
        }
    }
    printf("%s %d\n", temp2.c_str(), MAX);

    return 0;
}

```

```C++
//1022 Digital Library (30 分)
//优先复习！
//考察点1：map<type, set<type>> 这种嵌套映射的使用及如何作为参数传入函数
//考察点2：“xxx xxx xxx”带空格的字符串，如何以空格为分割按单词进行读取（while(cin读取单词) getchar读取空格，getchar最后一次读取的是回车检测到就跳出while，好用！）
//考察点3：多种读取函数之间的配合，如果cin或scanf读取的和getline不是一行的内容，那么它们两个之间要加getchar读取空格，否则getline就会把后面的换行读入

//几个新get的点
//using namespace std;要紧接着#include...声明，如果放到一些类型声明之后，会出现意想不到的错误
//string这个模块find和substr在期间尝试比较多

#include <iostream>
#include <stdio.h>
#include <math.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <set>
const double eps = 1e-8;
const double odds = 0.65;
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 100010
using namespace std;

map<string, set<int> > title, author, keyword, publisher, year;

void query(map<string, set<int> >& mp, string& str){//这里加上引用是为了对数据量大的数据点避免超时，map, string的参数传递较慢
    if(mp.find(str) == mp.end()) printf("Not Found\n");
    else{
        for(set<int>::iterator it = mp[str].begin(); it != mp[str].end(); it++){
            printf("%07d\n", *it); //两个数据点因为这个07所影响
        }
    }
}

int main()
{

    int N;
    string tit, aut, key, pub, yr;
    cin >> N;
    while(N--){
        int book;
        cin >> book;
        getchar();

        getline(cin, tit);
        title[tit].insert(book);
        getline(cin, aut);
        author[aut].insert(book);

        while(cin >> key){
            keyword[key].insert(book);
            char c = getchar(); 
            if(c == '\n') break;
        }

        getline(cin, pub);
        publisher[pub].insert(book);

        getline(cin, yr);
        year[yr].insert(book);
        }

    int M, no;
    string temp;
    cin >> M;
    for(int i = 1; i <= M; i++){
        scanf("%d: ", &no);
        getline(cin, temp);
        cout << no << ": " << temp << '\n';
        if(no == 1) query(title, temp);
        else if(no == 2) query(author, temp);
        else if(no == 3) query(keyword, temp);
        else if(no == 4) query(publisher, temp);
        else if(no == 5) query(year, temp);


    }

    return 0;
}
```
