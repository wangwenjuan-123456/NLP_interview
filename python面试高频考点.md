## 一、数据结构

|              | 特点                                                         |                              增                              | 删                                                           | 查找                                                         | 应用场景                                                     |
| ------------ | ------------------------------------------------------------ | :----------------------------------------------------------: | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 列表         | 列表元素可变<br />可查看索引有序                             |        append() <br /> Extend()<br />Insert(idx,val)         | Pop(idx) 删除并返回指定索引的元素 <br />Remove:按值删除找到的第一个元素 | Index(元素）返回 对应索引<br /> 某元素 in 列表名：判断某元素是否在列表内 |                                                              |
| 元组         | 元组与列表类似，不同之处在于元组的元素不能修改。<br />空的tuple可以记为()，若只有一个元素的tuple记为(1,) |                                                              |                                                              |                                                              | 字符串格式化需要使用元组 函数返回多个返回值时返回的是元组类型 一些内置函数的返回值是元组类型 |
| 字典         | 键：任何不可变类型，不能进行修改<br />键不可重复，值可重复   | 变量名[key]=value 通过 key 添加 value 值，如果 key 存在则覆盖 setdefault(key,default_value) 指定 key 和 value,如果 key 存在则覆盖 | pop 弹出，返回并删除指定键对应的值 <br />popitem 随机弹出一个键值元组， | get 以键取值，如果指定键不存在，默认返回 None,可以指定返回内容 |                                                              |
| 集合去重场景 | 集合不能被切片，不能被索引，除了做集合运算之外，集合元素可以被添加和删除。 |                          add(elem)                           | remove(elem)<br />pop()<br />clear()                         |                                                              |                                                              |

### list vs dict

和list比较，dict有以下几个特点：

1. 查找和插入的速度极快，不会随着key的增加而变慢；
2. 需要占用大量的内存，内存浪费多。

而list相反：

1. 查找和插入的时间随着元素的增加而增加；
2. 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。

#### 列表VS数组

列表里元素类型可以不同，数组必须元素类型相同

列表长度可变，数组须一开始就申明大小

| 存储类别     | 顺序存储结构                                     | 单链表                                                 |
| :----------- | :----------------------------------------------- | :----------------------------------------------------- |
| 存储分配方式 | 用一段连续的存储单元依次存储线性表的数据元素     | 采用链式存储结构，用一组任意的存储单元存放线性表的元素 |
| 时间性能     | 查找O（1）、插入和删除O（n）                     | 查找O（n）、插入和删除O（1）                           |
| 空间性能     | 需要预分配存储空间，分大了浪费，小了容易发生上溢 | 不需要分配存储空间，只要有就可以分配，元素个数不受限制 |

### 栈VS队列

数组、链表等是作为数据存储工具，适用于数据库应用中做数据记录，但栈与队列不是完全的数据存储工具，他们的生命周期比较短，在程序操作执行期间他们才被创建，在完成任务后就被销毁。

|      |                                        |                                                     |                                                          |      |
| ---- | -------------------------------------- | --------------------------------------------------- | -------------------------------------------------------- | ---- |
| 栈   | 先进后出<br />场景：模拟二叉树深度遍历 | 栈顶添加元素 append o(1)<br />栈顶删除元素 pop o(1) |                                                          |      |
| 队列 | 先进先出<br />场景：模拟二叉树层次遍历 | 对头删除<br />队尾添加元素                          | 双端队列<br />appendleft() append()<br />popleft() pop() |      |
|      |                                        |                                                     |                                                          |      |



## 二、可变对象 VS 不可变

可变对象有list,dict.不可变类型.(开辟新的内存有string，number,tuple）

当进行修改操作时，可变类型传递的是内存中的地址，直接修改内存中的值，并没有开辟新的内存。可变参数是引用传递：比如像列表，字典这样的对象是通过引用传递、和C语言里面的用指针传递数组很相似，可变对象能在函数内部改变。

而不可变类型被改变时，原内存地址中的值并没有改变，而是开辟一块新的内存，将原地址中的值复制过去，对这块新开辟的内存中的值进行操作。不可变参数用值传递：像整数和字符串这样的不可变对象，是通过拷贝进行传递的，因为你无论如何都不可能在原处改变不可变对象。

以int类型为例:实际上 i += 1 并不是真的在原有的int对象上+1，而是重新创建一个value为6的int对象，i引用自这个新的对象。不可变数据类型在第一次声明赋值声明的时候, 会在内存中开辟一块空间, 用来存放这个变量被赋的值, 而这个变量实际上存储的并不是被赋予的这个值, 而是存放这个值所在空间的内存地址, 通过这个地址, 变量就可以在内存中取出数据了. 所谓不可变就是说, 我们不能改变这个数据在内存中的值, 所以当我们改变这个变量的赋值时, 只是在内存中重新开辟了一块空间, 将这一条新的数据存放在这一个新的内存地址里, 而原来的那个变量就不在引用原数据的内存地址而转为引用新数据的内存地址了,相当于改变了变量指向的内存地址.

## 三、迭代器VS生成器

可迭代对象：使用 iter 内置函数可以获取迭代器的对象。即要么对象实现了能返回迭代器的 iter 方法，要么对象实现了 getitem 方法，而且其参数是从零开始的索引。接下来我们分别用这两种方法来实现

标准的迭代器接口有两个方法：

____next____  :返回下一个可用的元素，没有的话抛出一个StopIteration异常

____iter____  : 返回self,迭代器本身

```
sentence ="i wanna go out and play"
for word in sentence:#
    print(word)#  
   
class iter_selfmade:
    def __init__(self,text):
        self.text=text
        self.sub_text=text.split(" ")
    def __iter__(self):
        return SentenceIterator(self.sub_text)
class SentenceIterator:
    def __init__(self,text):
        self.text=text
        self.idx=0
    def __next__(self):
        try:
            word=self.text[self.idx]
        except:
            raise StopIteration()
        self.idx+=1
        return word
    def __iter__(self):
        return self
sen_iter=iter_selfmade(sentence)
for w in sen_iter:
    print(w)
```

```
i
wanna
go
out
and
play
```

```
class iter_selfmade:
    def __init__(self,text):
        self.text=text
        self.sub_text=text.split(" ")
    def __getitem__(self, idx):
        return self.sub_text[idx]

sen_iter=iter_selfmade(sentence)
for w in sen_iter:
    print(w)
```

实现了迭代器协议的对象（如何实现：对象内部定义一个__iter__()方法），python的内部工具（如for循环，sum，min，max函数等)使用迭代器协议访问对象等。迭代器协议是指：对象必须提供一个next方法，执行该方法要么返回迭代中的下一项，要么就引起一个StopIteration异常，以终止迭代 （只能往后走不能往前退）

for 循环机制
for循环的本质：循环所有对象，全都是使用迭代器协议。
列表，字符串，元组，字典，集合，文件对象等本质上来说都不是可迭代对象，在使用for循环的时候内部是先调用他们内部的iter方法，使他们变成了可迭代对象，然后在使用可迭代对象的next方法依次循环元素，当元素循环完时，会触发StopIteration异常，for循环会捕捉到这种异常，终止迭代

## 四、生成器

我们知道 列表解析式有很多优点很多，比如编写简单，但是他是一次性生成整个列表。如果整个列表非常大，这对内存也同样会造成很大压力，**想要实现内存的节约，可以将列表解析式转换为生成器表达式。现在我们不必创建完整的list，一边循环一边计算，从而节省大量的空间。最佳服用方式：想得到大量数据，又想占用内存少

创建生成器两种方式：

把一个列表生成式的`[]`改成`()`，就创建了一个generator

如果一个函数中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator。调用函数就是创建了一个生成器（generator）对象。

每次循环的时候，生成器函数都会在yield处产生一个值，并将其返回给调用者，即for循环。然后在yield处保存内部状态，并挂起中断退出。在下一轮迭代调用时，**从yield的地方继续执行**，并且沿用上一轮的函数内部变量的状态，直到内部循环过程结束。yield就是保存当前程序执行状态，generator每次计算需要上一次计算结果，所以用yield,否则一return，上次计算结果就没了调用。

　generator function产生的generator与普通的function有什么区别呢

　　（1）function每次都是从第一行开始运行，而generator从上一次yield开始的地方运行

　　（2）function调用一次返回一个（一组）值，而generator可以多次返回

（3）function可以被无数次重复调用，而一个generator实例在yield最后一个值 或者return之后就不能继续调用了

## 四、Python作用域

简单说就是一个变量的命名空间。代码中变量被赋值的位置，就决定了哪些范围的对象可以访问这个变量，这个范围就是变量的作用域。
Python的变量名解析机制也称为 LEGB 法则：本地作用域（Local）→当前作用域被嵌入的本地作用域（Enclosing locals）→全局/模块作用域（Global）→内置作用域（Built-in）

在L中修改nON-L:可在L内 加上global(L中修改G)，nonlocal(L中修改E)

##### L(local)局部作用域

局部变量：，即在函数中定义的变量。每当函数被调用时都会创建一个新的局部作用域。在函数内部的变量声明，除非特别的声明为全局变量，否则均默认为局部变量。有些情况需要在函数内部定义全局变量，这时可以使用global关键字来声明变量的作用域为全局。局部变量域就像一个 栈，仅仅是暂时的存在，依赖创建该局部作用域的函数是否处于活动的状态。所以，一般建议尽量少定义全局变量，因为全局变量在模块文件运行的过程中会一直存在，占用内存空间。
注意：如果需要在函数内部对全局变量赋值，需要在函数内部通过global语句声明该变量为全局变量。

#### E(enclosing)嵌套作用域

E是定义在此函数的上一层父级函数的局部作用域，主要是为了实现Python的闭包。

#### G(global)全局作用域

即在模块层次中定义的变量，每一个模块都是一个全局作用域。也就是说，在模块文件顶层声明的变量具有全局作用域，从外部开来，模块的全局变量就是一个模块对象的属性。
注意：全局作用域的作用范围仅限于单个模块文件内

#### B(built-in)内置作用域

系统内固定模块里定义的变量，如预定义在**builtin** 模块内的变量。

```
例1
def test_scopt():
    a = 200
    print(a)
    def func():
       print(a)
       func()#这里的变量a在E中绑定了内存对象200，为函数func()引入了一个新的变量
a = 100
test_scopt()
print(a)
输出为
200
200
100
例2
a = 100
def test_scopt():
 		print(a)
    a=10  
test_scopt()
print(a)
输出
UnboundLocalError: local variable 'a' referenced before assignment
例3
a = 100
def test_scopt():
 		print(a)
   # a=10  #
test_scopt()
print(a)
输出
100
100
```

希望在L中修改G中的变量，使用global/nonlocal关键字

## 五、类方法VS 实例方法VS静态方法

实例方法，必须要创建实例才能调用。里面有self关键字，有初始化函数必须对初始化函数进行传参。

类方法，可以直接类名.方法名直接调用，也可以创建实例调用。里面有cls关键字，直接类名.方法名，可以绕过实例方法的初始化函数，类方法不能访问实例属性。

静态方法，可以直接类名.方法名直接调用，也可以创建实例调用。没有关键字，就像调用函数一样方便，调用时，直接类名.方法名，可以绕过实例方法的初始化函数，静态方法不能访问实例属性。

## 六、闭包 和装饰器

**闭包**是一种组织代码的结构，作用：用于装饰器的实现，提高了代码的可重复使用性。

当一个内嵌函数引用其外部作作用域的变量,我们就会得到一个闭包. 总结一下,创建一个闭包必须满足以下几点:

必须有一个内嵌函数

内嵌函数必须引用外部函数中的变量

外部函数的返回值必须是内嵌函数

    def 外层函数(参数):
        def 内层函数():
            print("内层函数执行", 参数)
    return 内层函数

内层函数的引用 = 外层函数("传入参数")
内层函数的引用()

```
def func(a, b): *实现一个 求一点在不同直线上对应的值
    def line(x):
        return a * x - b
    return line   #注意这里返回line ,而不是line（）。外函数返回内函数的引用，这里的引用指的是内函数line在内存中的起始地址，最终调用内函数line()得到返回值7
a = func(5, 1)
print(a)  #<function func.<locals>.line at 0x1063e2dd0>
print(a(1)) #输出为1
为社么说能提升代码复用性呢？
如果我们要设很多˙直线，2*x-1，3*x+2，4*x+7 等，为每一个直线 写上面几行代码肯定 会造成很多重复。现在利用闭包 就可以轻松解决了。


```

**装饰器**：**增强函数或类的功能的一个函数**

经常用于 插入日志、性能测试。假设现在产品经理想知道所有函数的执行时间，那我们得为所有函数去写计算执行时间的代码嘛？聪明的你必然知道 肯定不是啦。我们可以去定义 一个装饰器函数，用来计算每个函数的执行时间，再对每个需要被修饰的函数 使用装饰器

```
def time_calc(func): #定义装饰器函数
	def wrapper(*args,**kargs):
		s_time=time.time()
		f=func(*args,**kargs)
		time=time.time()-start.time
		return func
	return wrapper
假设被修饰函数是
def add(x,y):
	return x+y

使用装饰器:一种使用语法糖@ ，第二种time_calc(x,y)(add)
@time_calc
def add(x,y):
	return x+y
```



## 七、进程VS线程

进程进程是线程的容器,一个进程可以包含多个线程。是系统进行资源分配和调度的最小单位,进程之间数据不能互相访问。线程是运算调度的最小单位,线程是程序执行流的最小单元, 每一个进程都至少有一个线程, 线程之间数据可以共享。进程线程都是由操作系统调度,python中多线程和多进程都是通过切换上下文来实现,都会耗费额外的系统资源
进程和线程都面临着内核态和用户态的切换问题而耗费许多切换时间，而协程就是用户自己控制切换的时机，不再需要陷入系统的内核态。Python里最常见的yield就是协程的思想

线程有几种状态?生命周期是怎样的?

线程有五种状态:创建、就绪start()、运行run()、阻塞、死亡。
调用start方法时，线程就会进入就绪状态。
在线程得到cpu时间片时进入运行状态。
线程调用yield方法可以让出cpu时间回到就绪状态。
线程运行时可能由于IO、调用sleep、wait、join方法或者无法获得同步锁等原因进入阻塞状态。
当线程获得到等待的资源资源或者引起阻塞的条件得到满足时，会从阻塞状态进入就绪状态。
当线程的run方法执行结束时，线程就进入死亡状态。

**Python 多线程为何鸡肋**

 	在非python环境中，多核时可以支持多个线程同时执行。但是在<u>python中，无论有多少核，同时只能执行一个线程</u>。究其原因，这就是由于GIL的存在导致的。GIL的全称是Global Interpreter Lock(全局解释器锁)，来源是python设计之初的考虑，为了数据安全所做的决定。某个线程想要执行，必须先拿到GIL，我们可以把GIL看作是“通行证”，并且在一个python进程中，GIL只有一个。拿不到通行证的线程，就不允许进入CPU执行。GIL只在cpython中才有，因为cpython调用的是c语言的原生线程，所以他不能直接操作cpu，只能利用GIL保证同一时间只能有一个线程拿到数据。而在pypy和jpython中是没有GIL的。python下想要充分利用多核CPU，就用多进程。因为每个进程有各自独立的GIL，互不干扰，这样就可以真正意义上的并行执行，在python中，多进程的执行效率优于多线程(仅仅针对多核CPU而言)。

**python针对不同类型的代码执行效率也是不同的：**

> 1、CPU密集型代码(各种循环处理、计算等等)，在这种情况下，由于计算工作多，ticks计数很快就会达到阈值，然后触发GIL的释放与再竞争（多个线程来回切换当然是需要消耗资源的），所以**python下的多线程对CPU密集型代码并不友好**。
> 2、IO密集型代码(文件处理、网络爬虫等涉及文件读写的操作)，多线程能够有效提升效率(单线程下有IO操作会进行IO等待，造成不必要的时间浪费，而开启多线程能在线程A等待时，自动切换到线程B，可以不浪费CPU的资源，从而能提升程序执行效率)。所以python的多线程对IO密集型代码比较友好。



## 八、内存管理和垃圾回收机制

Python 主要使用<u>引用计数</u>（reference counting）来跟踪和回收垃圾。在引用计数的基础上，通过“标记-清除”（mark and sweep）解决容器对象可能产生的循环引用问题，通过“分代回收”（generation）以空间换时间的方法提高垃圾回收效率。  

1. 内存管理&引用计数
   python创建新对象都是在内存上开辟一个块, 每个对象只存有一份数据, 赋值和复制都是创建了新的引用, 使用的是对象和引用分离策略.在Python中，每个对象都有存有指向该对象的引用总数，即引用计数, 如果引用计数为0, 那这个对象就会被python垃圾回收机制回收

2. 标记-清除机制
   基本思路是先按需分配，等到没有空闲内存的时候从寄存器和程序栈上的引用出发，遍历以对象为节点、以引用为边构成的图，把所有可以访问到的对象打上标记，然后清扫一遍内存空间，把所有没标记的对象释放。
   同时为了保证效率, Python只会在垃圾达到一定阈值时，垃圾回收才会启动。

3. 分代回收策略
   这一策略的基本假设是，存活时间越久的对象，越不可能在后面的程序中变成垃圾。Python默认定义了三代对象集合，索引数越大，对象存活时间越长。