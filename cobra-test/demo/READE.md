# Go 每日一库学习之 cobra
cobra是一个命令行程序库，可以用来编写命令行程序。同时，它也提供了一个脚手架， 用于生成基于 cobra 的应用程序框架。非常多知名的开源项目使用了 cobra 库构建命令行，如Kubernetes、Hugo、etcd等等等等。

## 使用
`sudo apt install cobra`安装
`go get -u github.com/spf13/cobra@latest`

创建一个新的 Cobra 项目：
```bash
`go mod init cobrademo`
cobra init demo --pkg-name cobrademo
cd demo
```
创建一个名为 greet 的命令，用于打印出问候语。执行以下命令：
`cobra add greet`
编辑这个文件：`cmd/greet.go` 

```go
package cmd

import (
    "fmt"
    "github.com/spf13/cobra"
)

// greetCmd represents the greet command
var greetCmd = &cobra.Command{
    Use:   "greet",
    Short: "Prints a greeting message",
    Long: `This command prints a simple greeting message.`,
    Run: func(cmd *cobra.Command, args []string) {
        fmt.Println("Hello, world!")
    },
}

func init() {
    rootCmd.AddCommand(greetCmd)
}

```
可以构建并运行该应用程序了：
```bash
go build -o demo
./demo greet
./demo greet --help
# 将输出Hello, world!
```

```go
func echoCmd() {
	echoCmd := cobra.Command{
		// 命令名称
		Use: "echo",
		// 命令执行过程
		Run: func(cmd *cobra.Command, args []string) {
			fmt.Println(strings.Join(args, " "))
		},
	}

	// 执行命令
	echoCmd.Execute()
}
```
## 自动生成的文件结构
```bash
.
├── LICENSE 
├── READE.md
├── cmd
│   ├── greet.go # 对于每个子命令，都会生成一个文件，文件名与命令名称相对应。每个子命令文件中的 init() 函数将子命令添加到根命令中。
│   └── root.go # 定义了根命令，是整个应用程序的入口点。包含了应用程序的基本设置，比如版本号、作者信息等
├── demo
├── go.mod
├── go.sum
└── main.go # 整个应用程序的入口文件。
```

