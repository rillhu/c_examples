# c\_examples
some usefull examples for c deep learning

## c\_va\_arg\_test\_01： 关于c语言中，可变参数长度函数的一个简单用例。

### 参考了下面链接中的例子，修正了其中的错误，在C-FREE5.0上便宜运行通过。

http://www.cnblogs.com/hanyonglu/archive/2011/05/07/2039916.html

#### 要点摘要如下：
函数参数是以数据结构:栈的形式存取,从右至左入栈。

首先是参数的内存存放格式：
参数存放在内存的堆栈段中，在执行函数的时候，从最后一个开始入栈。因此栈底高地址，栈顶低地址，举个例子如下：
    void func(int x, float y, char z);
　　那么，调用函数的时候，实参` char z` 先进栈，然后是 `float y`，最后是 `int x`，因此在内存中变量的存放次序是` x->y->z`，因此，从理论上说，我们只要探测到任意一个变量的地址，并且知道其他变量的类型，通过指针移位运算，则总可以顺藤摸瓜找到其他的输入变量。

下面是` <stdarg.h> `里面重要的几个宏定义如下：
typedef char* va_list;
    void va_start ( va_list ap, prev_param ); /* ANSI version */
    type va_arg ( va_list ap, type ); 
    void va_end ( va_list ap ); 
`va_list` 是一个字符指针，可以理解为指向当前参数的一个指针，取参必须通过这个指针进行。


- <Step 1> 在调用参数表之前，定义一个 `va_list` 类型的变量，(假设`va_list` 类型变量被定义为ap)；

- <Step 2> 然后应该对ap 进行初始化，让它指向可变参数表里面的第一个参数，这是通过 `va_start` 来实现的，第一个参数是 `ap` 本身，第二个参数是在变参表前面紧挨着的一个变量,即“...”之前的那个参数；

- <Step 3> 然后是获取参数，调用`va_arg`，它的第一个参数是`ap`，第二个参数是要获取的参数的指定类型，然后返回这个指定类型的值，并且把 `ap` 的位置指向变参表的下一个变量位置；

- <Step 4> 获取所有的参数之后，我们有必要将这个 `ap `指针关掉，以免发生危险，方法是调用 `va_end`，他是输入的参数 `ap` 置为 `NULL`，应该养成获取完参数表之后关闭指针的习惯。说白了，就是让我们的程序具有健壮性。通常`va_start`和`va_end`是成对出现。

### 更高级的用法可以参考下面的链接：
http://www.cppblog.com/qiujian5628/archive/2008/01/21/41562.html

#### 要点摘要如下：
在编程中应该注意的问题和解决办法：


1. 虽然可以通过在堆栈中遍历参数列表来读出所有的可变参数,但是由于不知道可变参数有多少个,什么时候应该结束遍历,如果在堆栈中遍历太多,那么很可能读取一些无效的数据.
解决办法:

	a.可以在第一个起始参数中指定参数个数,那么就可以在循环还中读取所有的可变参数;

	b.定义一个结束标记,在调用函数的时候,在最后一个参数中传递这个标记,这样在遍历可变参数的时候,可以根据这个标记结束可变参数的遍历;

2. 虽然可以根据上面两个办法解决读取参数个数的问题,但是如果参数类型都是不定的,该怎么办,如果不知道参数的类型,即使读到了参数也没有办法进行处理.
解决办法:

	可以自定义一些可能出现的参数类型,这样在可变参数列表中,可以可变参数列表中的那类型,然后根据类型,读取可变参数值,并进行准确地转换.
	
	传递参数的时候可以这样传递:参数数目,可变参数类型1,可变参数值1,可变参数类型2,可变参数值2,....


## c\_cJSON_01

cJSON的使用，例子中做了生成JSON字符串和解析JSON字符串代码。参考了下面链接中cJSON例子：

https://github.com/hxy513696765/ESP8266-Weather-Station

以及：
http://blog.csdn.net/xukai871105/article/details/17094113和
http://blog.csdn.net/xukai871105/article/details/33013455


## socket_gethostbyname

Socket 编程用例之一，展示如何使用gethostbyname. MAC/ubuntu系统下编译测试通过。

`bogon:socket_gethostbyname hongfeihu$ make clean`

rm -rf main main.o

`bogon:socket_gethostbyname hongfeihu$ make`

gcc -Wall -std=gnu99   -c -o main.o main.c

gcc -o main main.o

`bogon:socket_gethostbyname hongfeihu$ ./main www.baidu.com`

official hostname:www.a.shifen.com

 alias:www.baidu.com

 address:61.135.169.121

 address:61.135.169.125

 h_length:4

##socket_getaddrinfo
Socket 编程用例之一，getaddrinfo. MAC/ubuntu系统下编译测试通过。

    getaddrinfo$ make

gcc -Wall -std=gnu99   -c -o main.o main.c

gcc -o main main.o

hongfei@hongfei-xps:/mnt/c/Users/hongf/Documents/03_Git_local/C-Examples-master/

    socket_getaddrinfo$ ./main www.sina.xom

getaddrinfo: Name or service not known

    getaddrinfo$ ./main www.sina.com

IP: 218.30.66.248



## 数据结构的两个例子

graph和biTree