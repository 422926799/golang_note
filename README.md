# golang_note #
为了记录自己学习golang的过程创建的笔记仓库

## 目录 ##
事前准备：
[重点](#重点)

## 重点 ##
golang简介:C的变异版本
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

**数组**
数组的定义
```golang
package main //程序包名
import "fmt"

func main()  {
	var lists[10] int;
	for calc :=0;calc<10;calc++{
		lists[calc]=calc
	}
	fmt.Println(lists) //[0 1 2 3 4 5 6 7 8 9]
}
```

**哈希表**
```golang
package main //程序包名
import "fmt"

func main()  {
	s :=map[string]int{"one":1,"two":2}
	fmt.Println(s["one"]); //1
}
```

## 申请内存 ##
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

注意: new(T) 返回的类型是 *T , 而 make(T) 返回的是引用语意的 T 。如果你(错误的)使用 new()分配了一个引用对象，你将会得到一个指向 nil 引用的指针。这个相当于声明了一个未初始化引用变量并取得 它的地址。


**.......未完待续**
