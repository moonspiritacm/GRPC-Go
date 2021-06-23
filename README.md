# GRPC-Go

A simple grpc example in Go, referring to https://github.com/grpc/grpc-go/tree/master/examples.

## 1. 相关技术

### 1.1 Protobuf

Protobuf (Protocol Buffer) 是谷歌推出的一种通用数据交换格式，它独立于语言和平台。谷歌官方提供了 Java、C#、C++、Go、Python 等多种语言的具体实现，每种实现包含编译器和库文件两部分。Protobuf 是一种二进制格式，比 xml、json 等数据交换格式体积更小、速度更快，多用于分布式应用间的数据通信或者异构环境下的数据交换。

### 1.2 Protoc

Protoc 是 Protobuf 通用编译器，基于 C++ 实现，可以把 .proto 文件编译成各种语言对应的源代码，实现 Protobuf 数据交换格式与编程语言的解耦合。Protoc 项目托管在 [GitHub 仓库](https://github.com/protocolbuffers/protobuf) 中，可以下载源码本地编译，也可以直接下载对应平台的预编译文件。

```shell
protoc --go_out=plugins=grpc:. *.proto
```

其中，`--go_out=plugins=grpc:` 表示目标编译语言为 Go，并且该协议文件用于 grpc 通信（自动生成相关接口）。protoc 在内部是调用 protoc-gen-go 实现 Go 语言处理的。如果没有安装 protoc-gen-go，执行上述命令会出现 "--go_out: protoc-gen-go: Plugin failed with status code 1." 错误。

protoc-gen-go 是 Protobuf 的 Go 语言实现，它包含两部分：一个协议编译器插件，可以根据 .proto 文件生成 Go 源文件；一个运行库，实现 Protobuf 编解码的运行时支持。

```shell
go get -u github.com/golang/protobuf/protoc-gen-go
```

### 1.3 grpc

grpc 是谷歌开发的高性能、通用的开源 RPC 框架，主要面向移动应用开发并遵循 HTTP/2 协议标准，基于 Protobuf 数据交换格式开发，支持多种开发语言。

grpc 和 Protobuf 是一种天然的结合，但二者并非完全绑定。一方面，grpc 可以选用 json 等其他数据交换格式；另一方面，Protobuf 可以广泛用于序列化操作中，而不限于 RPC 通信。
