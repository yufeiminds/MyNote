.. syntax-java:

Java
================================

基本类型
----------

大家基本相同，字符串只支持 ``" "``
强制类型转换： ``type(x)`` ，eg. ``int(x)``

强类型，eg. 定义整型数组建议使用::

    int[] a = new int[100];


控制逻辑
--------

条件
^^^^

支持三元运算符

.. code-block:: java

    if (true) {
        data = x;
    } else {
        data = y;
    }

    data = true ? x : y;

分支选择
^^^^^^^^

条件多路选择使用 ``else if`` ，支持 ``switch``

.. code-block:: java

    switch(i) {
        case 0: statement; break;
        case 1: statement; break;
        case 2: statement; break;
        default: statement;
    }


循环(迭代)
^^^^^^^^^^^

for

.. code-block:: java

    for (int i = 0; i < 10; i ++)
        statement

while

.. code-block:: java

    while (bool) // true时进入
        statement

    do {
        statement
    } while (bool) // true时退出

增强型 For

.. code-block:: java

    int[] arr = int arr[10];

    // ...

    for (int i: arr) {
        // i
    }

OOP
---

包导入
^^^^^^

包分为三个层级： ``package`` 是一个库的基本组织方式， ``文件`` 是存放所编写类的地方，一个文件只能有一个 ``public`` 类，下一小节会讲解 ``public`` 类，类是程序接口的基本单位，也是最终调用的复合类型单元。

.. note:: 这几个术语我无法弄得准确，引用《Thinking in Java》，package对应的是[Library Unit，程序库单元]，原文件对应[Compliation Unit，编译单元或Translation Unit，转译单元]，有知道的同学请不吝赐教。

类定义
^^^^^^

权限修饰符分为public（可被任意package引入），protect（可被子类和同package类引入），friendly（默认权限，可被同package引入），private（可被当前类引入）。

每一个文件只能有一个public类，如果有public类，类名必须与文件名完全相同，类初始化自动调用类同名构造函数。

被GC（垃圾回收机制）回收时，自动调用 ``finalize`` 方法，通常用于回收由非Java调用分配的内存，清理动作请不要依赖垃圾回收机制（垃圾回收详情请参考 :ref:`语言特性参考<语言特性参考>` ）。

每一个java文件在命令行运行时，进入文件同名类（包括非public类）的main方法执行，可用于编写单元测试。

类中，``this`` 关键字代表当前类。

类继承
^^^^^^

类继承使用 ``extends`` 关键字，在子类中 ``super`` 代表基类，``this`` 代表当前类。基类如果有构造参数，在子类构造函数最开始的地方调用基类构造函数 ``super(arg)`` 。

方法绑定到实例分为 ``early binding`` （编译器已绑定）， ``late binding`` （运行时绑定）， ``dynamic binding`` （动态绑定），类继承自动采用 ``late binding`` 方式，即类初始化时可赋值给基类，运行时调用的是子类的方法。

.. note:: 各种中译本的术语太难统一了，后面类似的术语都采用原文标识。

接口
^^^^

Java把接口和实现分离这条原则发挥到了极致，创造出了一种完全定义化的一种抽象类， ``interface`` ，所有 ``interface`` 中的属性都是 ``final static`` 的，方法都是没有定义的。区别于 ``abstract`` 抽象类修饰的方法是可以有定义的。

Java类是单继承，规避C++中多继承带来的问题。但一个类可以实现多个接口，因为接口仅仅是一个定义，所以接口也可以多继承，继承的类也是接口。

接口实现使用 ``implements`` 关键字，当实现没有完全 ``override`` 接口方法的定义时，编译时会报错。

.. note:: ``final`` 和 ``static`` 的定义请参考 :ref:`特殊特性<#final>`

例子
^^^^

.. code-block:: bash

    .
    ├── CodeSnippets.class
    ├── CodeSnippets.java
    └── com
        └── thxminds
            ├── MaxNumInterface.java
            └── RectInterface.java

.. code-block:: java

    package com.thxminds;

    public interface RectInterface {
        public double area();
    }

.. code-block:: java

    import com.thxminds.*;
    import java.io.*;

    class Rect implements RectInterface {
        double length;
        double width;

        Rect(double length, double width) {
            this.length = length;
            this.width = width;
        }

        public double area() {
            return this.length * this.width;
        }
    }

    class Cube extends Rect {
        double height;
        double rd = 1;

        Cube(double length, double width, double height, double rd) {
            super(length, width);
            this.height = height;
            this.rd = rd;
        }

        Cube(double length, double width, double height) {
            super(length, width);
            this.height = height;
        }

        public double volume() {
            return this.area() * this.height;
        }

        public double weight() {
            return this.volume() * this.rd;
        }
    }

.. note:: 
    *多态、覆盖、重载的区别*

    多态是面向对象的一个重要特征，是指一个对象可以根据环境上下文确定自己的类型，相对它们在继承链中的位置，称之为向上转型或者向下转型。

    覆盖是指子类实现直接重写其方法。

    方法重载是指类方法可以接收多种不同参数，对不同的输入作出不同的响应。

数据结构
--------

Java常用的数据结构在 ``java.util`` 里，经常用到的包括:

- List
  + LinkedList

- Map
  + HashMap

- Queue
  + Deque

- Set
  + HashSet

抽象到Collection接口中，其中add, remove, contains都有all方法，接受一个Collections, eg. ``addall`` ， 下表并未包括Stream(流)等，详情请见: `Sun Java技术文档 <http://docs.oracle.com/javase/8/docs/api/>`_

其中 ``List`` 、 ``Set`` 都是 ``Collection`` 的接口实现，拥有如下公共方法。

=================== =========================== =====================
返回值              方法                        功能
=================== =========================== =====================
boolean 	        add(E e)                    添加元素
boolean 	        contains(Object o)          判断元素是否在集合中
boolean 	        remove(Object o)            移除元素
int 	            size()                      集合大小
void 	            clear()                     清空集合
boolean 	        isEmpty()                   集合判空
boolean 	        equals(Object o)            ?
int 	            hashCode()                  获取集合Hash
Iterator<E>         iterator()                  获取集合迭代器
boolean 	        retainAll(Collection<?> c)  仅保留元素
Object[]            toArray()                   转换为数组
=================== =========================== =====================

Map特有 ``get`` , ``put`` 方法，用来获取和设置元素，Map可使用 ``keySet`` 转换为 ``Set`` ， ``values`` 转换为 ``List``

``iterator`` 可以返回迭代器，使用迭代器 ``next`` 方法进行迭代，eg:

.. code-block:: java

    Iterator i = c.iterator();
    while(i.hasNext()) {
        System.out.println(i.next());
    }

特殊特性
--------

final
^^^^^^

符号不变特性， ``final`` 修饰的变量名称不能引用其他变量（使用前必须赋初值）， ``final static`` 修饰的变量其值也无法改变，同时编译器可以将 ``final`` 函数內联优化。 ``private`` 默认是 ``final`` 的。
