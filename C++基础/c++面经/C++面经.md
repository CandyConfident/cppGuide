# C++面经

## **C 与 C++ 的真正区别在哪里？**

<https://mp.weixin.qq.com/s/HZQrtejkKQDDB4vlG4qRgg> 

> 1、首先C和C++**在基础语句上没有太大区别。**
>
> 2、往上一层，则是**多出的语法，关键字。**姑且可以认为是小特色。
>
> 语法的区别典型的**头文件的不同以及名称空间的声明。**这里会有和C一样的概念就是作用域，但是两者又有不同。还有就是**新增new和delete**的语法。在浩瀚的c代码中，遍地都是传递副本或者传递地址，而c++标新立异，多出了一个变量别名的概念，所以就有了**按引用传递，实际上更深一点，就是指针的封装实现，而这些只不过是编译器做了你浑然不知而已。**一个典型的例子就是**auto和explicit**关键字，它们体现的是c++显式和隐式转换的概念，但你无需关心怎么实现显式和隐式。
>
> 3、C++比C最大的改进之一就是增加了很多类型安全的功能，在编译（或者运行时如dynamic_cast)时避免了指鹿为马事件的发生，程序运行起来更加的安全。 
>
> 3、再往上，就和C相差越来越远了，**重载和虚函数的概念，**可以认为是大特色**。**
>
> 4、再往上，就是完全独立于C的概念，**类，对象和继承。**
>
> 5、再往上， 可以算接近“真正”的含义的区别了，**那就是C++强大的独立特性** ，支持范式编程，如函数模板，模板类，C++还有异常机制，这也是C++的一个特性，还支持元编程，以及强大的STL标准库。
>
> 6、**终极封顶！设计思想和应用场景的区别！**
>
> 有一个很笼统的回答，就是C和C++的本质区别是**面向过程和面向对象**。这种回答看似没毛病，但是一看就知道水平不会有多高，应该是道听途说的“主流”看法，忽悠外行的还可以。用过这两门语言编程的人，不难体会，c可以实现面向过程，亦可实现类似的面向对象比如结构体封装，但用法上没有比真正有面向对象的C++高效和方便，只因为C++多了一个类的管理。而C++完全可以向下兼容C，即可以面向过程，也可以面向对象，我们常说C++是一种半面向对象的语言，但它完全可以面向过程。高级的系统编程，多线程，数据结构等等C++也可以做到，只不过出于执行效率和内存占用考虑，C的优势使它趋向于底层，如内核驱动和操作系统，越精简质量越高。对比C++，它更像是基于系统上的上层语言，可以做大型软件，界面开发，游戏开发等等等等。诚然，《C++ Primer Plus》中也说过**，把C的繁杂的实现过程抽象成类型并且实例化来管理，是C++设计之初的动机，也就是OOP思想**。用户可以自定义类型，并且可以不断往里面添加和拓展，必须修改的时候不需要大改全局，而只需要改局部，这就是OOP的优势之一。两者的侧重点会点不同，**C更注重实现逻辑，C++更注重的是程序的整体设计**，这就是常说的面向过程和面向对象，其本质还是在其设计思想上，C++更加开放和自由，代码维护和管理更加高效。
>
> 

## C++ nullptr

> 解引用：
> nullptr：未定义
> 野指针/悬垂指针：未定义
>
> delete
> nullptr：良好定义，delete什么也不用做
> 野指针/悬垂指针：未定义
>
> 值：
> nullptr：明确
> 野指针/悬垂指针：未定义，无法确定

## 纯虚函数和虚函数

> - 若父类包含纯虚函数,那么他只能作为抽象类,不能实例化对象,只能被继承.
> - 子类必须实现父类的纯虚函数,不然无法实例化对象,编译是没有问题的.
> - 父类含有虚函数,子类继承父类,便继承了父类函数的调用权.子函数可重写父类虚函数,也可不重写.
> - 子类实现父类纯虚函数,虽然可以不写virtual关键字,但其实还是虚函数.

## 多态是怎么实现的？

- 首先多态是借助虚函数和继承实现的
- 父类的指针指向子类的对象，函数调用的地址在是在运行时才确定的。

## 虚函数是怎么实现的？

> - 含有虚函数的类中会有一个vptr,用一张虚函数表（virtual table)存储所有指向虚函数的指 针，并在表头附加上一个该类的type_info对象，在对象中则保存一个指向虚函数表的指指针，如下图所示。
>
> - 虚表的构建：基类的虚表构建，先填上虚析构函数的入口地址，之后所有虚函数的入口地址按在类中声明顺序填入虚表；派生类的虚表构建，先将基类的虚表内容复制到派生类虚表中，如果派生类覆盖了基类的虚函数，则虚表中对应的虚函数入口地址也会被覆盖，为了后面寻址的一致性。
>
> - ![img](.\picture\webp) 
>
>   ![img](.\picture\610439-20151025195611333-359739251.png) 
>

## C++ class 和 struct

> C语言里面struct是一种数据类型，不能定义函数，所以在面向c的过程中，struct不能包含任何函数。否则编译器会报错  
>
> 在C++中struct得到了很大的扩充：
>
> 1.struct可以包括成员函数
>
> 2.struct可以实现继承
>
> 3.struct可以实现多态
>
> 1.默认的继承访问权。class默认的是private,strcut默认的是public。 
>
> 2.默认访问权限：struct作为数据结构的实现体，它默认的数据访问控制是public的，而class作为对象的实现体，它默认的成员变量访问控制是private的。 
>
> 4.class和struct在使用大括号{ }上的区别
>
> - 如果没有定义构造函数，struct可以用大括号初始化。　　
>
> - 如果没有定义构造函数，且所有成员变量全是public的话，class可以用大括号初始化

## 指针与引用的区别

> **从语言的角度来说**
>
> - reference在定义时必须初始化，没有null引用，所以使用引用，可以不做null检测，这么看的话，传递引用比传递指针更高效
>
> - 可以有空指针，指针也可以被重新赋值，引用一旦初始化则无法更改
>
> - 指针传递时值传递，拷贝指针的值，引用传递的是实参本身，而不是拷贝
>
> - ```c++
>   //若要修改指针本身的值，需传递引用
>   #include<iostream>
>   using namespace std;
>   
>   void test(int *&p)
>   {
>   　　int a=1;
>   　　p=&a;
>   　　cout<<p<<" "<<*p<<endl;
>   }
>   
>   int main(void)
>   {
>       int *p=NULL;
>       test(p);
>       if(p!=NULL)
>       cout<<"指针p不为NULL"<<endl;
>       system("pause");
>       return 0;
>   }
>   ```
>
> - "sizeof引用"得到的是所指向的变量(对象)的大小，而"sizeof指针"得到的是指针本身的大小； 
>
> - 指针和引用的自增(++)运算意义不一样；
>
> - **引用是类型安全的，指针不是？**
>
> - **从语言级别上，指针和引用没有关系，引用就是另一个变量的别名。**对引用的任何操作等价于对被引用变量的操作 
>
> **从编译器的角度来说**
>
> -  **C++中引用是编译器通过const 指针实现的**，但这个实现在语言层面对程序员做了透明化处理。 
> - 所以说引用在实现层面还是要分配空间的，不仅仅是别名这么简单。

## C++四种强制类型转换操作符

**static_cast**

- static_cast强制转换只会在编译时检查，但没有运行时类型检查来保证转换的安全性。 

- static_cast也不能去掉expression的const、volitale属性。 

- **能使用隐式转换的地方，均可以使用`static_cast`转换

- 在类层次结构中，上行转换

- 如果类型不兼容，使用`static_cast`编译检查，会报错

- ```C++
      //静态类型转换，编译器会做类型检查,类型不兼容,会报错 
      char *p1  = "hello world";                       
      int  *p2  = static_cast<int *>(p1);   
  ```

**const_cast**

- **编译器在期处理**

- const_cast用于去掉对象的const或者volatile属性。 (将常量对象转换为非常量对象)

- const_cast <new_type> (expression)

- **new_type 必须是一个指针、引用或者指向对象类型成员的指针。**

- 常量指针被转换成非常量指针，并且仍然指向原来的对象；常量引用被转换成非常量引用，并且仍然引用原来的对象。 

  ```c++
  void Func(double& d) { ... }  
  
  void ConstCast()  
  
  {  
  
     const double pi = 3.14;  
  
     Func(const_cast<double&>(pi)); //No error.  
  
  }
  
  ```

**dynamic_cast**

- 有运行时类型检查来保证转换的安全性，主要用于基类和派生类之间的转换。
- 相比static_cast，dynamic_cast会在运行时检查类型转换是否合法，具有一定的安全性。由于运行时的检查，所以会额外消耗一些性能。
- dynamic_cast使用场景与static相似，在类层次结构中使用时，**上行转换和static_cast没有区别**，都是安全的；下行转换时，dynamic_cast会检查转换的类型，相比static_cast更安全。 
- **dynamic_cast只有在基类存在虚函数(虚函数表)的情况下才有可能将基类指针转化为子类。** (无虚函数无法实现多态，即编译时就确定了函数调用地址，RTTI)
- **dynamic_cast转换仅适用于指针或引用。**
- 在转换可能发生的前提下，dynamic_cast会尝试转换，**若指针转换失败，则返回空指针**，若引用转换失败，则抛出异常。

**reinterpret_cast(重新诠释)** 

- 提供较低层次的重新解释
- 比较危险

## 内存泄漏

**动态开辟的空间，在使用完毕后未释放**，结果导致一直占据该内存单元，不能被任何程序再次使用，直到程序结束。即所谓内存泄漏。 注意：内存泄漏是指堆内存的泄漏。 

### 野指针

指未初始化的指针

### 垂悬指针

可以认为也是一种野指针。指针所指向的对象被释放，但是该指针仍旧指向已经回收的内存地址，此情况下该指针便称**悬垂指针** 

## **SIzeOf**



## 绝不在构造函数或析构函数中调用虚函数。 

  简要结论： 

  １.　从语法上讲，调用完全没有问题。 

  ２.　但是从效果上看，往往不能达到需要的目的。 

  Effective 的解释是： 

  派生类对象构造期间进入基类的构造函数时，对象类型变成了基类类型，而不是派生类类型。 

  同样，进入基类析构函数时，对象也是基类类型。 

   所以，虚函数始终仅仅调用基类的虚函数（如果是基类调用虚函数），不能达到多态的效果，所以放在构造函数中是没有意义的，而且往往不能达到本来想要的效果。

## C++中为什么构造函数不能是虚函数，析构函数是虚函数

1. **调用虚函数需要知道该类的虚指针，而虚指针是在构造函数中初始化的，所以相矛盾了。**
2. **就算在构造函数前拿到了虚指针，你调用一个虚拟构造函数，编译器不知道你想构建是继承树上的哪种类型。 构建一个对象，必须知道具体的类型信息 。**




[TOC]

## C++ 常用关键字

### extern关键字

1. extern可以置于变量或者函数前，以标示变量或者函数的定义在别的文件中，提示编译器遇到此变量和函数时在其他模块中寻找其定义。
2. 此外extern也可用来进行链接指定。（即C++与C函数的相互调用时，extern "C"）。

**具体来说：**

1. 当extern与"C"一起连用时，如: extern "C" void fun(int a, int b);则告诉编译器在编译fun这个函数名时按着C的规则去翻译相应的函数名而不是C++的，C++的规则在翻译这个函数名时会把fun这个名字变得面目全非，可能是fun@aBc_int_int#%$也可能是别的，这要看编译器的"脾气"了(不同的编译器采用的方法不一样)，为什么这么做呢，因为C++支持函数的重载啊，在这里不去过多的论述这个问题，如果你有兴趣可以去网上搜索，相信你可以得到满意的解释!   

2. 当extern不与"C"在一起修饰变量或函数时，如在头文件中: extern int g_Int; 它的作用就是声明**函数或全局变量**的关键字。**记住它是一个声明不是定义!**也就是说B模块要引用A模块中定义的全局变量或函数时，它只要包含A模块的头文件即可,在编译阶段，B模块虽然找不到该函数或变量，但它不会报错，它会在连接时从模块A生成的目标代码中找到此函数。 

    

### static关键字

无论修饰局部变量还是全局变量，static都会使其生命周期变为整个程序的生命周期，并且带了默认初始化。

#### static 修饰局部变量

- 一般情况下，对于局部变量是存放在栈区的，并且局部变量的生命周期在该语句块执行结束时便结束了。
- 但是如果用static进行修饰的话，该变量便存放在静态数据区，其生命周期一直持续到整个程序执行结束。
- static修饰局部变量，其生命周期以及存储空间发生了变化，但是其作用域并没有改变，其仍然是一个局部变量，作用域仅限于该语句块。
- 用static修饰局部变量后，该变量只在初次运行时进行初始化工作，且只进行一次。

#### static 修饰全局变量

- 一个全局变量，它既可以在本文件中被访问到，也可以在同一个工程的其它源文件中被访问(只需用extern进行声明即可)。 

  ```c++
  //有file1.cpp  
  int a=1;  
  
  //file2.cpp  
  #include<iostream> 
  using namespace std;
  extern int a;  
  int main(void)  
  {  
  	printf("%d\",a);  	
  	return 0;  
  } 
  ```

- static修饰全局变量a后，上述代码便会编译报错。也就是说static改变了全局变量a的作用域，由原来的整个工程可见变为本源文件可见。 

- static 修饰普通函数，表明函数的作用范围，仅在定义该函数的文件内才能使用。在多人开发项目时，为了防止与他人命名空间里的函数重名，可以将函数定位为 static。

#### static修饰成员变量和成员函数

- 修饰成员变量，修饰成员变量使所有的对象只保存一个该变量，而且不需要生成对象就可以访问该成员。**static成员变量必须类外初始化。初始化的动作伴随着内存分配，而内类只是声明**
- 修饰成员函数，修饰成员函数使得不需要生成对象就可以访问该函数，但是在 static 函数内不能访问非静态成员。

### const 关键字

const关键字我觉得这篇挺全面的，大家可以看看

<https://light-city.club/sc/basic_content/const/> 

这里我主要说下自己对const的一些认识

#### const的含义

- 常类型是指使用类型修饰符**const**说明的类型，常类型的变量或对象的值是不能被更新的。 
- **const常量与#define宏定义常量的区别**：#define宏定义只是简单的字符串替换，不能进行安全检查。 
- `const` 定义的变量只有类型为**整数或枚举**，且以常量表达式初始化时才能作为常量表达式。其他情况下它只是一个 `const` 限定的变量，不要将与常量混淆。 

#### const的应用情景

- 声明变量时，无论是局部、全局、类成员变量、指针类型、引用类型、内置类型、自定义类型，都可以使用const。这里const的作用就是说明这些被修饰者不能被更新了。

- const 修饰函数参数，这个比较常见，目的是防止参数被修改

- 这里需要注意的时const用于函数重载时的一些区别，看下面例子

  ```c++
  //下面编译错误，重定义，不算重载，因为传参是 by value
  void fun(int i) 
  void fun(const int i)  
   
  //下面编译正常，算重载，因为传参是 by reference
  void fun(int& i) 
  void fun(const int& i)    //指向常量的引用
  
  //下面编译正常，算重载，因为传参是 by reference
  void fun(char* a) 			//指向字符串变量
  void fun(const char* a)      //指向字符串常量
  
  //下面编译错误，重定义，不算重载，因为参数指针本身还是copy过来的。
  void fun(char* a) 			
  void fun(char* const a)     //常量指针
  ```

- const用于指针时要注意，

  ```c++
  int* const cp;   //指向int 的const指针
  int const *pc1;  //指向const int 的指针
  const int *pc2;  //指向const int 的指针（后两个声明是等同的）
      从右向左读的记忆方式：
  cp is a const pointer to int. 故pc不能指向别的int，但可以修改其指向的int变量的内容
  pc2 is a pointer to const int. 故*pc2的内容不可以改变，但pc2可以指向别的int变量
  
  且注意：允许把非 const 对象的地址赋给指向 const 对象的指针,不允许把一个 const 对象的地址赋给一个普通的、非 const 对象的指针。
  
  ```

- **const修饰成员函数，编译器不允许其修改类的数据成员。** 

  在C++中，为了防止类的数据成员被非法访问，将类的成员函数分成了两类，一类是常量成员函数（也被称为观察着）；另一类是非常量成员函数（也被成为变异者）。在一个函数的签名后面加上关键字const后该函数就成了常量函数。对于常量函数，最关键的不同是编译器不允许其修改类的数据成员。 

- const成员变量

  ```c++
  // "static_test.h"
  class static_test {
  public:
  
      static int m ;
      const int n ;
      static_test(int i):n(i){
  
      }
  
  };
  int static_test::m = 10;
  
  //main
  static_test s_t(200);
  
  //const常量要用初始化列表进行初始化，因为在构造函数内部不能叫初始化，而是赋值，对const来说是错误的
  ```

  我们除了上述的初始化const常量用初始化列表方式外，也可以通过下面方法：

  第一步：将常量定义与static结合，也就是：

  ```c++
  static const int n
  ```

  第二步：在外面初始化：

  ```c++
  const int static_test::n=10;
  ```

  当然，如果你使用c++11进行编译，直接可以在定义出初始化，可以直接写成：

  ```c++
  static const int n=10;
  或者
  const int n=10;
  ```

  这两种都在c++11中支持！

  编译的时候加上`-std=c++11`即可！

### inline 关键字

#### inline的意义

- inline函数在调用时编译器会将inline函数粘贴到调用点处 ，**省去了函数查找和调用的开销。**

 举个栗子 

```c++
int f(int a, int b){
    return a + b;
}

int main(){
    int x = 3, y = 4;
    int z = f(x, y);
}
```

  main函数里面的f(x, y)其实就是等价于x + y，所以能够直接替换成 

```c++
int f(int a, int b){
    return a + b;
}

int main(){
    int x = 3, y = 4;
    int z = x + y;
}
```



 **这一点功能上类似于宏展开，但是比宏展开好的地方是，inline发生在编译阶段，会做类型检查，消除了宏展开可能带来的语义隐患。例如定义宏#define f(x, y) (x*y)就会在 f(x+1,y)的时候f(x,y)就变成了x+1*y，完全错误。用inline可以达到相同的意图，却不会产生错误。**

**宏展开是在预编译阶段，宏这个东西，太麻烦了，不碰为妙。**

#### 内联函数使用原则

- 频繁调用的简小函数可以作为内联函数
  - 所谓简小是指：函数的执行时间小于或者和函数调用时间差不多
  - 内联函数仅仅省去了函数调用的开销，从而提高函数的执行效率。如果执行函数体内代码的时间，相比于函数调用的开销较大，那么效率的收获会很少。
  - 以下情况不适宜内联：
    - 代码中包含循环语句（内联收益不大）
    - 代码中包含递归函数   
    - 函数体代码很长（消耗内存比较大）
- 另一方面，内联是以代码膨胀（复制）为代价。若函数体很大，在多个函数调用的地方展开函数体，会造成代码体积的急剧膨胀（使程序的总代码量增大），消耗更多的内存空间。

#### 内联函数的声明与定义

- 在类内定义的函数，除了虚函数的其他函数都会自动隐式地当成内联函数。 
- 在内类声明的函数，要想成为内联函数，必须在类外定义处加inline关键字 。
- inline要与函数定义放在一起,inline是一种“用于实现的关键字,而不是用于声明的关键字” 

下面这一部分引用自  [huihut大佬的博客](https://interview.huihut.com/#/?id=inline-%e5%86%85%e8%81%94%e5%87%bd%e6%95%b0) 

> #### [编译器对 inline 函数的处理步骤](https://interview.huihut.com/#/?id=%e7%bc%96%e8%af%91%e5%99%a8%e5%af%b9-inline-%e5%87%bd%e6%95%b0%e7%9a%84%e5%a4%84%e7%90%86%e6%ad%a5%e9%aa%a4)
>
> 1. 将 inline 函数体复制到 inline 函数调用点处；
> 2. 为所用 inline 函数中的局部变量分配内存空间；
> 3. 将 inline 函数的的输入参数和返回值映射到调用方法的局部变量空间中；
> 4. 如果 inline 函数有多个返回点，将其转变为 inline 函数代码块末尾的分支（使用 GOTO）。
>
> #### [优缺点](https://interview.huihut.com/#/?id=%e4%bc%98%e7%bc%ba%e7%82%b9)
>
> 优点
>
> 1. 内联函数同宏函数一样将在被调用处进行代码展开，省去了参数压栈、栈帧开辟与回收，结果返回等，从而提高程序运行速度。
> 2. 内联函数相比宏函数来说，在代码展开时，会做安全检查或自动类型转换（同普通函数），而宏定义则不会。
> 3. 在类中声明同时定义的成员函数，自动转化为内联函数，因此内联函数可以访问类的成员变量，宏定义则不能。
> 4. 内联函数在运行时可调试，而宏定义不可以。
>
> 缺点
>
> 1. 代码膨胀。内联是以代码膨胀（复制）为代价，消除函数调用带来的开销。如果执行函数体内代码的时间，相比于函数调用的开销较大，那么效率的收获会很少。另一方面，每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存空间。
> 2. inline 函数无法随着函数库升级而升级。inline函数的改变需要重新编译，不像 non-inline 可以直接链接。
> 3. **是否内联，程序员不可控。内联函数只是对编译器的建议，是否对函数内联，决定权在于编译器。**
>
> #### [虚函数（virtual）可以是内联函数（inline）吗？](https://interview.huihut.com/#/?id=%e8%99%9a%e5%87%bd%e6%95%b0%ef%bc%88virtual%ef%bc%89%e5%8f%af%e4%bb%a5%e6%98%af%e5%86%85%e8%81%94%e5%87%bd%e6%95%b0%ef%bc%88inline%ef%bc%89%e5%90%97%ef%bc%9f)
>
> > [Are "inline virtual" member functions ever actually "inlined"?](http://www.cs.technion.ac.il/users/yechiel/c++-faq/inline-virtuals.html)
>
> - 虚函数可以是内联函数，内联是可以修饰虚函数的，但是当虚函数表现多态性的时候不能内联。
> - 内联是在编译器建议编译器内联，而虚函数的多态性在运行期，编译器无法知道运行期调用哪个代码，因此虚函数表现为多态性时（运行期）不可以内联。
> - `inline virtual` 唯一可以内联的时候是：编译器知道所调用的对象是哪个类（如 `Base::who()`），这只有在编译器具有实际对象而不是对象的指针或引用时才会发生。
>
> 虚函数内联使用
>
> ```c++
> #include <iostream>  
> using namespace std;
> class Base
> {
> public:
>     inline virtual void who()
>     {
>         cout << "I am Base\n";
>     }
>     virtual ~Base() {}
> };
> class Derived : public Base
> {
> public:
>     inline void who()  // 不写inline时隐式内联
>     {
>         cout << "I am Derived\n";
>     }
> };
> 
> int main()
> {
>     // 此处的虚函数 who()，是通过类（Base）的具体对象（b）来调用的，编译期间就能确定了，所以它可以是内联的，但最终是否内联取决于编译器。 
>     Base b;
>     b.who();
> 
>     // 此处的虚函数是通过指针调用的，呈现多态性，需要在运行时期间才能确定，所以不能为内联。  
>     Base *ptr = new Derived();
>     ptr->who();
> 
>     // 因为Base有虚析构函数（virtual ~Base() {}），所以 delete 时，会先调用派生类（Derived）析构函数，再调用基类（Base）析构函数，防止内存泄漏。
>     delete ptr;
>     ptr = nullptr;
> 
>     system("pause");
>     return 0;
> } 
> ```



**其实我觉得内联虚函数是没有啥必要的，因为虚函数的威力就是多态，不用于多态的虚函数时没有灵魂的虚函数，不过大家知道虚函数也可以内联就行了**

 

### auto 关键字

- C++11新特性，用于自动类型推断。

- auto主要用于比较复杂的类型

- auto变量必须在声明的同时被初始化

  ```c++
  C++98中：
  std::vector<double> scores;
  std::vector<double> iterator pv = scores.begin();
  C++11中：
  std::vector<double> scores;
  auto pv = scores.begin(); // 自动判断，简化代码
  
  ```



### mutable关键字

  主要用于C++中：该关键字跟constant（既C++中的const）是反义词，用来指出即使结构体或者类为const类型，其成员只要被mutable修饰，值仍然可以被修改。该关键字只用在类中或者结构体中，用来修饰单个变量是不被允许的。 

![1](C:/Users/mycan/Documents/CppGuild/cpp_keyword/picture/1.jpg)



### volatile关键字

  主要用于C语言，一个定义为volatile的变量是说这变量可能会被意想不到地改变，这样，编译器就不会去假设这个变量的值了。精确地说就是，优化器在用到这个变量时必须每次都小心地重新读取这个变量的值，而不是使用保存在寄存器里的备份。例如：

```c++
volatile int i=10;

int j = i;

... 

int k = i;

```

  如果没有 volatile关键字，由于编译器发现两次从i读数据的代码之间的代码没有对i进行过操作，它会自动把上次读的数据放在k中。而不是重新从i里面读；而加了volatile后，每次都会重新读取i的值。 

下面是volatile变量的几个常用方式：

- 并行设备的硬件寄存器（如：状态寄存器）
- 一个中断服务子程序中会访问到的非自动变量(Non-automatic variables)
- **多线程应用中被几个任务共享的变量**

> 一个参数既可以是const还可以是 volatile。例如：一个例子是只读的状态寄存器。它是volatile因为它可能被意想不到地改变。它是const因为程序不应该试图去修改它
>
> 一个指针可以是volatile。一个例子是当一个中断服务子程序修改一个指向一个buffer的指针时。



# C++2.0新特性

## Variable template

## nullptr

## auto

## decltype

auto 和 decltype都可以进行自动类型推导，

区别：

- auto 用于初始化时的类型推导，总是“值类型” 
- decltype 能够推导出表达式的精确类型 
- auto 顶层*const*会被忽略，底层*const*会被保留 
- 如果*decltype*使用表达式的结果类型可以作为一条赋值语句的**左值**，那么*decltype*返回一个引用类型
- 如果表达式类型本身就是一个引用类型，那么*decltype*返回对应类型的引用类型。
- decltype与auto关键字一样，用于进行编译时类型推导
- decltype的类型推导并不是像auto一样是从变量声明的初始化表达式获得变量的类型，而是总是**以一个普通表达式作为参数**，返回该表达式的类型,而且decltype并不会对表达式进行求值。 

## smart_ptr

**在智能指针出现以前，我们通常使用 new 和 delete 来管理动态分配的内存，但这种方式存在几个常见的问题：**

- **忘记 delete 内存：**会导致内存泄漏问题，且除非是内存耗尽否则很难检测到这种错误。
- **使用已经释放掉的对象：**如果能够记得在释放掉内存后将指针置空并在下次使用前判空，尚可避免这种错误。
- **同一块内存释放两次：**如果有两个指针指向相同的动态分配对象，则很容易发生这种错误。
- **发生异常时的内存泄漏：**若在 new 和 delete 之间发生异常，则会导致内存泄漏。

### 智能指针的思想

- **将基本类型指针封装为类对象指针（这个类肯定是个模板，以适应不同基本类型的需求），这样在对象过期时，让他的析构函数删除指向的内存（调用delete)**
- RAII ，它是 "Resource Acquisition Is Initialization" 的首字母缩写 。
- RAII的本质内容是用对象代表资源，把管理资源的任务转化为管理对象的任务，将资源的获取和释放与对象的构造和析构对应起来，从而确保在对象的生存期内资源始终有效，对象销毁时资源必被释放。 
- C++11后的智能指针  shared_ptr , unique_ptr 和 weak_ptr 

**使用注意点**

- **所有的智能指针类都有一个explicit构造函数，以指针作为参数。比如auto_ptr的类模板原型为：**

   

  ```c++
  templet<class X>
  class auto_ptr {
    explicit auto_ptr(X* p = 0) ; 
    ...
  };
  ```

  **因此不能自动将指针转换为智能指针对象，必须显式调用：**

  ```c++
  shared_ptr<double> pd; 
  double *p_reg = new double;
  pd = p_reg;                               // not allowed (implicit conversion)
  pd = shared_ptr<double>(p_reg);           // allowed (explicit conversion)
  shared_ptr<double> pshared = p_reg;       // not allowed (implicit conversion)
  shared_ptr<double> pshared(p_reg);        // allowed (explicit conversion)
  ```

   

- 对全部三种智能指针都应避免的一点：

   

  ```c++
  string vacation("I wandered lonely as a cloud.");
  shared_ptr<string> pvac(&vacation);   // No
  ```

  pvac过期时，程序将把delete运算符用于非堆内存，这是错误的。

### 示例

```c++
#include <iostream>
#include <string>
#include <memory>

class report
{
private:
    std::string str;
public:
    report(const std::string s) : str(s) {
        std::cout << "Object created.\n";
    }
    ~report() {
        std::cout << "Object deleted.\n";
    }
    void comment() const {
        std::cout << str << "\n";
    }
};

int main() {
    {
        std::auto_ptr<report> ps(new report("using auto ptr"));
        ps->comment();
    }

    {
        std::shared_ptr<report> ps(new report("using shared ptr"));
        ps->comment();
    }

    {
        std::unique_ptr<report> ps(new report("using unique ptr"));
        ps->comment();
    }
    return 0;
}
```

```c++
//output
Object created.
using auto ptr
Object deleted.
Object created.
using shared ptr
Object deleted.
Object created.
using unique ptr
Object deleted.
```

### auto_ptr/unique_ptr

C++98提供的解决方案，C++11已将其摒弃

#### 3. 为什么摒弃auto_ptr？

先来看下面的赋值语句:

```
auto_ptr< string> ps (new string ("I reigned lonely as a cloud.”）;
auto_ptr<string> vocation; 
vocaticn = ps;
```

上述赋值语句将完成什么工作呢？如果ps和vocation是常规指针，则两个指针将指向同一个string对象。这是不能接受的，因为程序将试图删除同一个对象两次——一次是ps过期时，另一次是vocation过期时。要避免这种问题，方法有多种：

- 定义陚值运算符，使之执行深复制。这样两个指针将指向不同的对象，其中的一个对象是另一个对象的副本，缺点是浪费空间，所以智能指针都未采用此方案。
- 建立所有权（ownership）概念。对于特定的对象，只能有一个智能指针可拥有，这样只有拥有对象的智能指针的构造函数会删除该对象。然后让赋值操作**转让所有权**。这就是用于auto_ptr和uniqiie_ptr 的策略，但unique_ptr的策略更严格。
- 创建智能更高的指针，跟踪引用特定对象的智能指针数。这称为**引用计数**。例如，赋值时，计数将加1，而指针过期时，计数将减1,。当减为0时才调用delete。这是shared_ptr采用的策略。

当然，同样的策略也适用于复制构造函数。
每种方法都有其用途，但为何说要摒弃auto_ptr呢？
下面举个例子来说明。

```c++
#include <iostream>
#include <string>
#include <memory>
using namespace std;

int main() {
  auto_ptr<string> films[5] =
 {
  auto_ptr<string> (new string("Fowl Balls")),
  auto_ptr<string> (new string("Duck Walks")),
  auto_ptr<string> (new string("Chicken Runs")),
  auto_ptr<string> (new string("Turkey Errors")),
  auto_ptr<string> (new string("Goose Eggs"))
 };
 auto_ptr<string> pwin;
 pwin = films[2]; // films[2] loses ownership. 将所有权从films[2]转让给pwin，此时films[2]不再引用该字符串从而变成空指针

 cout << "The nominees for best avian baseballl film are\n";
 for(int i = 0; i < 5; ++i)
  cout << *films[i] << endl;
 cout << "The winner is " << *pwin << endl;
 cin.get();

 return 0;
}
```

运行下发现程序崩溃了，原因在上面注释已经说的很清楚，films[2]已经是空指针了，下面输出访问空指针当然会崩溃了。但这里如果把auto_ptr换成shared_ptr或unique_ptr后，程序就不会崩溃，原因如下：

- 使用shared_ptr时运行正常，因为shared_ptr采用引用计数，pwin和films[2]都指向同一块内存，在释放空间时因为事先要判断引用计数值的大小因此不会出现多次删除一个对象的错误。

- 使用unique_ptr时编译出错，与auto_ptr一样，unique_ptr也采用所有权模型，但在使用unique_ptr时，程序不会等到运行阶段崩溃，而在编译器因下述代码行出现错误：

   

  ```
  unique_ptr<string> pwin;
  pwin = films[2]; // films[2] loses ownership.
  ```

  指导你发现潜在的内存错误。

这就是为何要摒弃auto_ptr的原因，一句话总结就是：**避免潜在的内存崩溃问题。**



#### 4. unique_ptr为何优于auto_ptr？

可能大家认为前面的例子已经说明了unique_ptr为何优于auto_ptr，也就是安全问题，下面再叙述的清晰一点。
请看下面的语句:

```c++
auto_ptr<string> p1(new string ("auto") ； //#1
auto_ptr<string> p2;                       //#2
p2 = p1;                                   //#3
```

在语句#3中，p2接管string对象的所有权后，p1的所有权将被剥夺。前面说过，这是好事，可防止p1和p2的析构函数试图刪同—个对象；

但如果程序随后试图使用p1，这将是件坏事，因为p1不再指向有效的数据。

下面来看使用unique_ptr的情况：

```c++
unique_ptr<string> p3 (new string ("auto");   //#4
unique_ptr<string> p4；                       //#5
p4 = p3;                                      //#6
```

编译器认为语句#6非法，避免了p3不再指向有效数据的问题。因此，unique_ptr比auto_ptr更安全。

**但unique_ptr还有更聪明的地方。**
有时候，会将一个智能指针赋给另一个并不会留下危险的悬挂指针。假设有如下函数定义：

```c++
unique_ptr<string> demo(const char * s)
{
    unique_ptr<string> temp (new string (s))； 
    return temp；
}
```

并假设编写了如下代码：

```
unique_ptr<string> ps;
ps = demo('Uniquely special")；
```

demo()返回一个临时unique_ptr，然后ps接管了原本归返回的unique_ptr所有的对象，而返回时临时的 unique_ptr 被销毁，也就是说没有机会使用 unique_ptr 来访问无效的数据，换句话来说，这种赋值是不会出现任何问题的，即没有理由禁止这种赋值。实际上，编译器确实允许这种赋值，这正是unique_ptr更聪明的地方。

**总之，党程序试图将一个 unique_ptr 赋值给另一个时，如果源 unique_ptr 是个临时右值，编译器允许这么做；如果源 unique_ptr 将存在一段时间，编译器将禁止这么做**，比如：

```c++
unique_ptr<string> pu1(new string ("hello world"));
unique_ptr<string> pu2;
pu2 = pu1;                                      // #1 not allowed
unique_ptr<string> pu3;
pu3 = unique_ptr<string>(new string ("You"));   // #2 allowed
```

其中#1留下悬挂的unique_ptr(pu1)，这可能导致危害。而#2不会留下悬挂的unique_ptr，因为它调用 unique_ptr 的构造函数，该构造函数创建的临时对象在其所有权让给 pu3 后就会被销毁。**这种随情况而已的行为表明，unique_ptr 优于允许两种赋值的auto_ptr 。**

当然，您可能确实想执行类似于#1的操作，仅当以非智能的方式使用摒弃的智能指针时（如解除引用时），这种赋值才不安全。要安全的重用这种指针，可给它赋新值。C++有一个标准库函数std::move()，让你能够将一个unique_ptr赋给另一个。下面是一个使用前述demo()函数的例子，该函数返回一个unique_ptr<string>对象：
使用move后，原来的指针仍转让所有权变成空指针，可以对其重新赋值。

```c++
unique_ptr<string> ps1, ps2;
ps1 = demo("hello");
ps2 = move(ps1);
ps1 = demo("alexia");
cout << *ps2 << *ps1 << endl;
```

#### 5. 如何选择智能指针？

在掌握了这几种智能指针后，大家可能会想另一个问题：在实际应用中，应使用哪种智能指针呢？
下面给出几个使用指南。

（1）如果程序要使用多个指向同一个对象的指针，应选择shared_ptr。这样的情况包括：

- 有一个指针数组，并使用一些辅助指针来标示特定的元素，如最大的元素和最小的元素；
- 两个对象包含都指向第三个对象的指针；
- STL容器包含指针。很多STL算法都支持复制和赋值操作，这些操作可用于shared_ptr，但不能用于unique_ptr（编译器发出warning）和auto_ptr（行为不确定）。如果你的编译器没有提供shared_ptr，可使用Boost库提供的shared_ptr。

（2）如果程序不需要多个指向同一个对象的指针，则可使用unique_ptr。如果函数使用new分配内存，并返还指向该内存的指针，将其返回类型声明为unique_ptr是不错的选择。这样，所有权转让给接受返回值的unique_ptr，而该智能指针将负责调用delete。可将unique_ptr存储到STL容器在那个，只要不调用将一个unique_ptr复制或赋给另一个算法（如sort()）。例如，可在程序中使用类似于下面的代码段。



```c++
unique_ptr<int> make_int(int n)
{
    return unique_ptr<int>(new int(n));
}
void show(unique_ptr<int> &p1)
{
    cout << *a << ' ';
}
int main()
{
    ...
    vector<unique_ptr<int> > vp(size);
    for(int i = 0; i < vp.size(); i++)
        vp[i] = make_int(rand() % 1000);              // copy temporary unique_ptr
    vp.push_back(make_int(rand() % 1000));     // ok because arg is temporary
    for_each(vp.begin(), vp.end(), show);           // use for_each()
    ...
}
```

其中push_back调用没有问题，因为它返回一个临时unique_ptr，该unique_ptr被赋给vp中的一个unique_ptr。另外，如果按值而不是按引用给show()传递对象，for_each()将非法，因为这将导致使用一个来自vp的非临时unique_ptr初始化pi，而这是不允许的。前面说过，编译器将发现错误使用unique_ptr的企图。

在unique_ptr为右值时，可将其赋给shared_ptr，这与将一个unique_ptr赋给一个需要满足的条件相同。与前面一样，在下面的代码中，make_int()的返回类型为unique_ptr<int>：

```c++
unique_ptr<int> pup(make_int(rand() % 1000));   // ok
shared_ptr<int> spp(pup);                       // not allowed, pup as lvalue
shared_ptr<int> spr(make_int(rand() % 1000));   // ok
```

模板shared_ptr包含一个显式构造函数，可用于将右值unique_ptr转换为shared_ptr。shared_ptr将接管原来归unique_ptr所有的对象。

在满足unique_ptr要求的条件时，也可使用auto_ptr，但unique_ptr是更好的选择。如果你的编译器没有unique_ptr，可考虑使用Boost库提供的scoped_ptr，它与unique_ptr类似。

6.unique_ptr vs auto_ptr

**unique_ptr优于auto_ptr的地方：**

**①：不允许将一个非临时unique_ptr对象拷贝或复制给另一个unique_ptr，比auto_ptr更安全**

**②：允许将一个临时unique_ptr对象拷贝或复制给另一个unique_ptr，安全之余更聪明**



### shared_ptr

**如果程序要使用多个指向同一个对象的指针，应选择shared_ptr。**

```c++
// 某个时刻只能有一个 unique_ptr 指向一个对象
// 所以，unique_ptr 不支持拷贝，也不支持赋值
// std::unique_ptr<Person> p5(p4); // 错误，不支持拷贝
// p5 = p4; // 错误，不支持赋值
```

shared_ptr的目标是在其所指的对象在不被需要之后（而非之前），自动释放与对象相关的资源。

使用make_shared

shared+ptr初始化时不能使用赋值操纵，不能隐式转换，

直接调用初始化，或者使用初始化列表

#### 2.1 shared_ptr的使用

shared_ptr多个指针指向相同的对象。shared_ptr使用引用计数，每一个shared_ptr的拷贝都指向相同的内存。每使用他一次，内部的引用计数加1，每析构一次，内部的引用计数减1，减为0时，自动删除所指向的堆内存。**shared_ptr内部的引用计数是线程安全的，但是对象的读取需要加锁。**

- 初始化。智能指针是个模板类，可以指定类型，传入指针通过构造函数初始化。也可以使用make_shared函数初始化。不能将指针直接赋值给一个智能指针，一个是类，一个是指针。例如std::shared_ptr<int> p4 = new int(1);的写法是错误的
- 拷贝和赋值。拷贝使得对象的引用计数增加1，赋值使得原对象引用计数减1，当计数为0时，自动释放内存。后来指向的对象引用计数加1，指向后来的对象。
- get函数获取原始指针
- 注意不要用一个原始指针初始化多个shared_ptr，否则会造成二次释放同一内存
- 注意避免循环引用，shared_ptr的一个最大的陷阱是循环引用，循环，循环引用会导致堆内存无法正确释放，导致内存泄漏。循环引用在weak_ptr中介绍。

```c++
#include <iostream>
#include <memory>

int main() {
    {
        int a = 10;
        std::shared_ptr<int> ptra = std::make_shared<int>(a);
        std::shared_ptr<int> ptra2(ptra); //copy
        std::cout << ptra.use_count() << std::endl;

        int b = 20;
        int *pb = &a;
        //std::shared_ptr<int> ptrb = pb;  //error
        std::shared_ptr<int> ptrb = std::make_shared<int>(b);
        ptra2 = ptrb; //assign
        pb = ptrb.get(); //获取原始指针

        std::cout << ptra.use_count() << std::endl;
        std::cout << ptrb.use_count() << std::endl;
    }
}
```

#### 2.2 shared_ptr循环引用问题

```c++
#include <memory>
#include <iostream>
using namespace  std;

class B;
class A
{
public:
    std::shared_ptr<B> m_b;
    A(){
        cout<<"A constructed"<<endl;
    }
    ~A(){
        cout<<"A destructed"<<endl;
    }
};

class B
{
public:
    std::shared_ptr<A> m_a;
    B(){
        cout<<"B constructed"<<endl;
    }
    ~B(){
        cout<<"B destructed"<<endl;
    }
};

int main()
{

    {
        std::shared_ptr<A> a(new A); // new出来的A的引用计数此时为1
        std::shared_ptr<B> b(new B); // new出来的B的引用计数此时为1
        a->m_b = b; // B的引用计数增加为2
        b->m_a = a; // A的引用计数增加为2
        cout<<a.use_count()<<endl;
        cout<<b.use_count()<<endl;
    }
    // b先出作用域，B的引用计数减少为1，不为0，所以堆上的B空间没有被释放，
    // 且B持有的A也没有机会被析构，A的引用计数也完全没减少
    // a后出作用域，同理A的引用计数减少为1，不为0，所以堆上A的空间也没有被释放
}
```

```c++
//output
A constructed
B constructed
2
2
//没有调用A和B的析构函数，内存泄露
```

```
#include <memory>
#include <iostream>
using namespace  std;

class B;
class A
{
public:
	
	//使用weak_ptr
    std::weak_ptr<B> m_b;
    A(){
        cout<<"A constructed"<<endl;
    }
    ~A(){
        cout<<"A destructed"<<endl;
    }
};

class B
{
public:
	//使用weak_ptr,也可只一处使用weak_ptr，
    std::weak_ptr<A> m_a;
    B(){
        cout<<"B constructed"<<endl;
    }
    ~B(){
        cout<<"B destructed"<<endl;
    }
};
int main{
    //同上
}
```

```c++
//output
A constructed
B constructed
2
1
B destructed
A destructed
```

#### 2.3 weak_ptr的使用

**只引用，不计数。**

- weak_ptr是为了配合shared_ptr而引入的一种智能指针，因为它不具有普通指针的行为，没有重载operator*和->,它的最大作用在于协助shared_ptr工作，像旁观者那样观测资源的使用情况。weak_ptr可以从一个shared_ptr或者另一个weak_ptr对象构造，获得资源的观测权。
- **但weak_ptr没有共享资源，它的构造不会引起指针引用计数的增加。**
- 使用weak_ptr的成员函数use_count()可以观测资源的引用计数，另一个成员函数expired()的功能等价于use_count()==0,但更快，表示被观测的资源(也就是shared_ptr的管理的资源)已经不复存在。
- weak_ptr可以使用一个非常重要的成员函数lock()从被观测的shared_ptr获得一个可用的shared_ptr对象， 从而操作资源。但当expired()==true的时候，lock()函数将返回一个存储空指针的shared_ptr。

```c++
#include <iostream>
#include <memory>

int main() {
    {
        std::shared_ptr<int> sh_ptr = std::make_shared<int>(10);
        std::cout << sh_ptr.use_count() << std::endl;

        std::weak_ptr<int> wp(sh_ptr);
        std::cout << wp.use_count() << std::endl;

        if(!wp.expired()){
            std::shared_ptr<int> sh_ptr2 = wp.lock(); //get another shared_ptr

            std::cout << wp.use_count() << std::endl;
        }
    }
    //delete memory
}
//output
1
1
2
```

### 优先用std::make_unique和std::make_shared而不是直接new

先做一下介绍，`std::make_shared`是在C++11中增加的，但`std::make_unique`却是在C++14中增加的。如果你想在C++11中就用上`std::make_unique`，自己写一个简单版的也不难：

```c++
template <typename T, typename... Ts>
std::unique_ptr<T> make_unique(Ts&&... params) {
    return std::unique_ptr<T>(new T(std::forward<Ts>(params)...));
}
```

这个版本不支持数组，不支持自定义的销毁器，但这些都不重要，它足够用了。但要记住的是，不要把它放到`namespace std`下面。

这两个make函数的功能就不解释了，和它们类似的还有一个`std::allocate_shared`。

```c++
auto upw1(std::make_unique<Widget>());
std::unique_ptr<Widget> upw2(new Widget);

auto spw1(std::make_shared<Widget>());
std::shared_ptr<Widget> spw2(new Widget);
```

上面这个例子说明了用make函数的第一个好处：**不需要重复写一遍类型。所有程序员都知道：不要重复代码。代码越少，bug越少。**

***第二个好处：异常安全性。想象我们有两个函数：***

```c++
void processWidget(std::shared_ptr<Widget> spw, int priority);
int computePriority();
```

调用代码很可能长成这个样子：

```c++
processWidget(std::shared_ptr<Widget>(new Widget), computePriority()); // potential resource leak!
```

上面这行代码有内存泄漏的风险，为什么？根据C++标准，在`processWidget`的参数求值过程中，我们只能确定下面几点：

- `new Widget`一定会执行，即一定会有一个`Widget`对象在堆上被创建。
- `std::shared_ptr<Widget>`的构造函数一定会执行。
- `computePriority`一定会执行。

`new Widget`的结果是`std::shared_ptr<Widget>`构造函数的参数，因此前者一定早于后者执行。除此之外，编译器不保证其它操作的顺序，即有可能执行顺序为：

1. `new Widget`
2. 执行`computePriority`
3. 构造`std::shared_ptr<Widget>`

如果第2步抛异常，第1步创建的对象还没有被`std::shared_ptr<Widget>`管理，就会发生内存泄漏。

如果这里我们用`std::make_shared`，就能保证`new Widget`和`std::shared_ptr<Widget>`是一起完成的，中间不会有其它操作插进来，即不会有不受智能指针保护的裸指针出现：

```c++
processWidget(std::make_shared<Widget>(), computePriority()); // no potential resource leak
```

**第三个好处：更高效。**

```c++
std:shared_ptr<Widget> spw(new Widget);
```

这行代码中，我们以为只有一次内存分配，实际发生了两次，第二次是在分配`std::shared_ptr`控制块。如果用`std::make_shared`，它会把`Widget`对象和控制块合并为一次内存分配。

但是make函数也有一些缺点。

第一个缺点：无法传入自定义的销毁器。

第二个缺点：make函数初始化时使用了括号初始化，而不是花括号初始化，比如`std::make_unique<std::vector<int>>(10, 20)`创建了一个有着20个值为10的元素的`vector`，而不是创建了`{10, 20}`这么两个元素的`vector`

第三个缺点：对象和控制块分配在一块内存上，减少了内存分配的次数，但也导致对象和控制块占用的内存也要一次回收掉。即，如果还有`std::weak_ptr`存在，控制块就要在，对象占用的内存也没办法回收。如果对象比较大，且`std::weak_ptr`在对象析构后还可能长期存在，那么这种开销是不可忽视的。

如果我们因为前面这三个缺点而不能使用`std::make_shared`，那么我们要保证，智能指针的构造一定要单独一个语句。回到之前`processWidget`的例子中，假设我们有个自定义的销毁器`void cusDel(Widget* ptr);`，因此不能使用`std::make_shared`，那么我们要这么写来保证异常安全性：

```c++
std::shared_ptr<Widget> spw(new Widget, cusDel);
processWidget(spw, computePriority());
```

但这么写还不够高效，这里我们明确知道`spw`就是给`processWidget`用的，那么可以使用`std::move`，将其转为右值，来避免对引用计数的修改：

```c++
std::shared_ptr<Widget> spw(new Widget, cusDel);
processWidget(std::move(spw), computePriority());
```

### 多线程安全

本章所说的线程安全有两种情况：

#### 多个线程操作多个不同的shared_ptr对象

C++11中声明了shared_ptr的计数操作具有原子性，不管是赋值导致计数增加还是释放导致计数减少，都是原子性的，这个可以参考sp_counted_base的源码，因此，基于这个特性，假如有多个shared_ptr共同管理一个裸指针，那么多个线程分别通过不同的shared_ptr进行操作是线程安全的。

#### 多个线程操作同一个shared_ptr对象

同样的道理，既然C++11只负责sp_counted_base的原子性，那么shared_ptr本身就没有保证线程安全了，加入两个线程同时访问同一个shared_ptr对象，一个进行释放（reset），另一个读取裸指针的值，那么最后的结果就不确定了，很有可能发生野指针访问crash。



## 右值引用与转移语义

### 新特性的目的

右值引用 (Rvalue Referene) 是 C++ 新标准 (C++11, 11 代表 2011 年 ) 中引入的新特性 , 它实现了转移语义 (Move Sementics) 和精确传递 (Perfect Forwarding)。它的主要目的有两个方面：

1. 消除两个对象交互时不必要的对象拷贝，节省运算存储资源，提高效率。
2. 能够更简洁明确地定义泛型函数。

### 左值与右值的定义

C++( 包括 C) 中所有的表达式和变量要么是左值，要么是右值。通俗的左值的定义就是非临时对象，那些可以在多条语句中使用的对象。所有的变量都满足这个定义，在多条代码中都可以使用，都是左值。右值是指临时的对象，它们只在当前的语句中有效。请看下列示例 :

1. 简单的赋值语句`如：int i = 0;` 在这条语句中，i 是左值，0 是临时值，就是右值。在下面的代码中，i 可以被引用，0 就不可以了。立即数都是右值。 

2. 右值也可以出现在赋值表达式的左边，但是不能作为赋值的对象，因为右值只在当前语句有效，赋值没有意义。如：`((i>0) ? i : j) = 1;`在这个例子中，0 作为右值出现在了”=”的左边。但是赋值对象是 i 或者 j，都是左值。

3. 在 C++11 之前，右值是不能被引用的，最大限度就是用常量引用绑定一个右值，如 :

   `const int &a = 1;`

   在这种情况下，右值不能被修改的。但是实际上右值是可以被修改的，如 :

   `T().set().get();`

   T 是一个类，set 是一个函数为 T 中的一个变量赋值，get 用来取出这个变量的值。在这句中，T() 生成一个临时对象，就是右值，set() 修改了变量的值，也就修改了这个右值。

   既然右值可以被修改，那么就可以实现右值引用。右值引用能够方便地解决实际工程中的问题，实现非常有吸引力的解决方案。

### 左值和右值的语法符号

左值的声明符号为”&”， 为了和左值区分，右值的声明符号为”&&”。

```c++
void process_value(int& i) { 
 std::cout << "LValue processed: " << i << std::endl; 
} 
 
void process_value(int&& i) { 
 std::cout << "RValue processed: " << i << std::endl; 
} 
 
int main() { 
 int a = 0; 
 process_value(a); 
 process_value(1); 
}

//output
//LValue processed: 0 
//RValue processed: 1
```

Process_value 函数被重载，分别接受左值和右值。由输出结果可以看出，临时对象是作为右值处理的。

但是如果临时对象通过一个接受右值的函数传递给另一个函数时，就会变成左值，因为这个临时对象在传递过程中，变成了命名对象。

```c++
void process_value(int& i) { 
 std::cout << "LValue processed: " << i << std::endl; 
} 
 
void process_value(int&& i) { 
 std::cout << "RValue processed: " << i << std::endl; 
} 
 
void forward_value(int&& i) { 
 process_value(i); 
} 
 
int main() { 
 int a = 0; 
 process_value(a); 
 process_value(1); 
 forward_value(2); 
}
```

```c++
LValue processed: 0 
RValue processed: 1 
LValue processed: 2
```

虽然 2 这个立即数在函数 forward_value 接收时是右值，但到了 process_value 接收时，变成了左值。 

### 转移语义的定义

右值引用是用来支持转移语义的。转移语义可以将资源 ( 堆，系统对象等 ) 从一个对象转移到另一个对象，这样能够减少不必要的临时对象的创建、拷贝以及销毁，能够大幅度提高 C++ 应用程序的性能。临时对象的维护 ( 创建和销毁 ) 对性能有严重影响。

转移语义是和拷贝语义相对的，可以类比文件的剪切与拷贝，当我们将文件从一个目录拷贝到另一个目录时，速度比剪切慢很多。

通过转移语义，临时对象中的资源能够转移其它的对象里。

在现有的 C++ 机制中，我们可以定义拷贝构造函数和赋值函数。要实现转移语义，需要定义转移构造函数，还可以定义转移赋值操作符。对于右值的拷贝和赋值会调用转移构造函数和转移赋值操作符。如果转移构造函数和转移拷贝操作符没有定义，那么就遵循现有的机制，拷贝构造函数和赋值操作符会被调用。

普通的函数和操作符也可以利用右值引用操作符实现转移语义。



### 实现转移构造函数和转移赋值函数

以一个简单的 string 类为示例，实现拷贝构造函数和拷贝赋值操作符。

```c++
class MyString { 
private: 
 char* _data; 
 size_t   _len; 
    
 void _init_data(const char *s) { 
   _data = new char[_len+1]; 
   memcpy(_data, s, _len); 
   _data[_len] = '\0'; 
 } 
public: 
 MyString() { 
   _data = NULL; 
   _len = 0; 
 } 
 
 MyString(const char* p) { 
   _len = strlen (p); 
   _init_data(p); 
 } 
 
 MyString(const MyString& str) { 
   _len = str._len; 
   _init_data(str._data); 
   std::cout << "Copy Constructor is called! source: " << str._data << std::endl; 
 } 
 
 MyString& operator=(const MyString& str) { 
   if (this != &str) { 
     _len = str._len; 
     _init_data(str._data); 
   } 
   std::cout << "Copy Assignment is called! source: " << str._data << std::endl; 
   return *this; 
 } 
 
 virtual ~MyString() { 
   if (_data) free(_data); 
 } 
}; 
 
int main() { 
 MyString a; 
 a = MyString("Hello"); 
 std::vector<MyString> vec; 
 vec.push_back(MyString("World")); 
}
```

运行结果 :

```
Copy Assignment is called! source: Hello 
Copy Constructor is called! source: World

```

这个 string 类已经基本满足我们演示的需要。在 main 函数中，实现了调用拷贝构造函数的操作和拷贝赋值操作符的操作。MyString(“Hello”) 和 MyString(“World”) 都是临时对象，也就是右值。虽然它们是临时的，但程序仍然调用了拷贝构造和拷贝赋值，造成了没有意义的资源申请和释放的操作。如果能够直接使用临时对象已经申请的资源，既能节省资源，有能节省资源申请和释放的时间。这正是定义转移语义的目的。

我们先定义转移构造函数。

```
MyString(MyString&& str) { 
   std::cout << "Move Constructor is called! source: " << str._data << std::endl; 
   _len = str._len; 
   _data = str._data; 
   str._len = 0; 
   str._data = NULL; 
}

```

和拷贝构造函数类似，有几点需要注意：

1. 参数（右值）的符号必须是右值引用符号，即“&&”。
2. 参数（右值）不可以是常量，因为我们需要修改右值。
3. 参数（右值）的资源链接和标记必须修改。否则，右值的析构函数就会释放资源。转移到新对象的资源也就无效了。

现在我们定义转移赋值操作符。

```c++
MyString& operator=(MyString&& str) { 
   std::cout << "Move Assignment is called! source: " << str._data << std::endl; 
   if (this != &str) { 
     _len = str._len; 
     _data = str._data; 
     str._len = 0; 
     str._data = NULL; 
   } 
   return *this; 
}
```

这里需要注意的问题和转移构造函数是一样的。

增加了转移构造函数和转移复制操作符后，我们的程序运行结果为 :

```c++
Move Assignment is called! source: Hello 
Move Constructor is called! source: World
```

由此看出，编译器区分了左值和右值，对右值调用了转移构造函数和转移赋值操作符。节省了资源，提高了程序运行的效率。

有了右值引用和转移语义，我们在设计和实现类时，对于需要动态申请大量资源的类，应该设计转移构造函数和转移赋值函数，以提高应用程序的效率。

### 标准库函数 std::move  std::forward

既然编译器只对右值引用才能调用转移构造函数和转移赋值函数，而所有命名对象都只能是左值引用，**如果已知一个命名对象不再被使用而想对它调用转移构造函数和转移赋值函数，也就是把一个左值引用当做右值引用来使用**，怎么做呢？标准库提供了函数 std::move，这个函数以非常简单的方式将左值引用转换为右值引用。

`std::move`和`std::forward`仅仅是进行转换的函数。`std::move`无条件地将它的参数转换为右值，而`std::forward`只在某些条件满足时进行这种转换（**当且仅当**它的参数是通过右值初始化时进行转换）。

示例程序 :

```c++
void ProcessValue(int& i) { 
 std::cout << "LValue processed: " << i << std::endl; 
} 
 
void ProcessValue(int&& i) { 
 std::cout << "RValue processed: " << i << std::endl; 
} 
 
int main() { 
 int a = 0; 
 ProcessValue(a); 
 ProcessValue(std::move(a)); 
}
```

运行结果 : 

```
LValue processed: 0 
RValue processed: 0

```

`std::move`在提高 swap 函数的的性能上非常有帮助，一般来说，`swap`函数的通用定义如下：

```
template <class T> swap(T& a, T& b) 
   { 
       T tmp(a);   // copy a to tmp 
       a = b;      // copy b to a 
       b = tmp;    // copy tmp to b 
}

```

有了 std::move，swap 函数的定义变为 :

```
 template <class T> swap(T& a, T& b) 
   { 
       T tmp(std::move(a)); // move a to tmp 
       a = std::move(b);    // move b to a 
       b = std::move(tmp);  // move tmp to b 
}

```

通过 std::move，一个简单的 swap 函数就避免了 3 次不必要的拷贝操作。



C++11 中定义的 T&& 的推导规则为：

右值实参为右值引用，左值实参仍然为左值引用。

一句话，就是参数的属性不变。这样也就完美的实现了参数的完整传递。

右值引用，表面上看只是增加了一个引用符号，但它对 C++ 软件设计和类库的设计有非常大的影响。它既能简化代码，又能提高程序运行效率。每一个 C++ 软件设计师和程序员都应该理解并能够应用它。我们在设计类的时候如果有动态申请的资源，也应该设计转移构造函数和转移拷贝函数。在设计类库时，还应该考虑 std::move 的使用场景并积极使用它。





[TOC]

# C++内存管理

## new

1. **调用 operator new 分配内存（operator new可以被重载），用一个指针记下来**
   1. **调用malloc**
2. **对指针转型**
3. **使用此指针调用构造函数**



**注意 程序员不能直接调用构造函数，若想要调用，请使用placement new**

![1594014211325](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1594014211325.png)

![1594013757339](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1594013757339.png)

![1593701626459](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1593701626459.png)

![1593701748136](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1593701748136.png)

## delete

1. **先调用析构函数**
2. **再调用operator delete**

![1593701690793](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1593701690793.png)

![1593701811540](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1593701811540.png)

## **Placement New**

![1594015295266](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1594015295266.png)

## C++有了malloc/free 为什么还要new/delete？

- 创建C++的对象时，不仅仅是需要申请空间，还需要自动调用构造函数，以及在对象消亡之前要自动执行析构函数。 
- malloc/free只能申请空间，无法对空间进行操作，无法满足动态对象的要求。
- 说到底，mallco/free是C语言库函数，不在编译器控制权限之内，无法执行构造函数和析构函数。

## C++malloc/free 和new/delete区别？

- malloc/free和是C标准库函数，new/delete是C++的运算符。

![1593955371924](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1593955371924.png)

4）：malloc/free  和 new/delete 的相同点和不同点

相同点：它们都可以申请和释放空间。

不同点：

一、new/delete 在申请空间的时候能对空间进行操作，而malloc/free 不能。

（1）new ：分配内存 + 调用类的构造函数 + 初始化  delete：释放内存 + 调用类的析构函数

（2）malloc：只分配内存，不会进行初始化类成员的工作   free只释放内存，不会调用析构函数

二、new/delete是C++运算符，能重载

（1）new、delete 是运算符，可以进行重载

（2）malloc,free是标准库函数，不可以进行重载，但可以覆盖。

三、new delete 更加安全，简单：

（1）不用计算类型大小：自动计算要分配存储区的字节数

（2）不用强制类型转换：自动返回正确的指针类型（二者返回值不同，一个为void*,一个是某种数据类型指针）

## New[N]

1. 调用operator new分配空间。
2. 调用N此构造函数来初始化对象。 

## Delete[N]

1. 调用N次析构函数清理对象。 
2. 调用operator delete释放空间。 

## 内存对齐

### 内存对齐规则

每个特定平台上的编译器都有自己的默认“对齐系数”（也叫对齐模数）。**gcc中默认#pragma pack(4)（这也许是以前的版本，现在版本（8.1）不是这样**，可以通过预编译命令#pragma pack(n)，n = 1,2,4,8,16来改变这一系数。

有效对齐值：是给定值#pragma pack(n)和结构体中最长数据类型长度中较小的那个。有效对齐值也叫**对齐单位**。

了解了上面的概念后，我们现在可以来看看内存对齐需要遵循的规则：

(1) 结构体第一个成员的**偏移量（offset）**为0，以后每个成员相对于结构体首地址的 offset 都是**该成员大小与有效对齐值中较小那个**的整数倍，如有需要编译器会在成员之间加上填充字节。

(3) **结构体的总大小**为 有效对齐值 的**整数倍**，如有需要编译器会在最末一个成员之后加上填充字节。

```c++
//32位系统
#include<stdio.h>
struct
{
    int i;    
    char c1;  
    char c2;  
}x1;

struct{
    char c1;  
    int i;    
    char c2;  
}x2;

struct{
    char c1;  
    char c2; 
    int i;    
}x3;

int main()
{
    printf("%d\n",sizeof(x1));  // 输出8
    printf("%d\n",sizeof(x2));  // 输出12
    printf("%d\n",sizeof(x3));  // 输出8
    return 0;
}
```

![preview](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/v2-86c644ce29b1e2d3858380aaa631cc1d_r.jpg) 

### 为什么进行内存对齐

1. 平台原因(移植原因)：不是所有的硬件平台都能访问任意地址上的任意数据的；某些硬件平台只能在某些地址处取某些特定类型的数据，否则抛出硬件异常。
2. 性能原因：数据结构(尤其是栈)应该尽可能地在自然边界上对齐。原因在于，为了访问未对齐的内存，处理器需要作两次内存访问；而对齐的内存访问仅需要一次访问。  

程序员通常倾向于认为内存就像一个字节数组.在C及其衍生语言中,char * 用来指代”一块内存”

![img](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/1.jpeg)



**尽管内存是以字节为单位，但是大部分处理器并不是按字节块来存取内存的.它一般会以双字节,四字节,8字节,16字节甚至32字节为单位来存取内存，我们将上述这些存取单位称为内存存取粒度.**

![img](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/2.jpeg)



现在考虑4字节存取粒度的处理器取int类型变量（32位系统），该处理器只能从地址为4的倍数的内存开始读取数据。

假如没有内存对齐机制，数据可以任意存放，现在一个int变量存放在从地址1开始的联系四个字节地址中，该处理器去取数据时，要先从0地址开始读取第一个4字节块,剔除不想要的字节（0地址）,然后从地址4开始读取下一个4字节块,同样剔除不要的数据（5，6，7地址）,最后留下的两块数据合并放入寄存器.这需要做很多工作.

![img](C:\Users\mycan\Documents\CppGuild\memory_contral\picture\6.jpeg) 

现在有了内存对齐的，int类型数据只能存放在按照对齐规则的内存中。内存从0地址开始，都是按照对齐规则放在内存中的，那么现在该处理器在取数据时一次性就能将数据读出来了，而且不需要做额外的操作，提高了效率。 



## C++内存分区

- 栈（stack）：指那些由编译器在需要的时候分配，不需要时⾃动清除的变量所在的存储区，效率高，分配的内存空间有限，形参和局部变量分配在栈区，栈是向地地址生长的数据结构，是一块连续的内存
- 堆（heap）：由程序员控制内存的分配和释放的存储区，是向高地址生长的数据结构，是不连续的存储空间，堆的分配(malloc)和释放(free)有程序员控制，容易造成二次删除和内存泄漏
- 静态存储区（static）：存放全局变量和静态变量的存储区，初始化的变量放在初始化区，未初始化的变量放在未初始化区。在程序结束后释放这块空间
- 常量存储区（const）：存放常量字符串的存储区，只能读不能写，const修饰的全局变量存储在常量区（取决于编译器），const修饰的局部变量在栈区
- 程序代码区：存放源程序二进制代码
- ![img](C:/Users/mycan/Documents/CppGuild/memory_contral/picture/format,png) 

## 堆和栈究竟有什么区别

　　好了，我们回到我们的主题：堆和栈究竟有什么区别？
　　主要的区别由以下几点：
　　(1). 管理方式不同
　　(2). 空间大小不同
　　(3). 能否产生碎片不同
　　(4). 生长方向不同
　　(5). 分配方式不同
　　(6). 分配效率不同
　　**管理方式：对于栈来讲，是由编译器自动管理，无需我们手工控制；对于堆来说，释放工作由程序员控制，容易产生`memory leak`。**
　　**空间大小：一般来讲在32位系统下，堆内存可以达到4G的空间，从这个角度来看堆内存几乎是没有什么限制的。但是对于栈来讲，一般都是有一定的空间大小的，例如，在VC6下面，默认的栈空间大小是1M（好像是，记不清楚了）。当然，我们可以修改：**

　　**碎片问题：对于堆来讲，频繁的`new/delete`势必会造成内存空间的不连续，从而造成大量的碎片，使程序效率降低。**对于栈来讲，则不会存在这个问题，因为栈是先进后出的队列，他们是如此的一一对应，以至于永远都不可能有一个内存块从栈中间弹出，在他弹出之前，在他上面的后进的栈内容已经被弹出，详细的可以参考数据结构，这里我们就不再一一讨论了。
　　**生长方向：对于堆来讲，生长方向是向着内存地址增加的方向；对于栈来讲，它的生长方向是向着内存地址减小的方向增长。**
　　**分配方式：****堆都是动态分配的，没有静态分配的堆。栈有2种分配方式：静态分配和动态分配。静态分配是编译器完成的，比如局部变量的分配。**动态分配由`alloca`函数进行分配，但是栈的动态分配和堆是不同的，他的动态分配是由编译器进行释放，无需我们手工实现。
　　**分配效率：****栈是机器系统提供的数据结构，计算机会在底层对栈提供支持：分配专门的寄存器存放栈的地址，压栈出栈都有专门的指令执行，这就决定了栈的效率比较高。**堆则是C/C++函数库提供的，它的机制是很复杂的，例如为了分配一块内存，库函数会按照一定的算法（具体的算法可以参考数据结构/操作系统）在堆内存中搜索可用的足够大小的空间，如果没有足够大小的空间（可能是由于内存碎片太多），就有可能调用系统功能去增加程序数据段的内存空间，这样就有机会分到足够大小的内存，然后进行返回。显然，堆的效率比栈要低得多。
　　**从这里我们可以看到，堆和栈相比，由于大量`new/delete`的使用，容易造成大量的内存碎片；由于没有专门的系统支持，效率很低；由于可能引发用户态和核心态的切换，内存的申请，代价变得更加昂贵。所以栈在程序中是应用最广泛的，就算是函数的调用也利用栈去完成，函数调用过程中的参数，返回地址，EBP和局部变量都采用栈的方式存放。所以，我们推荐大家尽量用栈，而不是用堆。**

# 计算机网络面经

# 1 网络结构

## 1.1 有哪些网络结构

计算机网络一共有3种模型。

1. OSI七层结构
2. TCP/IP结构
3. 五层协议结构

![img](https://uk-1259555870.cos.eu-frankfurt.myqcloud.com/20200216134035.png) 

OSI是Open Systems Interconnect，也就是开放的互联系统，将复杂的互联网系统划分为不同块，方便处理。实际应用中，并没有采用这个理论模型，而是使用TCP/IP协议的四层模型。而5层模型是一个理论上的网络通信模型，方便教学的时候理解，实际上并不存在。 

![1593255216105](C:\Users\mycan\Documents\CppGuild\computer networks\picture\1593255216105.png)

## 1.2 为什么要分层

之所以要分层，在工程学中有个很重的 概念是解耦每一只做自己之所以要分层，在工程学中有个很重的 概念是解耦每一只做自己之所以要分层，在工程学中有个很重的 概念是解耦每一只做自己之所以要分层，在工程学中有个很重的概念是解耦每一只做自己事。



# 2 TCP/IP协议

消息-------->报文段------->数据包------>帧

以上五个术语都用来表述数据的单位，大致区分如下：

- 帧用于表示数据链路层中包的单位；
- 数据包是 IP 和 UDP 等网络层以上的分层中包的单位；
- 段则表示 TCP 数据流中的信息；
- 消息是指应用协议中数据的单位。

![1593259710680](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/1593259710680.png)

![img](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/v2-8149ac257c0302d7225af9fe5879cfa7_720w.jpg) 

![1593259836725](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/1593259836725.png)

## 应用层

应用层的任务是通过**应用进程间的交互**来完成特定网络应用 

## 传输层

为两台主机进程之间的通信提供**通用的数据传输服务** 。建立连接需要的行为、传输数据需要的行为、断开连接需要的行为。

### TCP和UDP的区别？

简单来说：

- TCP：面向连接，面向字节流，可靠，传输慢，有流量控制阻塞控制。以段为单位发送数据。
- UDP：广播形式不需要连接，面向报文，不可靠，传输快，无流量控制阻塞控制。直接将UDP包发出去。

解释一下报文和字节流的区别：

- 字节流：**发送次数和接收次数可以不相同**，比如向水池倒了20盆水，可以开水龙头一次性全放出。
- 报文：**发送次数和接收次数必须相同**。

两者的应用场景：

- TCP：邮件，远程登录，文件传输等对准确性要求较高的地方
- UDP：及时通信，比如QQ，网络电话等。
- 

### TCP三次握手/四次挥手

![img](https://i.bmp.ovh/imgs/2019/07/8dabc100eb0549e0.png)  

![img](https://i.bmp.ovh/imgs/2019/07/074e5304e133a22c.png) 

位码即tcp标志位，有6种标示：SYN(synchronous建立联机) ACK(acknowledgement 确认) PSH(push传送) FIN(finish结束) RST(reset重置) URG(urgent紧急)Sequence number(顺序号码) Acknowledge number(确认号码)

#### **1 为什么不能用两次握手连接？**

- 如果是两次握手，**服务器端无法确认自己输出数据的通道是否有问题。**
- **防止已经失效的连接请求报文段突然又传送到了 B，因而产生错误 。**
- **防止历史连接初始化了连接。** 
- **「两次握手」：无法防止历史连接的建立，会造成双方资源的浪费，也无法可靠的同步双方序列号；*「四次握手」：三次握手就已经理论上最少可靠连接建立，所以不需要使用更多的通信次数。**
- 若之间两次，B在回复后就给A发消息，但是回复却丢了，A又会重传，但是B已经给A发消息，有点问题。

#### **2 Server 端收到 Client 端的 SYN 后，为什么还要传回 SYN？**

- 接收端传回发送端所发送的SYN是为了告诉发送端，我接收到的信息确实就是你所发送的信号了。 
- 传回SYN是建立服务器端到客户端的连接

#### **3、传了 SYN，为什么还要传 ACK？**

- ACK是确认客户端到服务器端的连接。

#### **4、为什么不四次握手？**

- 没有必要

#### **5、为什么是四次挥手？**

由于 TCP 协议是全双工的，也就是说客户端和服务端都可以发起断开连接。两边各发起一次断开连接的申请，加上各自的两次确认，看起来就像执行了四次挥手。  

#### **6、为什么 TIME-WAIT 状态必须等待 2MSL（Maximum Segment Lifetime ） 的时间呢？**

1. 为了保证 A 发送的最后一个 ACK 报文段能够到达 B。这个 ACK 报文段有可能丢失，因而使处在 LAST-ACK 状态的 B 收不到对已发送的 FIN + ACK 报文段的确认。B 会超时重传这个 FIN+ACK 报文段，而 A 就能在 2MSL 时间内**（超时 + 1MSL 传输）**收到这个重传的 FIN+ACK 报文段。接着 A 重传一次确认，重新启动 2MSL 计时器。最后，A 和 B 都正常进入到 CLOSED 状态。**如果 A 在 TIME-WAIT 状态不等待一段时间，而是在发送完 ACK 报文段后立即释放连接，那么就无法收到 B 重传的 FIN + ACK 报文段，因而也不会再发送一次确认报文段，这样，B 就无法按照正常步骤进入 CLOSED 状态。**
2. A 在发送完最后一个 ACK 报文段后，再经过时间 2MSL，就可以**使本连接持续的时间内所产生的所有报文段都从网络中消失**。**这样就可以使下一个连接中不会出现这种旧的连接请求报文段。**
3. 

#### **7、DDos 预防 ( 没有彻底根治的办法，除非不使用TCP )**

- 限制同时打开SYN半链接的数目
- 缩短SYN半链接的Time out 时间
- 关闭不必要的服务
- syn cookie

#### 8、TCP的SYN队列和Accept队列

<https://www.cnblogs.com/linguoguo/p/12369959.html> 



### TCP协议如何保证可靠性



**（1）**检验和、序列号、确认应答、重发控制、连接管理、窗口控制

![1593271586151](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/1593271586151.png)

**（2）超时重发如何确定？**

- TCP在每次发包时都会计算往返时间及其偏差（方差），将往返时间和 偏差相加、超时重发的时间就是比这个和稍微大一点的值。
- 若超时，等待确认时间以指数增长

**（3）丢弃重复的包**。

- 重传一个确认就可以防止发送方再次发送，接收方这边保留一份即可。

**（4）设置最大消息长度（MSS)**

![1593274226826](C:\Users\mycan\Documents\CppGuild\computer networks\picture\1593274226826.png)

**（4）失序数据重新排序**。

- 一是对没有按序号到达的报文直接丢弃。
- 二是将未按序号到达的数据包先放于缓冲区内，等待它前面 的序号包到达后，再将它交给应用进程。
- 后一种方法将会提高系统的效率。例如，发送方连续发送了每个报文中100个字节的TCP数据报，其序号分别是1， 101，201，…,701。假如其它7个数据报都收到了，而201这个数据报没有收到，则接收端应当对1和101这两个数据报进行确认，并将数据递交给相关的应用 进程，301至701这5个数据报则应当放于缓冲区，等到201这个数据报到达后，然后按序将201至701这些数据报递交给相关应用进程，并对701数据报进行 确认，确保了应用进程级的TCP数据的按序到达。 

**对于可靠性，TCP通过以下方式进行保证：**

数据包校验：目的是检测数据在传输过程中的任何变化，若校验出包有错，则丢弃报文段并且不给出响应，这时TCP发送数据端超时后会重发数据；

对失序数据包重排序：既然TCP报文段作为IP数据报来传输，而IP数据报的到达可能会失序，因此TCP报文段的到达也可能会失序。TCP将对失序数据进行重新排序，然后才交给应用层；

丢弃重复数据：对于重复数据，能够丢弃重复数据；

应答机制：当TCP收到发自TCP连接另一端的数据，它将发送一个确认。这个确认不是立即发送，通常将推迟几分之一秒；

超时重发：当TCP发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段；

流量控制：TCP连接的每一方都有固定大小的缓冲空间。TCP的接收端只允许另一端发送接收端缓冲区所能接纳的数据，这可以防止较快主机致使较慢主机的缓冲区溢出，这就是流量控制。TCP使用的流量控制协议是可变大小的滑动窗口协议。

**（1）**采用三次握手四次挥手保证建立的**传输信道是可靠的**。

**（2）**采用了**ARQ自动重传请求**协议**数据传输的可靠性**。

**（3）**采用**滑动窗口**协议进行流量控制

**（4）**使用**慢开始**、**拥塞避免**、**快重传**和**快恢复**来进行**拥塞控制**

### **ARQ协议**

一、ARQ协议

ARQ协议，即自动重传请求（Automatic Repeat-reQuest），它通过使用确认和超时这两个机制，如果发送方在发送后一段时间之内没有收到确认帧，它通常会重新发送。ARQ包括停止等待ARQ协议和连续ARQ协议。

一:停止等待协议
停止等待协议是tcp保证传输可靠的重要途径,”停止等待”就是指发送完一个分组就停止发送,等待对方的确认,只有对方确认过,才发送下一个分组.

> 1:无差错情况:发送方发送分组,接收方在规定时间内收到,并且回复确认.发送方再次发送……
> [![TCP协议总结--停止等待协议,连续ARQ协议,滑动窗口协议](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/b18941a85b3252818cdb21658de1a162_thumb.png)](http://img.jeepxie.net/upload/b/18/b18941a85b3252818cdb21658de1a162_thumb.png)
> *2:超时重传有以下三种情况:*
> *(1)分组丢失:发送方发送分组,接收方没有收到分组,那么接收方不会发出确认,只要发送方过一段时间没有收到确认,就认为刚才的分组丢了,那么发送方就会再次发送.*
> *(2):确认丢失:发送方发送成功,接收方接收成功,确认分组也被发送,但是分组丢失,那么到了等待时间,发送方没有收到确认,又会发送分组过去,此时接收方前面已经收到了分组,那么此时接收方要做的事就是:丢弃分组,重新发送确认.*
> *(3):传送延迟:发送方发送成功,接收方接收成功,确认分组也被发送,没有丢失,但是由于传输太慢,等到了发送方设置的时间,发送方又会重新发送分组,此时接收方要做的事情:丢弃分组,重新发送确认. 发送方如果收到两个或者多个确认,就停止发送,丢弃其他确认.*
> [![TCP协议总结--停止等待协议,连续ARQ协议,滑动窗口协议](C:\Users\mycan\Documents\CppGuild\computer networks\picture\4278a013faf01be0cbac3f271909f403_thumb.png)](http://img.jeepxie.net/upload/4/27/4278a013faf01be0cbac3f271909f403_thumb.png)

停止等待协议的优点是简单,但是缺点是信道的利用率太低,一次发送一条消息,使得信道的大部分时间内都是空闲的,为了提高效率,我们采用流水线传输,这就与下面两个协议有关系了.

二:连续ARQ协议和滑动窗口协议
这两个协议主要解决的问题信道效率低和增大了吞吐量,以及控制流量的作用.

- 连续ARQ协议:它是指发送方维护着一个窗口,这个窗口中不止一个分组,有好几个分组,窗口的大小是由接收方返回的win值决定的,所以窗口的大小是动态变化的,只要在窗口中的分组都可以被发送,这就使得TCP一次不是只发送一个分组了,从而大大提高了信道的利用率.并且它采用累积确认的方式,对于**按序**到达的最后一个分组发送确认.
- 滑动窗口协议:之所以叫滑动窗口协议,是因为窗口是不断向前走的,该协议允许发送方在停止并等待确认前发送多个数据分组。由于发送方不必每发一个分组就停下来等待确认，因此该协议可以加速数据的传输,还可以控制流量的问题.
- 累积确认:如果发送方发送了5个分组,接收方只收到了1,2,4,5,没有收到3分组,那么我的确认信息只会说我期望下一个收到的分组是第三个,此时发送方会将3,4,5,全部重发一次,当通信质量不是很好的时候,连续ARQ还是会带来负面影响.

### TCP流量控制

防止发送方发的太快，耗尽接收方的资源，从而使接收方来不及处理。

<https://blog.csdn.net/dangzhangjing97/article/details/81008836> 

3.滑动窗口的一些知识点

（1）接收端将自己可以接收的缓冲区大小放入TCP首部中的“窗口大小”字段，通过ACK来通知发送端
（2）窗口大小字段越大，说明网络的吞吐率越高
（3）窗口大小指的是无需等待确认应答而可以继续发送数据的最大值，即就是说不需要接收端的应答，可以一次连续的发送数据
（4）操作系统内核为了维护滑动窗口，需要开辟发送缓冲区，来记录当前还有那些数据没有应答，只有确认应答过的数据，才能从缓冲区删掉

ps：发送缓冲区如果太大，就会有空间开销

（5）接收端一旦发现自己的缓冲区快满了，就会将窗口大小设置成一个更小的值通知给发送端，发送端收到这个值后，就会减慢自己的发送速度
（6）如果接收端发现自己的缓冲区满了，就会将窗口的大小设置为0，此时发送端将不再发送数据，但是需要定期发送一个窗口探测数据段，使接收端把窗口大小告诉发送端

ps: 在TCP的首部中，有一个16为窗口字段，此字段就是用来存放窗口大小信息的



## 网络层

- IPv4 32bit。IP地址由两部分组成，即网络号（ Network ID）和主机号（ Host ID）。
- 网络号标识的是 Internet上的一个子网，而主机号标识是中某台。
- Network ID = (IP) & (Subnet Mask) 
- Host ID = (IP) & ~ (Subnet Mask)

![1593259546390](C:\Users\mycan\Documents\CppGuild\computer networks\picture\1593259546390.png)

![1593259571264](C:\Users\mycan\Documents\CppGuild\computer networks\picture\1593259571264.png)



**IP提供不可靠，无连接得服务**



![1593260604289](C:\Users\mycan\Documents\CppGuild\computer networks\picture\1593260604289.png)

![1593261030191](C:/Users/mycan/Documents/CppGuild/computer%20networks/picture/1593261030191.png)



**路由算法就是在寻找下一跳**

**路由器的一个作用是连通不同的网络，另一个作用是选择信息传送的线路** 

**路由算法暂不介绍**



[TOC]

# 操作系统

## 进程和线程

### 进程和线程的区别

简而言之,一个程序至少有一个进程,一个进程至少有一个线程.
线程的划分尺度小于进程，使得多线程程序的并发性高。
另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。
线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。
从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。

进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动,进程是系统进行资源分配和调度的一个独立单位.
线程是进程的一个实体,是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位.线程自己基本上不拥有系统资源,只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源.
一个线程可以创建和撤销另一个线程;同一个进程中的多个线程之间可以并发执行.

**进程和线程的主要差别在于它们是不同的操作系统资源管理方式。进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。如果有兴趣深入的话，我建议你们看看《现代操作系统》或者《操作系统的设计与实现》。对就个问题说得比较清楚。**



### Linux下的copy-on-write

在说明Linux下的copy-on-write机制前，我们首先要知道两个函数：fork()和exec()。需要注意的是exec()并不是一个特定的函数, 它是一组函数的统称, 它包括了execl()、execlp()、execv()、execle()、execve()、execvp()。

#### 1.1简单来用用fork

首先我们来看一下`fork()`函数是什么鬼：

> fork is an operation whereby a process creates a copy of itself.

fork是类Unix操作系统上**创建进程**的主要方法。fork用于**创建子进程**(等同于当前进程的副本)。

- 新的进程要通过老的进程复制自身得到，这就是fork！

如果接触过Linux，我们会知道Linux下**init进程是所有进程的爹**(相当于Java中的Object对象)

- Linux的进程都通过init进程或init的子进程fork(vfork)出来的。

 下面以例子说明一下fork吧：

```c++
#include <unistd.h>  
#include <stdio.h>  
 
int main ()   
{   
    pid_t fpid; //fpid表示fork函数返回的值  
    int count=0;
	
	// 调用fork，创建出子进程  
    fpid=fork();

	// 所以下面的代码有两个进程执行！
    if (fpid == -1)   
        printf("创建进程失败!/n");   
    else if (fpid == 0) {  
        printf("我是子进程，由父进程fork出来/n");   
        count++;  
    }  
    else if(fpid>0) {  
        printf("我是父进程/n");   
        count++;  
    }  
    printf("统计结果是: %d/n",count);  
    return 0;  
}  
```

得到的结果输出为：

```c++
我是子进程，由父进程fork出来

统计结果是: 1

我是父进程

统计结果是: 1

```

解释一下：

- fork作为一个函数被调用。这个函数会有**两次返回**，将**子进程的PID返回给父进程，0返回给子进程**。(如果小于0，则说明创建子进程失败)。
- 再次说明：当前进程调用`fork()`，会创建一个跟当前进程完全相同的子进程(除了pid)，所以子进程同样是会执行`fork()`之后的代码。

所以说：

- 父进程在执行if代码块的时候，`fpid变量`的值是子进程的pid
- 子进程在执行if代码块的时候，`fpid变量`的值是0

#### 1.2再来看看exec()函数

从上面我们已经知道了fork会创建一个子进程。**子进程的是父进程的副本**。

exec函数的作用就是：**装载一个新的程序**（可执行映像）覆盖**当前进程**内存空间中的映像，**从而执行不同的任务**。

- exec系列函数在执行时会**直接替换掉当前进程的地址空间**。

我去画张图来理解一下：

![exec函数的作用](https://user-gold-cdn.xitu.io/2018/10/31/166c94cfc1728f4e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

参考资料：

- 程序员必备知识——fork和exec函数详解[blog.csdn.net/bad_good_ma…](https://blog.csdn.net/bad_good_man/article/details/49364947)
- linux中fork（）函数详解（原创！！实例讲解）：[blog.csdn.net/jason314/ar…](https://blog.csdn.net/jason314/article/details/5640969)
- linux c语言 fork() 和 exec 函数的简介和用法：[blog.csdn.net/nvd11/artic…](https://blog.csdn.net/nvd11/article/details/8856278)
- Linux下Fork与Exec使用：[www.cnblogs.com/hicjiajia/a…](https://www.cnblogs.com/hicjiajia/archive/2011/01/20/1940154.html)
- Linux 系统调用 —— fork()内核源码剖析：[blog.csdn.net/chen8927040…](https://blog.csdn.net/chen892704067/article/details/76596225)

#### 1.3回头来看Linux下的COW是怎么一回事

> fork()会产生一个和父进程完全相同的子进程(除了pid)

如果按**传统**的做法，会**直接**将父进程的数据拷贝到子进程中，拷贝完之后，父进程和子进程之间的数据段和堆栈是**相互独立的**。

![父进程的数据拷贝到子进程中](https://user-gold-cdn.xitu.io/2018/10/31/166c94cfc1818295?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

但是，以我们的使用经验来说：往往子进程都会执行`exec()`来做自己想要实现的功能。

- 所以，如果按照上面的做法的话，创建子进程时复制过去的数据是没用的(因为子进程执行`exec()`，原有的数据会被清空)

既然很多时候复制给子进程的数据是无效的，于是就有了Copy On Write这项技术了，原理也很简单：

- fork创建出的子进程，**与父进程共享内存空间**。也就是说，如果子进程**不对内存空间进行写入操作的话，内存空间中的数据并不会复制给子进程**，这样创建子进程的速度就很快了！(不用复制，直接引用父进程的物理空间)。
- 并且如果在fork函数返回之后，子进程**第一时间**exec一个新的可执行映像，那么也不会浪费时间和内存空间了。

另外的表达方式：

> 在fork之后exec之前两个进程**用的是相同的物理空间**（内存区），子进程的代码段、数据段、堆栈都是指向父进程的物理空间，也就是说，两者的虚拟空间不同，但其对应的**物理空间是同一个**。

> 当父子进程中**有更改相应段的行为发生时**，再**为子进程相应的段分配物理空间**。

> 如果不是因为exec，内核会给子进程的数据段、堆栈段分配相应的物理空间（至此两者有各自的进程空间，互不影响），而代码段继续共享父进程的物理空间（两者的代码完全相同）。

> 而如果是因为exec，由于两者执行的代码不同，子进程的代码段也会分配单独的物理空间。

Copy On Write技术**实现原理：**

> fork()之后，kernel把父进程中所有的内存页的权限都设为read-only，然后子进程的地址空间指向父进程。当父子进程都只读内存时，相安无事。当其中某个进程写内存时，CPU硬件检测到内存页是read-only的，于是触发页异常中断（page-fault），陷入kernel的一个中断例程。中断例程中，kernel就会**把触发的异常的页复制一份**，于是父子进程各自持有独立的一份。

Copy On Write技术**好处**是什么？

- COW技术可**减少**分配和复制大量资源时带来的**瞬间延时**。
- COW技术可减少**不必要的资源分配**。比如fork进程时，并不是所有的页面都需要复制，父进程的**代码段和只读数据段都不被允许修改，所以无需复制**。

Copy On Write技术**缺点**是什么？

- 如果在fork()之后，父子进程都还需要继续进行写操作，**那么会产生大量的分页错误(页异常中断page-fault)**，这样就得不偿失。

几句话总结Linux的Copy On Write技术：

- fork出的子进程共享父进程的物理空间，当父子进程**有内存写入操作时**，read-only内存页发生中断，**将触发的异常的内存页复制一份**(其余的页还是共享父进程的)。
- fork出的子进程功能实现和父进程是一样的。如果有需要，我们会用`exec()`把当前进程映像替换成新的进程文件，完成自己想要实现的功能。

参考资料：

- Linux进程基础：[www.cnblogs.com/vamei/archi…](http://www.cnblogs.com/vamei/archive/2012/09/20/2694466.html)
- Linux写时拷贝技术(copy-on-write)[www.cnblogs.com/biyeymyhjob…](http://www.cnblogs.com/biyeymyhjob/archive/2012/07/20/2601655.html)
- 当你在 Linux 上启动一个进程时会发生什么？[zhuanlan.zhihu.com/p/33159508](https://zhuanlan.zhihu.com/p/33159508)
- Linux fork()所谓的写时复制(COW)到最后还是要先复制再写吗？[www.zhihu.com/question/26…](https://www.zhihu.com/question/265400460)
- 写时拷贝（copy－on－write） COW技术[blog.csdn.net/u012333003/…](https://blog.csdn.net/u012333003/article/details/25117457)
- Copy-On-Write 写时复制原理[blog.csdn.net/ppppppppp20…](https://blog.csdn.net/ppppppppp2009/article/details/22750939)



#### [Linux写时拷贝技术(copy-on-write)](https://www.cnblogs.com/biyeymyhjob/archive/2012/07/20/2601655.html)

**COW技术初窥：**

​      在Linux程序中，fork（）会产生一个和父进程完全相同的子进程，但子进程在此后多会exec系统调用，出于效率考虑，linux中引入了“写时复制“技术，也就是只有进程空间的各段的内容要发生变化时，才会将父进程的内容复制一份给子进程。

​      那么子进程的物理空间没有代码，怎么去取指令执行exec系统调用呢？

​      在fork之后exec之前两个进程用的是相同的物理空间（内存区），子进程的代码段、数据段、堆栈都是指向父进程的物理空间，也就是说，两者的虚拟空间不同，但其对应的物理空间是同一个。当父子进程中有更改相应段的行为发生时，再为子进程相应的段分配物理空间，如果不是因为exec，内核会给子进程的数据段、堆栈段分配相应的物理空间（至此两者有各自的进程空间，互不影响），而代码段继续共享父进程的物理空间（两者的代码完全相同）。而如果是因为exec，由于两者执行的代码不同，子进程的代码段也会分配单独的物理空间。      

​      在网上看到还有个细节问题就是，fork之后内核会通过将子进程放在队列的前面，以让子进程先执行，以免父进程执行导致写时复制，而后子进程执行exec系统调用，因无意义的复制而造成效率的下降。

 

**COW详述：**

​     现在有一个父进程P1，这是一个主体，那么它是有灵魂也就身体的。现在在其虚拟地址空间（有相应的数据结构表示）上有：正文段，数据段，堆，栈这四个部分，相应的，内核要为这四个部分分配各自的物理块。即：正文段块，数据段块，堆块，栈块。至于如何分配，这是内核去做的事，在此不详述。

1. 现在P1用fork()函数为进程创建一个子进程P2，

内核：

（1）复制P1的正文段，数据段，堆，栈这四个部分，注意是其内容相同。

（2）为这四个部分分配物理块，P2的：正文段－＞PI的正文段的物理块，其实就是不为P2分配正文段块，让P2的正文段指向P1的正文段块，数据段－＞P2自己的数据段块（为其分配对应的块），堆－＞P2自己的堆块，栈－＞P2自己的栈块。如下图所示：同左到右大的方向箭头表示复制内容。

 

![img](https://pic002.cnblogs.com/images/2012/426620/2012072019525880.jpg)

1. 写时复制技术：内核只为新生成的子进程创建虚拟空间结构，它们来复制于父进程的虚拟究竟结构，但是不为这些段分配物理内存，它们共享父进程的物理空间，当父子进程中有更改相应段的行为发生时，再为子进程相应的段分配物理空间。

 

![img](https://pic002.cnblogs.com/images/2012/426620/2012072020252592.jpg)

 

1. vfork()：这个做法更加火爆，内核连子进程的虚拟地址空间结构也不创建了，直接共享了父进程的虚拟空间，当然了，这种做法就顺水推舟的共享了父进程的物理空间

 

![img](https://pic002.cnblogs.com/images/2012/426620/2012072020020166.jpg)

通过以上的分析，相信大家对进程有个深入的认识，它是怎么一层层体现出自己来的，进程是一个主体，那么它就有灵魂与身体，系统必须为实现它创建相应的实体， 灵魂实体与物理实体。这两者在系统中都有相应的数据结构表示，物理实体更是体现了它的物理意义。以下援引LKD

​     传统的fork()系统调用直接把所有的资源复制给新创建的进程。这种实现过于简单并且效率低下，因为它拷贝的数据也许并不共享，更糟的情况是，如果新进程打算立即执行一个新的映像，那么所有的拷贝都将前功尽弃。Linux的fork()使用写时拷贝（copy-on-write）页实现。写时拷贝是一种可以推迟甚至免除拷贝数据的技术。内核此时并不复制整个进程地址空间，而是让父进程和子进程共享同一个拷贝。只有在需要写入的时候，数据才会被复制，从而使各个进程拥有各自的拷贝。也就是说，资源的复制只有在需要写入的时候才进行，在此之前，只是以只读方式共享。这种技术使地址空间上的页的拷贝被推迟到实际发生写入的时候。在页根本不会被写入的情况下—举例来说，fork()后立即调用exec()—它们就无需复制了。fork()的实际开销就是复制父进程的页表以及给子进程创建惟一的进程描述符。在一般情况下，进程创建后都会马上运行一个可执行的文件，这种优化可以避免拷贝大量根本就不会被使用的数据（地址空间里常常包含数十兆的数据）。由于Unix强调进程快速执行的能力，所以这个优化是很重要的。这里补充一点：**Linux COW与exec没有必然联系**

### linux下的进程状态

![1592632417683](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592632417683.png)

进程状态： 新建、就绪、运行、阻塞、停止。

![1592559274466](C:\Users\mycan\AppData\Local\Temp\1592559274466.png)

#### 为什么要使用线程 ？

- 我觉得最根本的原因是：一些业务需求在同一个进程内进行并发操作，这种情况下用单个的进程是无法实现的。
- 这样就需要多个可以共享资源的进程，就产生了线程。在linux内，线程只是一种进程间共享资源的手段。
- 线程比进程更容易创建、也更容易撤销

#### 线程创建

unix系统线程创建和进程创建类似

#### 多进程与多线程

**2017.8.8更新**：之前的回答有问题有误，纠正一下，应该来说二者的切换开销没有太大差别。本质上进程/线程在Linux内核实现上都是Task（或者叫Thread，在内核里是同一个东东），只不过同源多线程对应的Task共享的东西多一些（最主要是地址空间）。所以即便是多线程切换，页表也还是要切换的，只不过页表内容相同而已；同样，对于多线程切换，TLB该刷还是要刷的，因为对于CPU来讲多线程与多进程一样，都有不同的标识和不同的上下文，为了保证一致性，TLB刷新就省不了。

  

**在Linux下编程多用多进程编程少用多线程编程**。

​         IBM有个家伙做了个测试，发现切换线程context的时候，windows比linux快一倍多。进出最快的锁（windows2k的 critical section和linux的pthread_mutex），windows比linux的要快五倍左右。当然这并不是说linux不好，而且在经过实际编程之后，综合来看我觉得linux更适合做high performance server，不过在多线程这个具体的领域内，linux还是稍逊windows一点。这应该是情有可原的，毕竟unix家族都是从多进程过来的，而 windows从头就是多线程的。

如果是UNIX/linux环境，采用多线程没必要。

多线程比多进程性能高？误导！

应该说，**多线程比多进程成本低，但性能更低**。

在UNIX环境，多进程调度开销比多线程调度开销，没有显著区别，就是说，UNIX进程调度效率是很高的。内存消耗方面，二者只差全局数据区，现在内存都很便宜，服务器内存动辄若干G，根本不是问题。

**多进程是立体交通系统，虽然造价高，上坡下坡多耗点油，但是不堵车。**

**多线程是平面交通系统，造价低，但红绿灯太多，老堵车。**

我们现在都开跑车，油（主频）有的是，不怕上坡下坡，就怕堵车。



**多线程的优点：**

无需跨进程边界； 程序逻辑和控制方式简单； 所有线程可以直接共享内存和变量等； 线程方式消耗的总资源比进程方式好；

 **多线程缺点：**

每个线程与主程序共用地址空间，受限于2GB地址空间； 线程之间的同步和加锁控制比较麻烦； 一个线程的崩溃可能影响到整个程序的稳定性； 到达一定的线程数程度后，即使再增加CPU也无法提高性能，例如Windows Server 2003，大约是1500个左右的线程数就快到极限了（线程堆栈设定为1M），如果设定线程堆栈为2M，还达不到1500个线程总数； 线程能够提高的总性能有限，而且线程多了之后，线程本身的调度也是一个麻烦事儿，需要消耗较多的CPU

**多进程优点：**

每个进程互相独立，不影响主程序的稳定性，子进程崩溃没关系； 通过增加CPU，就可以容易扩充性能； 可以尽量减少线程加锁/解锁的影响，极大提高性能，就算是线程运行的模块算法效率低也没关系； 每个子进程都有2GB地址空间和相关资源，总体能够达到的性能上限非常大 

**多线程缺点：**

逻辑控制复杂，需要和主程序交互； 需要跨进程边界，如果有大数据量传送，就不太好，适合小数据量传送、密集运算 多进程调度开销比较大； 最好是多进程和多线程结合，即根据实际的需要，每个CPU开启一个子进程，这个子进程开启多线程可以为若干同类型的数据进行处理。当然你也可以利用多线程+多CPU+轮询方式来解决问题……

方法和手段是多样的，关键是自己看起来实现方便有能够满足要求，代价也合适。

－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－

**进程的优点：**

1）顺序程序的特点：具有封闭性和可再现性；

2）程序的并发执行和资源共享。多道程序设计出现后，实现了程序的并发执行和资源共享，提高了系统的效率和系统的资源利用率。 

**进程的缺点：**

操作系统调度切换多个线程要比切换调度进程在速度上快的多。而且进程间内存无法共享，通讯也比较麻烦。

线程之间由于共享进程内存空间，所以交换数据非常方便；在创建或撤消进程时，由于系统都要为之分配和回收资源，导致系统的开销明显大于创建或撤消线程时的开销。    

**线程的优点：**

1）它是一种非常"节俭"的多任务操作方式。在Linux系统下，启动一个新的进程必须分配给它独立的地址空间，建立众多的数据表来维护它的代码段、堆栈段和数据段，这是一种"昂贵"的多任务工作方式。而运行于一个进程中的多个线程，它们彼此之间使用相同的地址空间，共享大部分数据，启动一个线程所花费的空间远远小于启动一个进程所花费的空间，而且，线程间彼此切换所需的时间也远远小于进程间切换所需要的时间。当然，在具体的系统上，这个数据可能会有较大的区别；

2）线程间方便的通信机制，由于同一进程下的线程之间共享数据空间，所以一个线程的数据可以直接为其它线程所用，这不仅快捷，而且方便；

3）使多CPU系统更加有效。操作系统会保证当线程数不大于CPU数目时，不同的线程运行于不同的CPU上；

4）改善程序结构。一个既长又复杂的进程可以考虑分为多个线程，成为几个独立或半独立的运行部分，这样的程序会利于理解和修改。

 **线程的缺点：** 1.调度时, 要保存线程状态，频繁调度, 需要占用大量的机时； 2.程序设计上容易出错（线程同步问题）。

![1592624383264](C:\Users\mycan\AppData\Local\Temp\1592624383264.png)

#### 线程的实现方式

![1592624273003](C:\Users\mycan\AppData\Local\Temp\1592624273003.png)

 ![1592624345119](C:\Users\mycan\AppData\Local\Temp\1592624345119.png)

 

 前言

- linux内核不存在整真正意义上的线程。linux将所有的执行实体都称之为任务（task），每一个任务在干年上都类似于一个单线程的进程，具有内存空间、执行实体、文件资源等。但是，linux下不同任务之间可以选择公用内存空间，因而在实际意义上，共享同一个内存空间的多个任务构成了一个进程，而这些任务就成为这个任务里面的线程。

#### 内核线程（在内核中实现线程）

- 内核线程又称为守护进程，内核线程的调度由内核负责，一个内核线程处于阻塞状态时不影响其他的内核线程，因为其是调度的基本单位。这与用户线程是不一样的；
- 这些线程可以在全系统内进行资源的竞争；
- 内核空间内为每一个内核支持线程设置了一个线程控制块（TCB），内核根据该控制块，感知线程的存在，并进行控制。在一定程度上类似于进程，只是创建、调度的开销要比进程小。有的统计是1：10。
- 内核线程切换由内核控制，当线程进行切换的时候，由用户态转化为内核态。切换完毕要从内核态返回用户态，**即存在用户态和内核态之间的转换**，**比如多核cpu，还有win线程的实现**。

##### 优点

在多处理器系统中，内核能够同时调度同一进程中多个线程并行执行到多个处理器中；如果进程中的一个线程被阻塞，内核可以调度同一个进程中的另一个线程；内核支持线程具有很小的数据结构和堆栈，线程的切换比较快，切换开销小；内核本身也可以使用多线程的方式来实现。

##### 缺点

即使CPU在同一个进程的多个线程之间切换，也需要陷入内核，因此其速度和效率不如用户级线程。

**内核级线程速度慢**

#### 用户线程（在用户空间中实现线程）

- 用户线程在用户空间中实现，内核并没有直接对用户线程进程调度，内核的调度对象和传统进程一样，还是进程（用户进程）本身，内核并不能看到用户线程，内核并不知道用户线程的存在。
- 不需要内核支持而在用户程序中实现的线程，其不依赖于操作系统核心，应用进程利用线程库提供创建、同步、调度和管理线程的函数来控制用户线程。
- 内核资源的分配仍然是按照进程（用户进程）进行分配的；**各个用户线程只能在进程内进行资源竞争**。
- 用户级线程内核的切换由用户态程序自己控制内核切换（通过系统调用来获得内核提供的服务）,不需要内核干涉，少了进出内核态的消耗，但不能很好的利用多核Cpu。**目前Linux pthread大体是这么做的**。
- 每个用户线程并不具有自身的线程上下文。因此，就线程的同时执行而言，任意给定时刻每个进程只能够有一个线程在运行，而且只有一个处理器内核会被分配给该进程。

##### 优点

线程的切换无需陷入内核，故切换开销小，速度非常快；

##### 缺点

系统调用的阻塞问题：对应用程序来讲，**同一进程中只能同时有一个线程在运行**，一个线程的阻塞将导致整个进程中所有线程的阻塞；由于这里的处理器时间片分配是以进程为基本单位，所以每个线程执行的时间相对减少。

#### 用户级线程和内核级线程的区别

- **内核支持：**用户级线程可在一个不支持线程的OS中实现；内核支持线程则需要得到OS内核的支持。亦即内核支持线程是OS内核可感知的，而用户级线程是OS内核不可感知的。
- **处理器分配：**在多处理机环境下，对用户级线程而言主，内核一次只为一个进程分配一个处理器，进程无法享用多处理机带来的好处；在设置有内核支持线程时，内核可调度一个应用中的多个线程同时在多个处理器上并行运行，提高程序的执行速度和效率。
- **调度和线程执行时间：**设置有内核支持线程的系统，其调度方式和算法与进程的调度十分相似，只不过调度单位是线程；对只设置了用户级线程的系统，调度的单位仍为进程。
- 用户级线程执行系统调用指令时将导致其所属进程被中断，而内核支持线程执行系统调用指令时，只导致该线程被中断。
- 在只有用户级线程的系统内，CPU调度还是以进程为单位，处于运行状态的进程中的多个线程，由用户程序控制线程的轮换运行；在有内核支持线程的系统内，CPU调度则以线程为单位，由OS的线程调度程序负责线程的调度。

### linux下的睡眠和唤醒

在[Linux](https://link.zhihu.com/?target=http%3A//www.magedu.com/) 中，仅等待 CPU 时间的进程称为就绪进程，它们被放置在一个运行队列中，一个就绪进程的状 态标志位为 TASK_RUNNING。一旦一个运行中的进程时间片用完， Linux 内核的调度器会剥夺这个进程对 CPU 的控制权，并且从运行队列中选择一个合适的进程投入运行。

当然，一个进程也可以主动释放 CPU 的控制权。函数 schedule() 是一个调度函数，它可以被一个进程主动调用，从而调度其它进程占用 CPU。一旦这个主动放弃 CPU 的进程被重新调度占用 CPU，那么它将从上次停止执行的位置开始执行，也就是说它将从调用 schedule() 的下一行代码处开始执行。

有时候，进程需要等待直到某个特定的事件发生，例如设备初始化完成、I/O 操作完成或定时器到时等。在这种情况下，进程则必须从运行队列移出，加入到一个等待队列中，这个时候进程就进入了睡眠状态。

Linux 中的进程睡眠状态有两种：一种是可中断的睡眠状态，其状态标志位

TASK_INTERRUPTIBLE；

另一种是不可中断 的睡眠状态，其状态标志位为 TASK_UNINTERRUPTIBLE。可中断的睡眠状态的进程会睡眠直到某个条件变为真，比如说产生一个硬件中断、释放 进程正在等待的系统资源或是传递一个信号都可以是唤醒进程的条件。不可中断睡眠状态与可中断睡眠状态类似，但是它有一个例外，那就是把信号传递到这种睡眠 状态的进程不能改变它的状态，也就是说它不响应信号的唤醒。不可中断睡眠状态一般较少用到，但在一些特定情况下这种状态还是很有用的，比如说：进程必须等 待，不能被中断，直到某个特定的事件发生。

在现代的 Linux 操作系统中，进程一般都是用调用 schedule() 的方法进入睡眠状态的，下面的代码演示了如何让正在运行的进程进入睡眠状态。

1. `sleeping_task = current;`
2. `set_current_state(TASK_INTERRUPTIBLE);`
3. `schedule();`
4. `func1();`
5. `/* Rest of the code ... */`

在第一个语句中，程序存储了一份进程结构指针 sleeping_task，current 是一个宏，它指向正在执行的进程结构。set_current_state() 将该进程的状态从执行状态 TASK_RUNNING 变成睡眠状态TASK_INTERRUPTIBLE。 如果 schedule() 是被一个状态为TASK_RUNNING 的进程调度，那么 schedule() 将调度另外一个进程占用 CPU；如果 schedule() 是被一个状态为 TASK_INTERRUPTIBLE 或 TASK_UNINTERRUPTIBLE 的进程调度，那么还有一个附加的步骤将被执行：当前执行的进程在另外一个进程被调度之前会被从运行队列中移出，这将导致正在运行的那个进程进入睡眠，因为 它已经不在运行队列中了。

我们可以使用下面的这个函数将刚才那个进入睡眠的进程唤醒。

wake_up_process(sleeping_task);

在调用了 wake_up_process() 以后，这个睡眠进程的状态会被设置为 TASK_RUNNING，而且调度器会把它加入到运行队列中去。当然，这个进程只有在下次被调度器调度到的时候才能真正地投入运行。

2 无效唤醒

几乎在所有的情况下，进程都会在检查了某些条件之后，发现条件不满足才进入睡眠。可是有的时候进程却会在 判定条件为真后开始睡眠，如果这样的话进程就会无限期地休眠下去，这就是所谓的无效唤醒问题。在操作系统中，当多个进程都企图对共享数据进行某种处理，而 最后的结果又取决于进程运行的顺序时，就会发生竞争条件，这是操作系统中一个典型的问题，无效唤醒恰恰就是由于竞争条件导致的。

设想有两个进程 A 和 B，A 进程正在处理一个链表，它需要检查这个链表是否为空，如果不空就对链表里面的数据进行一些操作，同时 B 进程也在往这个链表添加节点。当这个链表是空的时候，由于无数据可操作，这时 A 进程就进入睡眠，当 B 进程向链表里面添加了节点之后它就唤醒 A 进程，其代码如下：

**A 进程:**

1. `1 spin_lock(&list_lock);`
2. `2``if(list_empty(&list_head)) {`
3. `3 spin_unlock(&list_lock);`
4. `4 set_current_state(TASK_INTERRUPTIBLE);`
5. `5 schedule();`
6. `6 spin_lock(&list_lock);`
7. `7 }`
8. `8`
9. `9``/* Rest of the code ... */`
10. `10 spin_unlock(&list_lock);`

**B 进程:**

1. `100 spin_lock(&list_lock);`
2. `101 list_add_tail(&list_head, new_node);`
3. `102 spin_unlock(&list_lock);`
4. `103 wake_up_process(processa_task);`

这里会出现一个问题，假如当 A 进程执行到第 3 行后第 4 行前的时候，B 进程被另外一个处理器调度投入运行。在这个时间片内，B 进程执行完了它所有的指令，因此它试图唤醒 A 进程，而此时的 A 进程还没有进入睡眠，所以唤醒操作无效。在这之后，A 进程继续执行，它会错误地认为这个时候链表仍然是空的，于是将自己的状态设置为 TASK_INTERRUPTIBLE 然后调用 schedule() 进入睡 眠。由于错过了 B 进程唤醒，它将会无限期的睡眠下去，这就是无效唤醒问题，因为即使链表中有数据需要处理，A 进程也还是睡眠了。

3 避免无效唤醒

如何避免无效唤醒问题呢？我们发现无效唤醒主要发生在检查条件之后和进程状态被设置为睡眠状态之前， 本来 B 进程的 wake_up_process() 提供了一次将 A 进程状态置为 TASK_RUNNING 的机会，可惜这个时候 A 进程的状态仍然是 TASK_RUNNING，所以 wake_up_process() 将 A 进程状态从睡眠状态转变为运行状态的努力 没有起到预期的作用。要解决这个问题，必须使用一种保障机制使得判断链表为空和设置进程状态为睡眠状态成为一个不可分割的步骤才行，也就是必须消除竞争条 件产生的根源，这样在这之后出现的 wake_up_process () 就可以起到唤醒状态是睡眠状态的进程的作用了。
找到了原因后，重新设计一下 A 进程的代码结构，就可以避免上面例子中的无效唤醒问题了。

**A 进程:**

1. `1 set_current_state(TASK_INTERRUPTIBLE);`
2. `2 spin_lock(&list_lock);`
3. `3``if(list_empty(&list_head)) {`
4. `4 spin_unlock(&list_lock);`
5. `5 schedule();`
6. `6 spin_lock(&list_lock);`
7. `7 }`
8. `8 set_current_state(TASK_RUNNING);`
9. `9`
10. `10``/* Rest of the code ... */`
11. `11 spin_unlock(&list_lock);`

可以看到，这段代码在测试条件之前就将当前执行进程状态转设置成 TASK_INTERRUPTIBLE 了，并且在链表不为空的情况下又将自己置为 TASK_RUNNING 状态。这样一来如果 B 进程在 A 进程进程检查了链表为空以后调用 wake_up_process()，那么 A 进程的状态就会自动由原来 TASK_INTERRUPTIBLE变成 TASK_RUNNING，此后即使进程又调用了 schedule()，由于它现在的状态是 TASK_RUNNING，所以仍然不会被从运行队列中移出，因而不会错误的进入睡眠，当然也就避免了无效唤醒问题。

4 Linux 内核的例子

在 Linux 操作系统中，内核的稳定性至关重要，为了避免在 Linux 操作系统内核中出现无效唤醒问题，
Linux 内核在需要进程睡眠的时候应该使用类似如下的操作：

1. `/* ‘q’是我们希望睡眠的等待队列 */`
2. `DECLARE_WAITQUEUE(wait,current);`
3. `add_wait_queue(q, &wait);`
4. `set_current_state(TASK_INTERRUPTIBLE);`
5. `/* 或 TASK_INTERRUPTIBLE */`
6. `while(!condition) /* ‘condition’ 是等待的条件 */`
7. `schedule();`
8. `set_current_state(TASK_RUNNING);`
9. `remove_wait_queue(q, &wait);`

上面的操作，使得进程通过下面的一系列步骤安全地将自己加入到一个等待队列中进行睡眠：首先调用 DECLARE_WAITQUEUE () 创建一个等待队列的项，然后调用 add_wait_queue() 把自己加入到等待队列中，并且将进程的状态设置为TASK_INTERRUPTIBLE 或者 TASK_INTERRUPTIBLE。然后循环检查条件是否为真：如果是的话就没有必要睡眠，如果条件不为真，就调用 schedule()。当进程 检查的条件满足后，进程又将自己设置为 TASK_RUNNING 并调用 remove_wait_queue() 将自己移出等待队列。

从上面可以看到，Linux 的内核代码维护者也是在进程检查条件之前就设置进程的状态为睡眠状态，然后才循环检查条件。如果在进程开始睡眠之前条件就已经达成了，那么循环会退出并用 set_current_state() 将自己的状态设置为就绪，这样同样保证了进程不会存在错误的进入睡眠的倾向，当然也就不会导致出现无效唤醒问题。

下面让我们用 linux 内核中的实例来看看 Linux 内核是如何避免无效睡眠的，这段代码出自 Linux2.6 的内核 (linux-2.6.11/kernel/sched.c: 4254):

1. `4253``/* Wait for kthread_stop */`
2. `4254 set_current_state(TASK_INTERRUPTIBLE);`
3. `4255``while (!kthread_should_stop()) {`
4. `4256 schedule();`
5. `4257 set_current_state(TASK_INTERRUPTIBLE);`
6. `4258 }`
7. `4259 __set_current_state(TASK_RUNNING);`
8. `4260``return``0;`

上面的这些代码属于迁移服务线程 migration_thread，这个线程不断地检查 kthread_should_stop()，

直 到 kthread_should_stop() 返回 1 它才可以退出循环，也就是说只要 kthread_should_stop() 返回 0 该进程就会一直睡 眠。从代码中我们可以看出，检查 kthread_should_stop() 确实是在进程的状态被置为 TASK_INTERRUPTIBLE 后才开始执行 的。因此，如果在条件检查之后但是在 schedule() 之前有其他进程试图唤醒它，那么该进程的唤醒操作不会失效。

小结

通过上面的讨论，可以发现在 Linux 中避免进程的无效唤醒的关键是在进程检查条件之前就将进程的状态置为 TASK_INTERRUPTIBLE 或 TASK_UNINTERRUPTIBLE，并且如果检查的条件满足的话就应该将其状态重新设置为 TASK_RUNNING。这样无论进程等待的条件是否满足， 进程都不会因为被移出就绪队列而错误地进入睡眠状态，从而避免了无效唤醒问题。

## 操作系统的调度算法

### 为什么调度？

单核cpu，同一时间只能跑一个进程，如果就绪进程队列中有多个进程，下一时刻那个进程先运行呢？就需要调度。操作系统中完成这一任务的被称为调度程序，改程序使用的算法被称为调度算法。

### linux下的进程调度

#### 进程优先级

　　进程提供了两种优先级，一种是普通的进程优先级，第二个是实时优先级。前者适用SCHED_NORMAL调度策略，后者可选SCHED_FIFO或SCHED_RR调度策略。**任何时候，实时进程的优先级都高于普通进程**，实时进程只会被更高级的实时进程抢占，同级实时进程之间是按照FIFO（一次机会做完）或者RR（多次轮转）规则调度的。

![1592644279073](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592644279073.png)

#### 实时进程的调度

　　实时进程，只有静态优先级，因为内核不会再根据休眠等因素对其静态优先级做调整，其范围在0~MAX_RT_PRIO-1间。默认MAX_RT_PRIO配置为100，也即，默认的实时优先级范围是0~99。而nice值，影响的是优先级在MAX_RT_PRIO~MAX_RT_PRIO+40范围内的进程。

　　不同与普通进程，系统调度时，实时优先级高的进程总是先于优先级低的进程执行。知道实时优先级高的实时进程无法执行。实时进程总是被认为处于活动状态。如果有数个 优先级相同的实时进程，那么系统就会按照进程出现在队列上的顺序选择进程。假设当前CPU运行的实时进程A的优先级为a，而此时有个优先级为b的实时进程B进入可运行状态，那么只要b<a，系统将中断A的执行，而优先执行B，直到B无法执行（无论A，B为何种实时进程）。

 　　不同调度策略的实时进程只有在相同优先级时才有可比性：

1. 对于FIFO的进程，意味着只有当前进程执行完毕才会轮到其他进程执行。由此可见相当霸道。
2. 对于RR的进程。一旦时间片消耗完毕，则会将该进程置于队列的末尾，然后运行其他相同优先级的进程，如果没有其他相同优先级的进程，则该进程会继续执行。

 　　总而言之，对于实时进程，高优先级的进程就是大爷。它执行到没法执行了，才轮到低优先级的进程执行。等级制度相当森严啊。

![1592647436514](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592647436514.png)

![1592647529141](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592647529141.png)

#### 普通进程的调度

　Linux对普通的进程，根据动态优先级进行调度。而动态优先级是由静态优先级（static_prio）调整而来。Linux下，静态优先级是用户不可见的，隐藏在内核中。而内核提供给用户一个可以影响静态优先级的接口，那就是nice值，两者关系如下：

　　static_prio=MAX_RT_PRIO +nice+ 20

　　nice值的范围是-20~19，因而静态优先级范围在100~139之间。nice数值越大就使得static_prio越大，最终进程优先级就越低。

　　ps -el 命令执行结果：NI列显示的每个进程的nice值，PRI是进程的优先级（如果是实时进程就是静态优先级，如果是非实时进程，就是动态优先级）　　

　　而进程的时间片就是完全依赖 static_prio 定制的，见下图，摘自《深入理解linux内核》，

　　![1592647964305](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592647964305.png)

![1592648080684](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592648080684.png) 　　

我们前面也说了，系统调度时，还会考虑其他因素，因而会计算出一个叫进程动态优先级的东西，根据此来实施调度。因为，不仅要考虑静态优先级，也要考虑进程的属性。例如如果进程属于交互式进程，那么可以适当的调高它的优先级，使得界面反应地更加迅速，从而使用户得到更好的体验。Linux2.6 在这方面有了较大的提高。Linux2.6认为，交互式进程可以从平均睡眠时间这样一个measurement进行判断。进程过去的睡眠时间越多，则越有可能属于交互式进程。则系统调度时，会给该进程更多的奖励（bonus），以便该进程有更多的机会能够执行。奖励（bonus）从0到10不等。

　　系统会严格按照动态优先级高低的顺序安排进程执行。动态优先级高的进程进入非运行状态，或者时间片消耗完毕才会轮到动态优先级较低的进程执行。动态优先级的计算主要考虑两个因素：静态优先级，进程的平均睡眠时间也即bonus。计算公式如下，

​     dynamic_prio = max (100, min (static_prio - bonus + 5, 139))

　　在调度时，Linux2.6 使用了一个小小的trick，就是算法中经典的空间换时间的思想[**还没对照源码确认**]，使得计算最优进程能够在O(1)的时间内完成。

 　**为什么根据睡眠和运行时间确定奖惩分数是合理的**

　　睡眠和CPU耗时反应了进程IO密集和CPU密集两大瞬时特点，不同时期，一个进程可能即是CPU密集型也是IO密集型进程。对于表现为IO密集的进程，应该经常运行，但每次时间片不要太长。对于表现为CPU密集的进程，CPU不应该让其经常运行，但每次运行时间片要长。交互进程为例，假如之前其其大部分时间在于等待CPU，这时为了调高相应速度，就需要增加奖励分。另一方面，如果此进程总是耗尽每次分配给它的时间片，为了对其他进程公平，就要增加这个进程的惩罚分数。**可以参考CFS的virtutime机制.**

**现代方法CFS**

　　不再单纯依靠进程优先级绝对值，而是参考其绝对值，综合考虑所有进程的时间，给出当前调度时间单位内其应有的权重，也就是，每个进程的权重X单位时间=应获cpu时间，但是这个应得的cpu时间不应太小（假设阈值为1ms），否则会因为切换得不偿失。但是，当进程足够多时候，肯定有很多不同权重的进程获得相同的时间——最低阈值1ms，所以，CFS只是近似完全公平。

### 一般的进程调度算法

![1592649179130](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592649179130.png)



![1592649797846](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592649797846.png)



#### 批处理系统

- 先来先服务
  - 一个链表表示一个队列，新作业或者由阻塞状态变为运行状态的进程加到队列末尾即可。
  - 优点：有利于长作业以及CPU繁忙的作业 
  - 缺点：不利于短作业以及I/O繁忙的作业 

最短作业优先

- 对预计执行时间短的作业（进程）优先分派处理机.通常后来的短作业不抢先正在执行的作业. 

- 优点：

  比FCFS改善平均周转时间和平均带权周转时间，缩短作业的等待时间；

  提高系统的吞吐量；

- 缺点：

  对长作业非常不利，可能长时间得不到执行；

  未能依据作业的紧迫程度来划分执行的优先级；

  难以准确估计作业（进程）的执行时间，从而影响调度性能。

#### 交互式系统

round robin

- 一个链表表示一个队列，新作业、由阻塞状态变为运行状态、时间片用完的进程加到队列末尾即可。
- 优点：经典的做法
- 缺点：时间片设置过短会导致过多的进程切换，降低了cpu效率；时间片设置过长又可能引起对短的交互请求响应时间变长。 

优先级调度

- 非抢占式优先权算法 （批处理）
- 抢占式优先权调度算法 （交互式）参考上述linux系统的调用算法
- 

## 进程间通信的方式和区别



## linux内核同步技术

### 为什么要同步

![1592706338117](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592706338117.png)

还是竞争条件和临界区问题，几个线程同时访问同一个临界区

![1592706412179](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592706412179.png)

![1592706446578](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592706446578.png)

![1592706550385](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592706550385.png)

### 同步方法

#### 原子操作

- 原子整数操作：atomic_t类型 和 一些对应的原子操作函数
- ![1592713010030](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592713010030.png)
- 像int data++这种操作，无需加锁，直接使用原子操作，加锁开销太大了。

#### 自旋锁

![1592715684115](C:\Users\mycan\AppData\Local\Temp\1592715684115.png)

![1592715693885](C:\Users\mycan\AppData\Local\Temp\1592715693885.png)

![1592715707604](C:\Users\mycan\AppData\Local\Temp\1592715707604.png)

![1592716078571](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592716078571.png)

#### 读写自旋锁

- 读写自旋锁是为了增加内核的并发能力。
- 我们知道在共享资源的并发程序中，对共享数据的写操作是互斥的，但是只要没有写操作，对共享数据的并发读操作是安全的。
- 一个或多个读任务可以并发的持有读者锁，用于写的锁最多只能被一个写任务持有。
- 有时把读写锁也叫共享锁和排他锁。
- 下面这一点很重要。读会延迟写，对读友好，适用读侧重场合

![1592721735888](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592721735888.png)

#### 顺序锁

- linux 2.6中引入顺序锁，与自旋锁类似，不过写者赋予了较高的优先级，在《深入理解linux内核》中说到，即使读者在读的时候也允许写者继续运行。
- 顺序锁，支持读并发，写写/读写间互斥，写会延迟读，对写友好，适用写侧重场合；
- 优点：写者永远不会等待（除非另一个写着在写）
- 缺点：有些时候读者不得不反复多次读相同的数据，直到它获得有效的副本。

#### 信号量

所谓“**进程上下文**”，就是一个进程在执行的时候，CPU的所有寄存器中的值、进程的状态以及堆栈上的内容，当内核需要切换到另一个进程时，它需要保存当前进程的所有状态，即保存当前进程的进程上下文，以便再次执行该进程时，能够恢复切换时的状态，继续执行。

所谓“**中断上下文**”，就是硬件通过触发信号，导致内核调用中断处理程序，进入内核空间。这个过程中，硬件的一些变量和参数也要传递给内核，内核通过这些参数进行中断处理。中断上下文，其实也可以看作就是硬件传递过来的这些参数和内核需要保存的一些其他环境（主要是当前被中断的进程环境）。



![1592725083948](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592725083948.png)

**信号量的特点：**

![1592725720566](C:/Users/mycan/Documents/CppGuild/linux%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/picture/1592725720566.png)

![1592725112553](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592725112553.png)

#### 读写信号量

![1592725346236](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592725346236.png)

![1592725332409](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592725332409.png)

**看到这里我想起了陈硕在他的书中说，尽量不要用读写锁和信号量**，那用什么呢，

#### 互斥体

![1592726923701](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592726923701.png)

![1592726946401](C:\Users\mycan\AppData\Local\Temp\1592726946401.png)



![1592727069737](C:\Users\mycan\AppData\Local\Temp\1592727069737.png)

![1592727111112](C:\Users\mycan\AppData\Local\Temp\1592727111112.png)

![1592727164696](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592727164696.png)

#### 禁止抢占

内核是抢占性的；可能随时被停下来。因此一个任务与被抢占的任务可能会在同一个临界区内运行(新调度的任务可能访问被切换的同一个变量)。内核抢占代码使用自旋锁作为非抢占区域的标记。一个自旋锁被持有，内核便不能进行抢占。

可以通过`preempt_disable()`禁止内核抢占。直到`preempt_enable()`被启用之后才能重新启用。

![1592727269579](C:\Users\mycan\Documents\CppGuild\linux操作系统\picture\1592727269579.png)

### 锁的缺点

- 但锁的并行可扩展性很差，无法充分发挥多核的性能优势。
- 锁的粒度太粗会限制扩展性，粒度太细会导致巨大的系统开销，而且设计难度大，容易造成死锁。
- 除了并发可扩展性差和死锁外，锁还会引入很多其他问题，如[锁惊群](https://blog.csdn.net/aazhzhu/article/details/89967346)、活锁、饥饿、不公平锁、优先级反转等。不过也有一些技术手段或指导原则能解决或减轻这些问题的风险。
- 按统一的顺序使用锁（锁的层次），解决死锁问题；
- 指数后退，解决活锁/饥饿问题；
- 范围锁（树状锁），解决锁惊群问题；
- 优先级继承，解决优先级反转问题；

## 虚拟内存机制的作用







## 缓存的作用以及缓存替换算法

## 虚拟文件系统



 

 

 

 unique_lock和lock_guard最大的不同是unique_lock不需要始终拥有关联的mutex，而lock_guard始终拥有mutex。std::unique_lock 与std::lock_guard都能实现自动加锁与解锁功能，但是std::unique_lock要比std::lock_guard更灵活，但是更灵活的代价是占用空间相对更大一点且相对更慢一点。std::unique_lock相对std::lock_guard更灵活的地方在于在等待中的线程如果在等待期间需要解锁mutex，并在之后重新将其锁定。而std::lock_guard却不具备这样的功能。





lock_guard和unique_lock都是RAII机制下的锁，即依靠对象的创建和销毁也就是其生命周期来自动实现一些逻辑，而这两个对象就是在创建时自动加锁，在销毁时自动解锁。所以如果仅仅是依靠对象生命周期实现加解锁的话，两者是相同的，都可以用，因跟生命周期有关，所以有时会用花括号指定其生命周期。但lock_guard的功能仅限于此。unique_lock是对lock_guard的扩展，允许在生命周期内再调用lock和unlock来加解锁以切换锁的状态。

根据linux下条件变量的机制，condition_variable在wait成员函数内部会先调用参数unique_lock的unlock临时解锁，让出锁的拥有权（以让其它线程获得该锁使用权加锁，改变条件，解锁），然后自己等待notify信号，等到之后，再调用参数unique_lock的lock加锁，处理相关逻辑，最后unique_lock对象销毁时自动解锁。





 

 

 

 

 





 

 

 

 

