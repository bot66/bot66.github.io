---
layout: post
title:  "C++中char*, char[], char*[], char**的含义"
date:   2020-10-15 20:44:24 +0800
categories: 2020年
tags: C++
---

```cpp
#include <iostream>

using namespace std;

/*
这个cpp来研究一下字符串的定义方式(不包括string容器方式)，研究一下字符串在c++中的存在形式，
研究一下 char*, char[], char*[], char**。
*/


//1.探索一下字符串在c++中存在的形式
void test01()
{   
    cout << "test01: " << endl;
    //这里定义一个字符指针，用字符串"string"赋了初值，"string"其实被编译器看作是字符's'的地址
    //即字符串的首地址，同理单这个首地址会被编译器认为是"string"
    
    const char* str = "string";
    //输出str，其实str是's'的地址，这个时候cout << str 输出不显示地址，直接打印"string"
    cout << str << endl;
    //然后我们再解引用一下str, cout << *str 发现打印了's',说明"string"确实给的是's'的地址
    cout << *str << endl;
}

//2.探索以下char[]
void test02()
{
    cout << "test02： " << endl;
    //char str[]本质上应该是一个字符数组, 但我们赋的值确实一个字符串，说明编译器其实把字符串
    //看成了一个字符数组
    char str[] = "string";
    cout << str << endl;
    //还能当数组索引呢
    cout << str[0] << endl;
    //str[0]占用一个字节，其实就是字符型占用空间
    cout << sizeof(str[0]) << endl;
    //str占用7个字节，除了看见的6个字符外，还包含一个结束字符'\0',这是字符串数组特有的
    cout << sizeof(str) << endl;
    //输出以下第7个字符'\0'试试
    cout << str[6] << endl; //'\0'转义字符表示NULL

    //试一下正经的定义字符数组方法,这个时候sizeof(str2)就不会多算一个了，即'\0'结束符
    char str2[] = {'H','E','L','L','O'};
    cout << sizeof(str2[0]) << endl;
    cout << sizeof(str2) << endl;

    
}

//3.探索一下char* []和char**
void test03()
{
    cout << "test03: " << endl;
    //char* []很好理解，其实就是一个字符串数组
    const char* str_arr[] = {"str1","str2"};
    cout << str_arr[0] << endl;

    //char**可以这样看(char*)*，即定义了一个指向char指针类型的指针，把str_arr即char*数组
    //的首地址赋值给char**,这个时候char**就成为了一个指向char*数组的指针，从而可以操控char*数组,
    //这个时候char**也变成了一个char*数组。
    
    const char** str_arr2 = str_arr; //str_arr，第一个char*指针的地址
    cout << str_arr2[1] << endl;
    



}

int main()
{
    test01();
    test02();
    test03();
    cin.get();
    return 0;
}
```
