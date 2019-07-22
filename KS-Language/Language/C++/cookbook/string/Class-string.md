# string
```md
string类是一个模板类，位于名字空间std中
```
* #include <string>
```md
注意这里不是string.h，string.h是C字符串头文件。

通常为方便使用还需要增加：
   using namespace std;
```
* 声明
```C++
string str;
```
* 方法
* * const char *c_str();
```md
返回字符串地址，是一个c函数，返回类型const char*
c_str()函数返回一个指向正规C字符串的指针常量, 内容与本string串相同。
这是为了与c语言兼容，在c语言中没有string类型，故必须通过string类对象的成员函数c_str()把string 对象转换成c中的字符串样式。
注意：一定要使用strcpy()函数 等来操作方法c_str()返回的指针。
```

* 实例
```C++
#include <iostream>
#include <string>
using namespace std;
int main ( )
{
    string str;  //定义了一个空字符串str
    str = "Hello world";   // 给str赋值为"Hello world"
    char cstr[] = "abcde";  //定义了一个C字符串
    string s1(str);       //调用复制构造函数生成s1，s1为str的复制品
    cout<<s1<<endl;
    string s2(str,6);     //将str内，开始于位置6的部分当作s2的初值
    cout<<s2<<endl;
    string s3(str,6,3);  //将str内，开始于6且长度顶多为3的部分作为s3的初值
        cout<<s3<<endl;
    string s4(cstr);   //将C字符串作为s4的初值
    cout<<s4<<endl;
    string s5(cstr,3);  //将C字符串前3个字符作为字符串s5的初值。
    cout<<s5<<endl;
    string s6(5,'A');  //生成一个字符串，包含5个'A'字符
    cout<<s6<<endl;
    string s7(str.begin(),str.begin()+5); //区间str.begin()和str.begin()+5内的字符作为初值
    cout<<s7<<endl;
    return 0;
}
```
