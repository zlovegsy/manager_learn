# Block

block是不是一个对象?是一个对象,苹果官方文档有说明\(搜索working with block\)

可以联系C的函数指针，指针指向一片内存空间，即对象地址

## 对比

### C语言函数指针

```
//函数
int func(int count)
//函数指针
int (*funcptr)(int)
funcptr = func
funcptr(10)等价于func(10)
```

### OC Block

```
int (^funcblock)(int count) =   ^int(int count){

}
funcblock(10)
```

### Swift闭包

```
var funcblock:((_ count:int) -> (int))?

funcblock = { (count) in

}
```

### 总结：

OC和C语言的函数指针十分相似，只是把\*替换成了^

C语言不允许匿名函数    ，OC block是一个对象，Swift 闭包是引用类型  
实际上它们都代表一片内存空间，只是不同于普通对象，这个对象本身可以运行一段代码，可以传参，可以有返回值，就类似函数。

#### MRC:管理block

block放在栈里面.

block只能使用copy,不能使用retain,使用retain,block还是在栈里面

当block代码块结束后就会被释放,这样就无法在其它方法中调用block了

#### ARC:管理block

block放在堆里面

# 协议



