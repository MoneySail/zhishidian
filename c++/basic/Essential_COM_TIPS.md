Essential_COM
=============

COM组件的必要性分析
-------------------
　　重用性一直是面向对象的主要动机之一，但是事实上，要编写一个很容易被重用的C++类  
也十分的困难。C++领域中，除了设计和开发重用的许多障碍，在运行时也有大量的障碍，使  
C++对象模型不能够成为"构建可重用软件组件"的理想底层基础。这些障碍主要来自C++本身  
所假设的编译和链接模型。COM组件允许多个独立开发的二进制结构组件能够动态，有效地  
组成一个复合系统。  

接口
----

# 存在意义 #
　　把接口跟实现分开的动机，是要把对象内部工作的细节(对客户而言)都隐藏起来。这条基本  
的原则提供了一层间接性，允许实现类内部的数据成员的数量和顺序都可以发生变化，但是客户  
程序都无需重新编译，这条原则也允许客户在运行时候能够查询对象以便实现对象的扩展功能。  
但客户不需要重新编译。这条原则也允许客户在运行时询问对象以便发现对象的扩展功能。最后  
这条原则也允许DLL和客户不必使用同样的C++编译器。

# 基本构成 #
　　1.所有COM接口的VTBL都要从三个入口QueryIneterface, AddRef和Release开始。与接口相关  
的方法都有对应的vtbl入口，但是它们位于这三个公共的入口之后.  

# 智能指针 #
　　1.在赋值过程中，正确地处理AddRef/Release调用  
　　2.在析构函数中自动释放接口，从而降低资源泄露的可能性，以及改进异常的安全性  
　　3.通过C++类型系统来简化对QueryInterface的调用  
　　4.可以透明地将遗留代码中的纯接口指针(raw interface pointer)替换掉，而不会牺牲  
　　程序的正确性
