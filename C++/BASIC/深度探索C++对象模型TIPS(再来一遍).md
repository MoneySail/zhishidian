C++对象模型的概念
=================

# 基本概念 #

　　1.语言中直接支持面向对象程序设计的部分  
　　2.对于各种支持的底层实现机制  

# 说明 #
　　1.C++ class的完整的virtual functions在编译时期就固定下来了  
　　程序员没有办法在执行期动态增加或取代其中的某一个。这使得  
　　虚拟调用得以有快速的dispatch结果，付出的成本是执行期的弹性.  

　　2.目前所有编译器对于virtual function的实现法都是使用各个class   
　　专属的virtual table，大小固定，并且都在程序执行前就构造好了  

# C++对象模型 #
　　1.每个Class产生出一堆指向Virtual functions的指针，放在表格之后  
　　，这个表格被称为virtual table(vtbl)  
　　2.每个class object被添加一个指针，指向相关的virtual table。通常  
　　这个指针称作为vptr, vptr的设定与重置都由每一个class的构造函数  
　　，析构函数，和拷贝赋值运算符自动完成。每一个class关联的tpye_info  
　　object(用以支持runtime type indentification RTTI)也经由virtual table  
　　被指出来，通常是放在表格的第一个slot处。

# C++ class object 内存需求 #
　　1.nostatic data members的总和大小  
　　2.加上任何由于alignment的需求而填补的上去的空间(可能存在于members之间)  
　　，也可能存在于集合体边界。  
　　3.加上virtual而由内部产生的任何额外负担  

# 虚拟继承 #
　　1.实现模型1 => 如Microsoft编译器引入的virtual base class table, 每一个class  
　　object 如果有一个或者多个virtual base classes，就会由编译器安插一个指针，指向  
　　virtual base class table, 至于真正的virtual base class指针，当然是被放在该表格  
　　中。
　　2.实现模型2 => vbtl(virtual function table)中放置virtual base class的offset  
　　(而不是地址), 这种做法是C++之父 Bjarne比较喜欢的方法.  

　　TIPS => 一般而言，virtual base class最有效的一种运用形式是：一个抽象的virtual  
　　base class, 没有任何data members。  

# C++ Static函数 #
　　不能直接存储Nonestaic数据，不能被声明为const  

# 内联函数 #
　　1.在类的内部定义的函数自动默认为内联函数。  
　　2.内联函数是在编译时期展开，而虚函数的特性是运行时才动态联编，所以不能定义内联函数为虚函数  
　　3.构造函数是用来创建一个新的对象，而虚函数的运行时是建立在对象的基础上的，在构造函数执行时  
　　对象尚未形成，所以不能将构造函数定义为虚函数。  
　　4.静态成员函数属于某一个类而非某一对象，没有this指针，它无法进行对象的判别。  
　　5.在类的内部定义的函数自动默认为内联函数。  

