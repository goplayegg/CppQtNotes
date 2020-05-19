# CppQtNotes
[MarkDown语法教程](https://www.jianshu.com/p/q81RER) 

## [QML](qml.md)

## Qt

####  关闭时析构窗口
```
setAttribute(Qt::WA_DeleteOnClose);
```
####  connect 连接方式区别 

- Qt::DirectConnection：发送信号的线程直接调用槽 多线程危险
- Qt::QueuedConnection：接收者所在线程的消息循环中执行
- Qt::AutoConnection：发和收 在同一个线程 =》DirectConnection
									发和收 不在同一个线程=》QueuedConnection
									
- Qt::BlockingQueuedConnection： 在接收者线程调用， 发送者会阻塞
- Qt::UniqueConnection  按位或（|）结合使用，=》避免重复连接

#### QImage QPixmap
- QImage平台无关 IO操作快 显示慢
- QPixmap平台有关 Windows显示快

## Cpp
####  文件读取in  /  写文件out
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
	
	//写
	string strPath = "d:/3.txt";
	ofstream out(strPath, ios::out | ios::binary|ios::app);
	out.write(pBuff, iLen);
	
```

#### 容器
(1)、vector：可变大小数组。支持快速随机访问。在尾部之外的位置插入或删除元素可能很慢。

(2)、deque：双端队列。支持快速随机访问。在头尾位置插入/删除速度很快。

(3)、list：双向链表。只支持双向顺序访问。在list中任何位置进行插入/删除操作速度都很快。

(4)、forward_list：单向链表。只支持单向顺序访问。在链表任何位置进行插入/删除操作速度都很快。

(5)、array：固定大小数组。支持快速随机访问。不能添加或删除元素。

(6)、string：与vector相似的容器，但专门用于保存字符。随机访问快。在尾部插入/删除速度快。

以下是一些选择容器的基本原则：

(1)、除法你有很好的理由选择其他容器，否则应该使用vector；

(2)、如果你的程序有很多小的元素，且空间的额外开销很重要，则不要使用list或forward_list；

(3)、如果程序要求随机访问元素，应使用vector或deque；

(4)、如果程序要求在容器的中间插入或删除元素，应使用list或forward_list；

(5)、如果程序需要在头尾位置插入或删除元素，但不会在中间位置进行插入或删除操作，则使用deque；

(6)、如果程序只有在读取输入时才需要在容器中间位置插入元素，随后需要随机访问元素，则：首先，确定是否真的需要在容器中间位置添加元素。当处理输入数据时，通常可以很容器地向vector追加数据，然后再调用标准库的sort函数来重排容器中的元素，从而避免在中间位置添加元素。如果必须在中间位置插入元素，考虑在输入阶段使用list，一旦输入完成，将list中的内容拷贝到一个vector中。

#### stl 骚操作
    std::for_each( m_attachedSurfaces.begin(), m_attachedSurfaces.end(),
                   std::bind2nd( std::mem_fun( &QmlVlcVideoSurface::presentFrame ), frame ) );
				   调用成员函数
				   
bind2nd bind1st 将2元函数变成1元 绑定第2/1个参数

#### ms级别时间
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

#### 随机数
```cpp
#include <random>
    default_random_engine randEng(time(nullptr));
    uniform_int_distribution<> dis(1,5);
    int iMyRand = dis(randEng);

```

#### λ表达式
```cpp
auto func = [=](int i)->bool{
	return false;
};

bool b = func(1);
```

## 调试
- windbg 内存泄漏
  1. Set _NT_SYMBOL_PATH  = D:/PdbPath
  2. cd 到windbg安装目录
  3. gflags.exe -i D:/exePath/app.exe +ust    若有空格用\\*转义
  4. umdh.exe -pn:app.exe -f:"D:/1.log"
  5. umdh.exe -pn:app.exe -f:"D:/2.log"
  6. umdh.exe "D:/1.log" "D:/2.log" > "D:/1.txt"
  
 ## 其他
 
 ### github技巧
 高级搜索：  in:name language:c++ stars:>1000    也可以是readme\description
 |字段|必选|类型|说明|
|----|----|----|----|
|spid|false|int|专题编号|
|title|false|string|专题名称|