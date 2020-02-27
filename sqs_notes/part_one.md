[TOC]

---

<u>**非指针类：**</u>
![7658cf17e8688da3a15c35a2f24d5c6f.png](en-resource://database/1010:1)


### C++编程简介

#### 目标

- 培养正规的、大气的编程习惯
- 以良好的方式编写C++ class（**基于对象（Objected Based**））
    - class without pointer menbers--Complex（复数）
    - class with pointer members--String（字符串）

**这里的复数与字符串为举例**

- 学习Classes之间的关系（**面向对象（Objected Oriented）**）
    - 继承（inheritance）
    - 复合（composition）
    - 委托（delegation）

#### C++介绍

**C++：**
- C++语言
- C++标准库

#### C vs C++ 关于数据和函数
![fc002e8f0613b8b7bcfd643046f54c97.png](en-resource://database/685:1)

#### Object Based（基于对象）vs Object Oriented（面向对象）

- **Object Based**：面对的是单一class的设计
- **Object Oriented**：面对的是多重classes的设计，class和class之间的关系

#### C++ programs 代码基本形式

![6469151c63e3ad9016809d8acf558ca8.png](en-resource://database/687:1)

#### Output C++ vs C

![79528f3bff6884ab263e460564c0145f.png](en-resource://database/689:1)

### 头文件与类的声明

#### Header（头文件）中的防卫式声明
![1862517b9cefefde4826479d58f33d1b.png](en-resource://database/691:1)

防卫式声明：当头文件在第一次被included的时候进行定义，重复included时不会进入中间的代码区域，起到了防止重定义的作用 

#### Header（头文件）的布局

![29ee3b25dd72815811b007dcc9f4d7df.png](en-resource://database/693:1)

#### class的声明（declaration）

![c7d1f9ac18b52aae6b6077d1bdcbf5fc.png](en-resource://database/695:1)

#### Class template（模板）简介

![3909621482c3b618882d0ab6200e2286.png](en-resource://database/697:1)

### 构造函数

#### inline（内联）函数

![bedcdf453e441ca438f3d4ea01da9a2d.png](en-resource://database/699:1)

内联函数：函数在class body内完成定义。内联函数具备宏定义的特性（优点），但通常函数过于复杂便无法inline，inline只是相当于对编译器的一种建议，能否成为inline是编译器自行决定

#### access level （访问级别）

![8397000d3812fa3ee6666885ce562172.png](en-resource://database/701:1)
访问级别还包含：protected，通常函数为public，变量为


#### consructor（ctor 构造函数）

![59e8c83a82a718c88d6f9906557db0d3.png](en-resource://database/703:1)
<u>**构造函数：**</u>
- 创建对象时自动被调用
- 构造函数名称==类的名称
- 没有返回值类型
- 可以拥有初始列（初值列initialization list）

构造函数可以对变量进行初始化或对其赋值（assignments），建议使用初始化，且还须知道，函数（不只构造函数）是可以有默认实参的（default argument），此时介绍的class中是不包含指针的，通常不包含指针的类无需析构函数

#### ctor（构造函数）可以有多个overloading（重载）

![655c6bed5f0c85a5b8de663039db2660.png](en-resource://database/705:1)

实际应用中，创建一个class往往需要多种方法，因此需要对其ctor进行多次overloading，重载的函数实际名称取决于编译器，当然不只构造函数可以被重载

**<u>图中的两个ctor会发生冲突，因为ctor1的参数有默认值，在创建对象时，编译器会不知道应调用ctor1还是ctor2</u>**


#### constructor（ctor 构造函数）被放在private区

![4d0f2932df7bece8043ded22cc30fd22.png](en-resource://database/707:1)

当构造函数被放置private区，外界无法创建该class的对象，单例模式就是如此。 

![f90e628f579e6c110a2a4a8a08181b8e.png](en-resource://database/709:1)

#### const member function（常成员函数）

![5d4c184845d9548673689f37fe69c00b.png](en-resource://database/711:1)

class中的function包含：
- 改变数据内容
- 不改变数据内容（加上const）

在创建class的const实例，且class中的function没有加const会出现无法调用函数的error

### 参数传递与返回值

#### 参数传递：pass by value vs pass by reference（to const）

![f4b799294303a26e3ccfffd17a1bd809.png](en-resource://database/713:1)

- pass by value：value整包传过去，value压到栈（**此处感觉是传递了复制的**）
- pass by reference：加快传参的速度，
- pass by reference to const：传递引用有被更改数据的风险，若不想更改可以在参数前加上const
- c语言中，当value过大，可以传指针

#### 返回值传递：renturn by value vs  return by  reference（to const）

![e73df52317a34601477be70fba5bba11.png](en-resource://database/715:1)

#### friend（友元）

![20e20fb469e3fe1c6c813a60d2e26517.png](en-resource://database/717:1)

friend可以获取class的private成员
friend不易太多，因为其打破了封装性

#### 相同class的各个objects互为friends（友元）

![1f42ba7813c0575c6bec6ca7803552bc.png](en-resource://database/719:1)

相同class的各个objects互为friends（友元），因此图中的函数不需要firend关键词

#### class body 外的各种定义（definitions）什么情况下pass by reference 什么情况下return by reference

![30e3434dc0563097e4437a4250fa6b71.png](en-resource://database/721:1)

local objecct 不要被return by reference

### 操作符重载与临时对象

#### operator overloading（操作符重载-1 成员函数）this

![8e372d89fdbebe2ed7359cc496ee7cfb.png](en-resource://database/725:1)
所有的成员函数包含了一个隐藏参数this，调用该成员函数的object即是this，例中c2便是this，而this是一个指针，编译器会将c2的指针传进函数

#### return by reference语法分析：传递者无需知道接收者是以reference形式接受

![adb7e92c5d27c32ff4f24b5f15dbd0c0.png](en-resource://database/727:1)

```c++
//接收是complex&，按reference接收的
inline complex&
__doapl(complex* this,const complex& r)
{
    ...
    //返回的是by value，返回了一个object
    return *this
}
```
```c++
    //该语句是先将c1加到c2，结果加到c3上
    c3 += c2 += c1;
    //c2与c1结果需要作为右值 加到c3身上
    //所以本例中的重载函数不可以为void
```

#### class body之外的各种定义（definitions）

全局函数：
![a12ec16abd71604ffd8c231d4dc625e7.png](en-resource://database/729:1)

#### operator overloading（操作符重载-2 非成员函数）（无this）

多次重载+：
![87ef47d16dabc8c2a2245c548212f247.png](en-resource://database/731:1)

 #### temp object（临时对象）typename()；

![a743ec5f73e9327c1daa0fe0e635b100.png](en-resource://database/733:1)
typename();该形式会创造临时对象，是一个local object不可以return by reference

```c++
//这两句话皆是临时对象，生命周期到这句话运行结束
complex();
complex(4,5);
```

#### class body 之外的各种定义（definitions）

![63ec2f376dca5db1d74e69581f7b3dcb.png](en-resource://database/735:1)
此处重载的不是加法而是正号和负号，同样重载负号时，因为对改变了传进来的complex，因此需要临时存储也就是local object，返回时不能return by reference
而正号重载时没有更改变量，没有local object，理论上是可以改为return by reference

#### operator overloading （操作符重载），非成员函数

![b7720b673e8db5dde97de55ef77e5731.png](en-resource://database/737:1)
重载操作符可以有两种选择：
- 定义为全局函数
- 定义为成员函数

**重载<<(特殊)：**
- <<是作用于左侧的cout，所以重载<<时应选择为全局函数，如果选择成员函数大概要写成complex << cout;
- 而cout 的type那么为ostream，在其作为参数时不可以加const，因为每次在cout时相当于都改变了os的状态
- 考虑到连续cout的情况，返回值不应该是void，应该还返回cout即ostream

 ### 三大函数：拷贝函数、拷贝复制、析构
 
 #### String class及三大函数
 
 ![7095741cbcad13777d466f768272e352.png](en-resource://database/908:1)
 
 ![210861204eb42e5299b2012405a25d92.png](en-resource://database/910:1)
 
 #### ctor和dtor（构造函数和析构函数）
 
 ![b83c1187b1add1b5776131f1ea5bca15.png](en-resource://database/912:1)
 
 #### class with pointer members必须有copy ctor和copy op=
 
 ![0f7b13d8a03053f1295cb2c3730b6353.png](en-resource://database/914:1)
**浅拷贝**：因为a、b为指针并不是字符串本身，使用默认拷贝构造或=，使得b的指针指向了a指针指向的内容，b原先指向的那块内存发生了内存泄漏memory lack，而ab同时指向一块内存会造成改变a时b也跟着改变的问题。为了避免发生浅拷贝所造成的的问题，需要采用**深拷贝**

#### copy ctor（拷贝构造函数）

![48d495d0d447363e93e5d6d2e5b1461e.png](en-resource://database/916:1)
深拷贝：
- 分配足够的空间
- 将内容复制到新的内存空间

#### copy assignment operator（拷贝赋值函数）

![885771907a0108328535669c1aca932a.png](en-resource://database/918:1)

拷贝赋值：
- a = b；
- a = a; 自我赋值

当a与b都有内容的时候，想完成如上的赋值操作，需要先将a的内存清空，重新分配足够容纳b内容的内存，再将b的内容拷贝过来

自我赋值的检测
```C++
if(this == &str)
    return *this;
```
this是函数的默认参数
判读传进来的引用与this指向是否为同一块内存

#### 一定要在operator中检测是否self assignment

![d6e3ab2adf0c593b7d2c87ad9b227099.png](en-resource://database/920:1)

#### output 函数

非成员函数（全局函数）：
把指针丢给<<
![78020d872685ab46a7eb8094110cef04.png](en-resource://database/956:1)


### 堆、栈与内存管理

#### 所谓stack（栈），所谓heap（堆）

![07384072209e7751989dfab4c3a39409.png](en-resource://database/958:1)

#### stack objects的生命期

![9369dc7be838ffe135434326e1ee5486.png](en-resource://database/960:1)

#### static local objects的生命期

![926aa1d00c8b9c777f33b22805215652.png](en-resource://database/962:1)

#### global objects的生命期

![6cda95e47209b2c46fbfe88e1ba18b19.png](en-resource://database/964:1)

#### heap objects的生命期

![db23f7051260774be3ed79a5ea2d2da4.png](en-resource://database/966:1)
new完要记得delete，否则会造成内存泄漏

#### new：先分配memory，在调用ctor

![555f476244f206db29f4e4e653ff507e.png](en-resource://database/968:1)

#### delete：先调用dtor，再释放memory

![94373dd95d52c1559a1fddf30360cd9d.png](en-resource://database/970:1)

operator new与operator delete 是C++的特殊函数

#### 动态分配得到的内存块（memory block），in vc

![16bb2fd766af13c1826713e0743b9bf3.png](en-resource://database/972:1)

**class complex：**
- class本身8个字节
- **debug mode：** 前面8 * 4个字节，后面4个字节 
- cookie：前后各4字节
- 占用内存：每一块分配内存必须是16的倍数，所以得到的内存块是64字节

**release mode：**
- complex+cookie = 16

**cookie的作用**：记录分配内存的大小。
cookie的值：
- debug mode：64的16进制数是40，cookie的数字是41，最后一个数字1代表着获得内存
- release mode：16的16进制为10，最后一位1，所以为11

这也说明了为什么使用16的倍数，最后四个位都是零

**class string：**
debug：
- class：4字节
- debug mode：32+4
- cookie：4 * 2
- 占用内存：48
- cookie值：31

release：
- class：4字节
- cookie：4 * 2
- 补充：4
- 占用内存：16
- cookie值：11

#### 动态分配所得的array，in vc

![ff655a0a99340f1dee73a2acacf9aa07.png](en-resource://database/974:1)
- new typename[];：术名array new
- delete[] name;：array delete

-array情况下会再多4字节：用一个整数记录储存数组的个数

#### array new一定要搭配array delete

![76891c2c4552478560ded8ae3cb99acc.png](en-resource://database/976:1)
没有搭配使用array delete：会发生内存泄漏，但并不是指针数组占用的内存泄漏，而是dtor只被调用了一次，指针数组的未被析构部分**指向的内存**会发生泄漏
本质上：没有指针的类是不会造成这样的内存泄漏

### 扩展

#### 关键字 static

![dd896dfbb527f4f42e398a9f6e78e4e4.png](en-resource://database/1015:1)

static 的对象没有this pointer

![1e779ea96dd62568a8df199368214857.png](en-resource://database/1017:1)

把ctors放在private区

![b24a81e6d094480dc936e23755bca8b5.png](en-resource://database/1019:1)

![bb9cc94cdacc6d9a24b11dc7be93f5a4.png](en-resource://database/1021:1)

### 组合与继承

- Inheritance（继承）
- Composition（复合）
- Delegation（委托）

#### Composition（复合）

Composition（复合），表示has-a
一个复合类型中包含了某一种类型的变量

Composition（复合）关系下的构造和析构

![147b811eece1ed32a8810e58ce99eae0.png](en-resource://database/1027:1)

关于复合：若你有一个外部的对象，你便会有内部的对象，因为你的外部对象的构造函数会在初值列对内部对象进行初始化，二者的生命期机会一致。

#### Delegation（委托）Composition by reference

![663dc280ba2dab6519eb6f7bbd11ab5d.png](en-resource://database/1029:1)

注意：没有Compostion by pointer 的说法

**委托的特点**
- 委托不同于复合其内外部对象的生命不保持同步
- 起到编译防火墙的作用，外部接口不需要编译，只编译内部指向的对象

引用计数、写时复制

#### Inheritance（继承），表示is-a

语法：（黄色）
![5cb215c5e50e3a740380bdb5a6bc068a.png](en-resource://database/1031:1)

Inheritance（继承）关系下的构造和析构

![3af584d027d39a9adb3c7eddabe67125.png](en-resource://database/1033:1)

父类的析构函数必须是virtual

### 虚函数与多态

#### Inheritance（继承）with virtual functions（虚函数）
![27b052902c0887e0af0e1ba549f99b21.png](en-resource://database/1035:1)
模板方法（设计模式）：
![e083613969a6e16a7ac5b3d049a3211e.png](en-resource://database/1037:1)

子类调用父类的函数等同于，子类作为this pointer，被传进了父类调用的该函数中，
CDocument中的serialize（）之所以能找到子类重写的虚函数，就是靠这个this pointer

**Inheritance+composition关系下的构造与析构**

![dd908ee85949cf7c5c2045cda609fe72.png](en-resource://database/1039:1)

![b74834b0ce6ebb470730ca3dad29942e.png](en-resource://database/1041:1)

**Delegation+Inheritance**

**观察者模式Obeserver**：
![1d4396912d06601f02485973970f60bc.png](en-resource://database/1043:1)
vector指针（delegation）指向Observer，
而Observer是可以被继承的，这些子类都可以放到vector这个容器中

**组合模式Composite**：

Primitive：个体
Composite：组合物
![513e7e66becc446afae4c2ca6910fce8.png](en-resource://database/1050:1)

Prototype：没懂