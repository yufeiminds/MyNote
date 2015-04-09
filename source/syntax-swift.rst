.. syntax-swift:

Swift
===========================

基本类型
------------

Swift是强类型语言， ``let`` 和 ``var`` 有个自动类型推导，类似于C++里面的 ``auto`` ，实际上在编译器依然有强类型约束。

Swift的基本概念， ``protocal`` 被称为 ``协议`` ，类似于Java中的 ``interface`` 和C++中的虚基类。

类型声明:

.. code-block:: swift

    var a: String = "asd" // 变量
    let b: Int = 10

    或直接

    var a = "asd"
    let b = 10

可选值:

.. code-block:: swift

    var a: String?  // 可选值，默认为nil
    var b: String? = "asd"  // 可选值"asd"
    println(b)  // 打印Optional("asd")
    println(b!) // 打印 "asd"

基本数据结构声明:

.. code-block:: swift

    var a = [String]() // 空数组
    let b = [1, 2, 3]

    var c = (1, 2, "3") // 元组
    var ca, cb, _ = c   // 元组解包，ca = 1，cb = 2，后面的元素丢弃

    var d = [
        "a": 1, // key可以是数字
    ] // 字典 key-value 对

类型扩展:

.. code-block:: swift

    extension Int {
    
    }

.. note:: 来自于 猫 仁波切 的博客

函数
^^^^

函数声明:

.. code-block:: swift

    func count(arg1: String) -> Int {
        /* Function body */
    }

闭包:

我的理解是，Swift闭包等同于绝大部分编程语言中的匿名函数（lambda表达式）。这里由一对花括号 ``{}`` 定义。

.. code-block:: swift

    print(sorted(a, {
        (a1: Int, a2: Int) -> Bool in
        return a1 > a2
    }))
    print(sorted(a, {a1, a2 in return a1 > a2}))
    print(sorted(a, {$0 > $1}))

类
^^

类声明:

.. code-block:: swift

    class Base {
        init() {
            /* Init method body */
        }

        func m() -> Int {
            /* Method body */
        }
    }

    class Subclass: Base {
        init() {
            super.init()
        }

        override func m() -> Int {
            /* Overrided method body */
        }
    }
