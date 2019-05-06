# hello-go-mod

## 定义模块
`$ export GO111MODULE=on` 
`$ go mod init  [name]`  go mod init github.com/my/repo


## 版本相关

go mod 的版本号对应 git的 commit，一般会用Tag，branch，或者是commit id。如果找不到有效的release，则会用最后一次提交生成一个最新版本号。

e.g. `v0.0.0-20190505092205-ebba11f9ea84`
由三部分组成，其中 `v0.0.0`是初始版本号，`20190505092205`是精确到秒的utc时间`ebba11f9ea84`为commit id，最新的提交。  


### 主版本号与go.mod的关系。

当主版本号 大于等于2时 （v2^.x.x），module 必须包含 /vN 作为后缀，引用时也需要增加对应后缀。
当主版本号是 0或者1时（v{0,1}.x.x），则不需要版本后缀。

>- If the module is version v2 or higher, the major version of the module must be included as a /vN at the end of the module paths used in go.mod files (e.g., module github.com/my/mod/v2, require github.com/my/mod/v2 v2.0.0) and in the package import path (e.g., import "github.com/my/mod/v2/mypkg").
>- If the module is version v0 or v1, do not include the major version in either the module path or the import path.

### demo 版本说明
v0.1.0，v1.0.0 测试不加后缀的版本升级。 v2.x.x 为加后缀的版本升级

- v0.1.0 
- v1.0.0 测试从v0.1.0 升级到v1.0.0
- v2.0.0 go.mod 没有/vN 后缀. 有悖于规则，版本无效。
- v2.0.1 go.mod 增加后缀/v2
- v2.0.2 go.mod 增加后缀/v2, 测试版本从v2.0.1 升级到v2.0.2

多版本共存时，需要从大版本上区别,也就是说后缀不同。

### 升级
`$ go list -u -m all`  查看所有依赖。
> github.com/chengjk/hello-go-mod v0.1.0 [v1.0.0] 
> 当前是 v0.1.0 可以升级为 v1.0.0




`go get -u mod[@version]` 次要版本号升级到指定新版，默认是@latest。
> -u 获取直接或者间接依赖， 通常不加该参数。
> go get -u github.com/chengjk/hello-go-mod 
从当前的v0.1.0 升级到 v1.0.0

`go get -u=patch` 升级到最新补丁版。
> 升级到最新补丁版



---

[官方文档](https://github.com/golang/go/wiki/Modules#how-to-use-modules)