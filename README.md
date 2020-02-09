# CppQtNotes
[MarkDown语法教程](https://www.jianshu.com/p/q81RER) 

## Qt

1. 关闭时析构窗口
```
setAttribute(Qt::WA_DeleteOnClose);
```
2.


## Cpp
1.  文本读取
```cpp
#include <iostream>
#include <fstream>
    using namespace std;
    string strFile = "d:/1.txt";
    ifstream in(strFile, ios::in|ios::binary|ios::ate);
    char *pText=nullptr;
    unsigned int size = in.tellg();
    if(size>0)
    {
        pText = new char[size+1];
        in.seekg(0, ios::beg);
        in.read(pText,size);
        pText[size]=0;
    }
    string strText = string(pText);
```
2. ms级别时间
```cpp
#include <chrono>
using namespace std;
using chrono::high_resolution_clock;
using chrono::milliseconds;
    auto tpStart = high_resolution_clock::now();
    auto tpEnd = high_resolution_clock::now();
    auto timeInter = chrono::duration_cast<milliseconds>(tpEnd -tpStart);
    qDebug()<<timeInter.count()<<"ms";
```

3. 随机数
```cpp
#include <random>
    default_random_engine randEng(time(nullptr));
    uniform_int_distribution<> dis(1,5);
    int iMyRand = dis(randEng);

```