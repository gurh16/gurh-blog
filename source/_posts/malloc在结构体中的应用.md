---
title: malloc在结构体中的应用
date: 2021-08-23 0:22
tags: [course,blog]
categories: C programming
number: 1
---

### malloc在结构体中的应用

------

​	在SEE222的第一个project中，我们被要求使用c语言+arduino mega2560 实现一个银行系统。关于addAccount()的实现部分，笔者思来想去，决定使用malloc函数实现结构体的动态实例化。此方式可以实现通过多次调用一个函数来实现多个结构体变量的实例化。

结构体：

```c
struct accounts
{
  char name[25];
  char cardNumber[4];
  char password;
  char expiryDate[4];
  int balance;
};
```

- 首先在main函数外使用`accounts *g_accounts[1024];`声明一个结构体指针。

- 创建计数函数g_count `int g_count = 0;`。

- 在addAccount的implementation中使用如下语句对accounts结构体进行实例化（第*g_count*er个实例变量）并分配空间：

```c
g_accounts[g_counter] = (accounts*)malloc(sizeof(accounts));
```

- 在操作某个实例的值时，使用`g_accounts[g_counter]->成员`来访问某一结构体实例中的某成员。

- 最后别忘了加上`g_counter++`.

------

完整示例代码：

```c
int g_counter = 0; //声明结计数变量
struct accounts //创建结构体
{
  char name[25];
  char cardNumber[4];
  char password;
  char expiryDate[4];
  int balance;
};
accounts *g_accounts[1024]; //声明一个结构体指针

void addAccount(){
  g_accounts[g_counter] = (accounts*)malloc(sizeof(accounts); //实例化并分配空间
  scanf("%s",(g_accounts[g_counter]->name)); //操作结构体实例中的成员
}
```

