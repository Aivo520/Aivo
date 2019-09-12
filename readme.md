实验报告：
仔细阅读 官方文档 如何使用Go编程 ，并按文档写第一个包，做第一次测试。
请写在 git 仓库 Readme.md 中。

实验过程：

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
$ go install github.com/Aivo520/Aivo/hello
$ hello
//注意，此时你可以在任意地方运行hello

4. 提交到远程仓库中，在hello目录下运行以下命令
$ git add hello.go
$ git commit -m "initial commit"

5. 建立一个库，包目录名字为stringutil
$ mkdir $GOPATH/src/github.com/Aivo520/Aivo/stringutil
$ vim hello.go
'''
// stringutil contains functions used to deal with strings
package stringutil

// Reverse function
func Reverse(s string) string {
	r := []rune(s)
	for i, j := 0, len(r)-1; i < len(r)/2; i, j = i+1, j-1 {
		r[i], r[j] = r[j], r[i]
	}
	return string(r)
}
'''
$ go build

6. 修改main.go文件
$ cd $GOPATH/src/github.com/Aivo520/Aivo/hello
$ vim hello.go
'''
package main

import (
	"fmt"

	"github.com/Aivo520/Aivo/stringutil"
)

func main() {
	fmt.Printf(stringutil.Reverse("!oG ,olleH"))
}
'''
$ go install github.com/Aivo520/Aivo/hello
$ hello
Hello, Go!

7. 测试，新建文件$GOPATH/src/github.com/Aivo520/Aivo/stringutil/reverse_test.go：
$ vim reverse_test.go
'''
package stringutil

import "testing"

func TestReverse(t *testing.T) {
	cases := []struct {
		in, want string
	}{
		{"Hello, world", "dlrow ,olleH"},
		{"Hello, 世界", "界世 ,olleH"},
		{"", ""},
	}
	for _, c := range cases {
		got := Reverse(c.in)
		if got != c.want {
			t.Errorf("Reverse(%q) == %q, want %q", c.in, got, c.want)
		}
	}
}
'''
$ go test github.com/Aivo520/Aivo/stringutil
ok	github.com/Aivo520/Aivo/stringutil	0.002s

8. 远程包：
$ go get github.com/golang/example/hello
$ $GOPATH/bin/hello
Hello, Go examples!
引用时，只需要import "github.com/golang/example/stringutil"


实验文档：
hello文档里面是hello.go文件
stringutil文档里面是reverse.go和reverse_test.go文件

运行说明：

