### <p align="center">loadbalance</p>
#### <p align="center">随机、轮训、权重、哈希负载均衡</p>
#### <p align="center"><a href="https://github.com/mazezen/loadbalance/releases"><img src="https://img.shields.io/github/release/loadbalance/releases.svg" alt="GitHub release"></a><a href="https://github.com/mazezen/loadbalance/blob/master/LICENSE"><img src="https://img.shields.io/github/license/mashape/apistatus.svg" alt="license"></a><p>
#### <p align="center"><a href="./README.md" target="_blank">简体中文</a> | <a href="./README_en.md" target="_blank">English</a> </p>

### 安装
```shell
go get github.com/mazezen/loadbalance
```

### E.g
#### 1. 随机
```go
r := &RandomBalancing{}
r.Add("127.0.0.1:2003")
r.Add("127.0.0.1:2004")
r.Add("127.0.0.1:2005")
r.Add("127.0.0.1:2006")
r.Add("127.0.0.1:2007")

fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
```
<img src="./random-load.png">

#### 2.轮训
```go
r := &RoundRotationBalance{}
r.Add("127.0.0.1:2003")
r.Add("127.0.0.1:2004")
r.Add("127.0.0.1:2005")
r.Add("127.0.0.1:2006")
r.Add("127.0.0.1:2007")

fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
```
<img src="./rotation-load.png">

#### 3.权重
```go
r := &WeightBalance{}
r.Add("127.0.0.1:2003", "4")
r.Add("127.0.0.1:2004", "3")
r.Add("127.0.0.1:2005", "2")

fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
fmt.Println(r.Next())
```
<img src="./weighted-load.png">

#### 4. 一致性hash
```go
r := NewConsistentHashBalance(10, nil)
r.Add("127.0.0.1:2003")
r.Add("127.0.0.1:2004")
r.Add("127.0.0.1:2005")
r.Add("127.0.0.1:2006")
r.Add("127.0.0.1:2007")

fmt.Println(r.Get("http://127.0.0.1:2002/base/getinfo"))
fmt.Println(r.Get("http://127.0.0.1:2002/base/errinfo"))
fmt.Println(r.Get("http://127.0.0.1:2002/base/getinfo"))
fmt.Println(r.Get("http://127.0.0.1:2002/base/pwd"))

fmt.Println(r.Get("127.0.0.1"))
fmt.Println(r.Get("192.168.0.1"))
fmt.Println(r.Get("127.0.0.1"))
```
<img src="./consistent-hash-load.png">