## 目录 ##
基本知识：
* [重点](#重点)
 * [推荐的编辑器](#推荐的编辑器 )
 * [需要设置的三个环境变量](#需要设置的三个环境变量)
* [示例 ](#示例 )
* [编译](#编译)
* [安装第三方包](#安装第三方包)

语法：
* [定义变量](#定义变量)
* [类型介绍](#类型介绍)


## 重点 ##
golang: 简介：C的变异版本
* 变量声明了就必须要用
* 模块导入了就必须要用
* 循环只有for，没有while和do...while
* golang是后置类型，变量可以自动识别类型，变量可以用:=命名
* NULL在golang里变成了nil

## 示例 ##
一个简单的例子
```golang
package main //程序包名

import "fmt" //导入的模块

func main()  {
	fmt.Print("666");
}


```

## 编译 ##
直接根据使用的平台自动生成：
```
C:\golang\bin\golang.exe build -o I:\exe\build\golang_build_test_golang.exe I:/exe/test.golang 
-i #指定文件路径
-o #build生成后保存的名称
```

定义平台类型和生成位数：
>方法二：本地编译
cmd控制台到main.golang文件目录下
set golangARCH=amd64
set golangOS=linux
golang build main.golang

会生成一个没有后缀的二进制文件
main
将该文件放入linux系统某个文件夹下
赋予权限
chmod 777 main
最后执行 ./main 就行了。
如果想让项目在后台执行：执行 nohup ./main & ，这样就可以程序在后台运行了

golang 支持在一个平台下生成另一个平台可执行程序的交叉编译功能。

Mac下编译Linux, Windows平台的64位可执行程序：

Cgolang_ENABLED=0 golangOS=linux golangARCH=amd64 golang build test.golang
Cgolang_ENABLED=0 golangOS=windows golangARCH=amd64 golang build test.golang
Linux下编译Mac, Windows平台的64位可执行程序：

Cgolang_ENABLED=0 golangOS=darwin golangARCH=amd64 golang build test.golang
Cgolang_ENABLED=0 golangOS=windows golangARCH=amd64 golang build test.golang
Windows下编译Mac, Linux平台的64位可执行程序：

SET Cgolang_ENABLED=0
SET golangOS=darwin3
SET golangARCH=amd64
golang build test.golang

SET Cgolang_ENABLED=0
SET golangOS=linux
SET golangARCH=amd64
golang build test.golang

golangOS：目标可执行程序运行操作系统，支持 darwin，freebsd，linux，windows
golangARCH：目标可执行程序操作系统构架，包括 386，amd64，arm

golang version 1.5以前版本在首次交叉编译时还需要配置交叉编译环境：
Cgolang_ENABLED=0 golangOS=linux golangARCH=amd64 ./make.bash
Cgolang_ENABLED=0 golangOS=windows golangARCH=amd64 ./make.bash

## 推荐的编辑器 ##
* Vscode
* Goland
* Submine

## 需要设置的三个环境变量 ##
```
GOPATH=I:\exe #项目路径
GOPROXY=https://goproxy.io #module 代理，在国内设置为了安装第三方包
GOROOT=C:\GO\ #go安装的路径
```
![](https://s1.ax1x.com/2020/05/06/YEQH6U.png)

## 安装第三方包 ##
在`https://godoc.org/`搜索对应的库
执行`go get <module_name>`
Example:`go get github.com/shirou/gopsutil`
会在GOPATH路径下创建一个pkg文件夹，里面就是你下载的库
![由于路径过于混乱，打码了防止读者看懵逼](https://s1.ax1x.com/2020/05/06/YE1jRx.png)

然后从pkg文件夹里把模块直接复制到自己的设置的路径里


**Goland识别第三方模块（包括基本配置）**
![](https://s1.ax1x.com/2020/05/06/YE31Fs.png)
GOROOT:Go Version  
GOPATH:Project Path  
Imports:Modules Path  
GO MODULES:Module agent  

GOROOT如果go是安装在默认路径的话，打开Goland就能看到对应的版本了  
GOPATH为你项目的地址前面设置了环境变量，这里会自动设置好  
![](https://s1.ax1x.com/2020/05/06/YE3rf1.png)

Imports为你的第三方模块路径，设置为`GOPATH\pkg\mod`(这里可以设置多个mod路径)  
![](https://s1.ax1x.com/2020/05/06/YE8sEQ.png)

GO MODULES，在墙内无法直接访问到github.com所以要设置这个  
设置为：`https://goproxy.io`(如果设置了GOPROXY环境变量这里应该会有，如果没有自己在设置一下)  
![](https://s1.ax1x.com/2020/05/06/YE8TUJ.png)

根据`https://goproxy.io/`进行设置  
![](https://s1.ax1x.com/2020/05/06/YEGi8I.png)

之后在项目里创建go.mod  
`go mod init test`
然后在项目里调用第三方的库，运行的时候就会自动在go.mod里添加。或者你手动加下也行  
重要的是goland能识别你下载的第三方库，否则白搞  
![](https://s1.ax1x.com/2020/05/06/YEGhRI.png)


## 定义变量 ##
定义一个变量的方法有：
* var <变量名> <类型>=<值>
* var <变量名>=<值>
* <变量名> := <值>

## 类型简介 ##
**字符串**
>golang语言中有一些通用的类型，例如"int"和"float"，它们对应的内存大小和处理器类型相关。同时， 也包含了许多固定大小的类型，例如"int8"和"float64"，还有无符号类型"uint"和"uint32"等。 需要注意的是，即使"int"和"int32"占有同样的内存大小，但并不是同一种数据类型。不过 "byte"和"uint8"对应是相同的数据类型，它们是字符串中字符类型。

注意事项：
* 默认值是空字符串 ""。
* 用索引号访问某字节，如 s[i]。
* 不能用序号获取字节元素指针，&s[i] 非法。 
* 不可变类型，无法修改字节数组。
* 字节数组尾部不包含 NULL。

golang中的字符串是一个内建数据类型。字符串虽然是字符序列，但并不是一个字符数组。可以创建新的 字符串，但是不能改变字符串。不过我们可以通过新的字符串来达到想改变字符串的目的。 下面列举"strings.golang"例子说明字符串的常见用法：
```golang
package main //程序包名

import "os"

func main()  {
	s :="this is testing";
	if s[1]!='t'{
		os.Exit(1)
	}
	s="fucking Cpp !!!"
	var p *string=&s
	*p="lbw nb"
}
```

试图修改任何字符串都是不行的
```golang
package main //程序包名


func main()  {
	s :="this is testing";
	s[0]="v"; //.\test.golang:6:6: cannot assign to s[0]
}

```

切片获取字符串的内容：
```golang
package main

import "fmt"

func main() {
	data:="lbw is 666"
	fmt.Println(data[:3])
}
```
输出：`lbw`

拼接字符串，方法有两种：
* +号拼接
* sprintf()

使用加号拼接
```golang
package main

import "fmt"

func main() {
	data:="lbw is 666"+
		"fucking good" //连接跨行字符串时，"+" 必须在上一行末尾，否则导致编译错误
	
	fmt.Println(data)
}
```

使用sprintf拼接：
```golang
package main

import "fmt"

func main() {
	data:=fmt.Sprintf("lbw is 666 %s","fucking good")
	fmt.Println(data)
}
```

遍历字符串：
```golang
//使用range
package main

import "fmt"

func main() {
	data:=fmt.Sprintf("lbw is 666 %s","fucking good")
	for _,vk:=range data{
		fmt.Println(string(vk))
	}
}


//获取字符串大小遍历
package main

import "fmt"

func main() {
	data:=fmt.Sprintf("lbw is 666 %s","fucking good")
	for calc:=0;calc<len(data);calc++{
		fmt.Println(string(data[calc]))
	}
}
```

常用的处理字符串函数：
* index() 寻找字符串第一次出现的位置
* Lastindex() 寻找字符串最后一次出现的位置
* Replace() || Replaceall() 替换字符串
* Repeat() 重复字符串N次
* ToUpper()  str转大写
* ToLower() str转小写
* TrimSpace() 去掉str首尾空格
* Trim() 去掉字符串首尾指定的字符
* TrimRight() 去掉字符串尾部指定的字符
* TrimLeft() 去掉字符串首部指定的字符
* split() 将指定字符串去除并转换成列表
* join() 从列表转换回字符串


index()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="USA fucking"
	fmt.Println(strings.Index(data,"fucking"))
}
```
输出：`4`

Lastindex()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="USA fucking"
	fmt.Println(strings.Index(data,"u"))
}
```
输出：`5`


Replace() and Replaceall()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="USA fucking"
	fmt.Println(strings.Replace(data,"u","l",1)) //1为替换的次数
	fmt.Println(strings.ReplaceAll(data,"i",""))
}
```
输出：`USA flcking\nUSA fuckng`

Repeat()
```golang
package main

import (
	"bytes"
	"fmt"
)

func main() {
	data:="USA fucking "
	fmt.Println(data)
	fmt.Println(string(bytes.Repeat([]byte(data),2))) //重复输出字符串两次
}

```
输出：
`USA fucking
USA fucking USA fucking`

ToUpper()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="USA fucking "
	fmt.Println(strings.ToUpper(data))
}
```
输出：`USA FUCKING`

ToLower()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="THIS"
	fmt.Println(strings.ToLower(data))
}
```
输出：`this`

Trimspace()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:=" THIS "
	fmt.Println(strings.TrimSpace(data))
}
```
输出：`THIS`

Trim()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="DDDTHISDDD"
	fmt.Println(strings.Trim(data,"DDD"))
}
```
输出：`THIS`

TrimRight()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="DDDTHISDDD"
	fmt.Println(strings.TrimRight(data,"DDD"))
}
```
输出：`DDDTHIS`

TrimLeft()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="DDDTHISDDD"
	fmt.Println(strings.TrimLeft(data,"DDD"))
}
```
输出：`THISDDD`


**列表**
列表的定义（参考链接：https://blog.csdn.net/ywdhzxf/java/article/details/83689375）
```golang
package main //程序包名
import "fmt"

func main()  {
	  // 声明列表, 下面两种为初始化, 生成内存地址, 双链表 ----容器
    var list3 = list.List{} //动态列表
    list4 := list.New()
    list5 :=[] int[10] //固定位数列表
   //列表插入方法
    a1 := list3.PushFront(2) //从左插入
    a2 :=list3.PushBack(1)  //从右插入
    list3.InsertAfter("after", a2)   //在 a2之后
    list3.InsertBefore("before", a1) //在 a1之前

    //列表删除
    list3.Remove(a2)

    //列表(容器)遍历
    for x := list3.Front(); x != nil; x = x.Next() {
        if x.Value == "after" {
            fmt.Println(x.Value)
        }
        fmt.Print(x.Value, " , ")
    }
}
```

**map**
定义方法：
```golang
map[sting]int #string代表key是string类型，int代表value是int类型
```
Example:
```golang
package main //程序包名
import "fmt"

func main()  {
	s :=map[string]int{"one":1,"two":2}
	fmt.Println(s["one"]); //1
}
```
定义不确定大小的map：
```golang
make(map[string]string)
```

Example2:
```golang
package main //程序包名
import "fmt"

func main()  {
	s:=make(map[string]string)
	s["one"]="ACBD"
	fmt.Println(s["one"]); //1
}
```

定义固定大小的map:
```golang
make(map[string]string,100) //最大100个
```

遍历map:
```golang
package main //程序包名
import "fmt"

func main()  {
	s:=make(map[string]string)
	s["one"]="ACBD"
	for x:=range s{ //只有key
		fmt.Println(x)
	} 

	for key,value:=range s{ //key和value
		fmt.Println(key,value)
	} 
}
```

map类型的切片：
```golang
package main
import "fmt"

func main() {
    // Version A:
    items := make([]map[int]int, 5)
    for i:= range items {
        items[i] = make(map[int]int, 1)
        items[i][1] = 2
    }
    fmt.Printf("Version A: Value of items: %v\n", items)

    // Version B: NOT GOOD!
    items2 := make([]map[int]int, 5)
    for _, item := range items2 {
        item = make(map[int]int, 1) // item is only a copy of the slice element.
        item[1] = 2 // This 'item' will be lost on the next iteration.
    }
    fmt.Printf("Version B: Value of items: %v\n", items2)
}
```

map的排序：
```golang
// the telephone alphabet:
package main
import (
    "fmt"
    "sort"


)

var (
    barVal = map[string]int{"alpha": 34, "bravo": 56, "charlie": 23,
                            "delta": 87, "echo": 56, "foxtrot": 12,
                            "golf": 34, "hotel": 16, "indio": 87,
                            "juliet": 65, "kili": 43, "lima": 98}
)

func main() {
    fmt.Println("unsorted:")
    for k, v := range barVal {
        fmt.Printf("Key: %v, Value: %v / ", k, v)
    }
    keys := make([]string, len(barVal))
    i := 0
    for k, _ := range barVal {
        keys[i] = k
    	i++
    }
    sort.Strings(keys) //从小到大排序
    fmt.Println()
    fmt.Println("sorted:")
    for _, k := range keys {
        fmt.Printf("Key: %v, Value: %v / ", k, barVal[k])
    }
}
```

split()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="DDDTHISDDD"
	fmt.Println(strings.Split(data,"DDD"))
}
```
输出：`[ THIS ]`


join()
```golang
package main

import (
	"fmt"
	"strings"
)

func main() {
	data:="DDDTHISDDD"
	fmt.Println(strings.Join(strings.Split(data,"DDD"),""))
}
```
输出：`THIS`


**常量**
使用const定义常量，example：
(常量的值不可被修改)
```golang
package main

import "fmt"

func main(){
	const a="This is AAAAAA"
	const ( //常量组，用法没区别
		test="BBB"
		test2="CCC"
		)
	fmt.Println("This is Cons A:",a)
}
```
iota ，特殊的常量类型
>iota，特殊常量，可以认为是一个可以被编译器修改的常量。
在每一个const关键字出现时，被重置为0，然后再下一个const出现之前，每出现一次iota，其所代表的数字会自动增加1。
关键字 iota 定义常量组中从 0 开始按行计数的自增枚举值。

```golang
package main

import "fmt"

func main(){
	const (a=iota
	b
	c
	d)
	fmt.Println(a,b,c,d)
}
```
输出:`0 1 2 3`

在同一常量组中，可以提供多个 iota，它们各自增长。
```golang
package main

import "fmt"

func main(){
	const (a=iota
	b=iota
	c=10
	d)
	fmt.Println(a,b,c,d)
}
```
输出：`0 1 10 10`

```golang
package main

import "fmt"

func main(){
	const (
		_        = iota // iota = 0
		KB int64 = 1 << (10 * iota) //从这里开始，每下面一个const都会*1024
		MB       // iota=1
		GB       // 与 KB 表达式相同，但 iota = 2
		TB
	)

	fmt.Println(KB,MB,GB,TB)
}
```
输出：`1024 1048576 1073741824 1099511627776`

如果 iota 自增被打断，须显式恢复
```golang
package main

import (
	"fmt"
)

const (
	A = iota //0
	B        // 1
	C = "c"  //c
	D        // c，与上  相同。
	E = iota // 4，显式恢复。注意计数包含了 C、D 两 。
	F        // 5
)

func main() {
	fmt.Println(A, B, C, D, E, F)
}
```
想要恢复自增得在次赋一次iota


**申请内存**
在golang语言中，大部分的类型都是值变量。例如int或struct(结构体)或array(数组)类型变量， 赋值的时候都是复制整个元素。如果需要为一个值类型的变量分配空间，可以用new()：
```golang
package main //程序包名

func main()  {
	type T struct {
		a,b int
	}
	t :=new (T);
}
```

还有另外一些类型，如：maps, slices 和 channels(见下面)是引用语意（reference semantics）。 如果你一个slice 或 map内的元素，那么其他引用了相同slice 或 map的变量也能看到这个改变。 对于这三类引用类型的变量，需要用另一个内建的make()分配并初始化空间：

```golang
 m := make(map[string]int);
```

上目的代码定义一个新的map并分配了存储空间。如果只是定一个map而不想分配空间的话，可以这样：
```golang
var m map[string]int;
```

它创建了一个nil(空的)引用并且没有分配存储空间。如果你想用这个map, 你必须使用make来 分配并初始化内存空间或者指向一个已经有存储空间的map。

注意: new(T) 返回的类型是 *T , 而 make(T) 返回的是引用语意的 T 。如果你(错误的)使用 new() `分配了一个引用对象，你将会得到一个指向 nil 引用的指针。这个相当于声明了一个未初始化引用变量并取得 它的地址。`

**数组**
```golang
 数组：是同一种数据类型的固定长度的序列。
 数组定义：var a [len]int，比如：var a [5]int，数组长度必须是常量，且是类型的组成部分。一旦定义，长度不能变。
 长度是数组类型的一部分，因此，var a[5] int和var a[10]int是不同的类型。
 数组可以通过下标进行访问，下标是从0开始，最后一个元素下标是：len-1
    for i := 0; i < len(a); i++ {
    }
    for index, v := range a {
    }
 访问越界，如果下标在数组合法范围之外，则触发访问越界，会panic
 数组是值类型，赋值和传参会复制整个数组，而不是指针。因此改变副本的值，不会改变本身的值。
 支持 "=="、"!=" 操作符，因为内存总是被初始化过的。
 指针数组 [n]*T，数组指针 *[n]T。
```




## 流程处理 ##
**select**
>select 语句
select 语句类似于 switch 语句，但是select会随机执行一个可运行的case。如果没有case可运行，它将阻塞，直到有case可运行。
select 是Go中的一个控制结构，类似于用于通信的switch语句。每个case必须是一个通信操作，要么是发送要么是接收。
select 随机执行一个可运行的case。如果没有case可运行，它将阻塞，直到有case可运行。一个默认的子句应该总是可运行的。

>在一个select语句中，Go会按顺序从头到尾评估每一个发送和接收的语句。
如果其中的任意一个语句可以继续执行（即没有被阻塞），那么就从那些可以执行的语句中任意选择一条来使用。
如果没有任意一条语句可以执行（即所有的通道都被阻塞），那么有两种可能的情况：
①如果给出了default语句，那么就会执行default的流程，同时程序的执行会从select语句后的语句中恢复。
②如果没有default语句，那么select语句将被阻塞，直到至少有一个case可以进行下去。

语法：
```golang
select {
    case communication clause  :
       statement(s);      
    case communication clause  :
       statement(s);
    /* 你可以定义任意数量的 case */
    default : /* 可选 */
       statement(s);
}
```

说明：
 *  每个 case 都必须是一个通信
 * 所有 channel 表达式都会被求值
 * 所有被发送的表达式都会被求值
 *   如果任意某个通信可以进行，它就执行，其他被忽略。
* 如果有多个 case 都可以运行，Select 会随机公平地选出一个执行。其他不会执行。
    否则：
    1. 如果有 default 子句，则执行该语句。
     2. 如果没有 default 子句，select 将阻塞，直到某个通信可以运行；Go 不会重新对 channel 或值进行求值。

使用select的时候需要用到chan类型
>通道又叫channel，顾名思义，channel的作用就是在多线程之间传递数据的。
创建无缓冲channel
chreadandwrite :=make(chan int)
chonlyread := make(<-chan int) //创建只读channel
chonlywrite := make(chan<- int) //创建只写channel 
参考链接：[Golang 关于通道 Chan 详解_golang_geek的博客-CSDN博客](https://blog.csdn.net/netdxy/java/article/details/54564436)

Example:
```golang
package main

import "fmt"
func main(){
    var cha=make(chan int) //创建一个通道
    var cha2=make(chan int)

    select {
    case i1:=<-cha:
        fmt.Println("this is i1:",i1)
    case i2:=<-cha2:
        fmt.Println("this is i2:",i2)
    default:
        fmt.Println("no cha and cha2")
        
    }

}
```
结果输出为`no cha and cha2`因为cha 为nil，cha2也是nil。没有值，跑到了default里


```golang
package main

import "fmt"
func main(){
	var cha=make(chan int,1) //主线程休眠一秒
	var cha2=make(chan int)

	cha<-6
	select {
	case i1:=<-cha:
		fmt.Println("this is i1:",i1)
	case i2:=<-cha2:
		fmt.Println("this is i2:",i2)
	default:
		fmt.Println("no cha and cha2")
	}

}
```
输出`this is i1: 6`cha为6，在判断cha的时候发现有值所以执行了
避免：`all goroutines are asleep - deadlock!`错误，这个错误是什么？
>创建了一个无缓冲的channel，然后给这个channel赋值了，程序就是在赋值完成后陷入了死锁。因为我们的channel是无缓冲的，即同步的，赋值完成后来不及读取channel，程序就已经阻塞了。这里介绍一个非常重要的概念：channel的机制是先进先出，如果你给channel赋值了，那么必须要读取它的值，不然就会造成阻塞，当然这个只对无缓冲的channel有效。对于有缓冲的channel，发送方会一直阻塞直到数据被拷贝到缓冲区；如果缓冲区已满，则发送方只能在接收方取走数据后才能从阻塞状态恢复。


Eaxmple2:
```goalng
import (

    "fmt"
    "time"
)
func produce(p chan<- int) {
    for i := 0; i < 10; i++ {
        p <- i
        fmt.Println("send:", i)
    }
}
func consumer(c <-chan int) {
    for i := 0; i < 10; i++ {
        v := <-c
        fmt.Println("receive:", v)
    }
}
func main() {
    ch := make(chan int, 10)
    go produce(ch)
    go consumer(ch)
    time.Sleep(1 * time.Second)
}
```


**if**
```golang
package main

import "fmt"

func main(){
	var data="A"
	if data=="A"{
		fmt.Println("This is A")
	}else if(data=="B"){
		fmt.Println("This is B")
	}else{
		fmt.Println("Not data")
	}

}
```

**switch**
```golang
package main

import "fmt"

func main(){
	var data="A"
	switch data {
	case "B":
		fmt.Println("This is B")
	case "C":
		fmt.Println("This is C")
	default:
		fmt.Println("not found data")
	}
}
```

**for**
```golang
package main

import "fmt"

func main(){
	data:=[]string{"A","B","C","D","E","F"}
	for calc:=0;calc<len(data);calc++{
		fmt.Println("value:",data[calc])
	}
}
```

**range**
```goalng
package main

import "fmt"

func main(){
	data:= map[string]int{"key":1,"key2":2}
	for x,v:=range data{
		fmt.Println(x,v)
	}
}
```

**循环控制**
continue、break、goto

continue示例：
```golang
package main

import "fmt"

func main(){
	data:= map[string]int{"key":1,"key2":2}
	for x,v:=range data{
		if v==1{
			continue
		}
		fmt.Println(x,v)
	}
}
```

break示例：
```golang
package main

import "fmt"

func main(){
	data:= map[string]int{"key":1,"key2":2}
	for x,v:=range data{
		if v==1{
			break
		}
		fmt.Println(x,v)
	}
}
```

goto示例：
```golang
package main

import "fmt"

func main(){
	a:=10
	LOOP: a+=1 //定义跳转瞄点
	for a<20{
		fmt.Println(a)
		goto LOOP //跳转到瞄点从瞄点开始执行语句
	}
}
```

**搭配的逻辑运算符**
不能使用三元运算那
```
if a=="a"?fmt.println("Not a") //不行
```

&& -> and
|| -> or

```golang
package main

import "fmt"

func main(){
	a:="A"
	if(a=="A"&&a!="B"){
		fmt.Println(a)
	}
}
```
