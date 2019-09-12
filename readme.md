实验报告：


实验准备：

1. 配置GOPATH环境变量，如下
$ mkdir $HOME/work
$ export GOPATH=$HOME/work
$ export PATH=$PATH:$GOPATH/bin

2. 建立包路径，在github（我的github名称是Aivo520, 仓库名为Aivo）下建立工作空间，如下
$ mkdir -p $GOPATH/src/github.com/Aivo520/Aivo

3. 建立一个新项目，并编写测试hello.go
$ mkdir $GOPATH/src/github.com/Aivo520/Aivo/hello
$ cd $GOPATH/src/github.com/Aivo520/Aivo/hello
$ vim hello.go
'''
package main

import "fmt"

func main() {
	fmt.Printf("Hello, world.\n")
}
'''
$ go install github.com/user/hello
$ hello
//注意，此时你可以在任意地方运行hello


实验过程：
$ mkdir $GOPATH/src/github.com/user/stringutil
