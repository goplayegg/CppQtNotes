# CppQtNotes
[MarkDown语法教程](https://www.jianshu.com/p/q81RER) 

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
```
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