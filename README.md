# hello-go-mod



## 版本 

git 的release 即是go mod 的版本号

### 没有Release时

自动生成的版本号为：`v0.0.0-20190505092205-ebba11f9ea84`，由三部分组成，其中 `v0.0.0`是初始版本号，`20190505092205`是精确到秒的utc时间`ebba11f9ea84`为commit id，最新的提交。  




If the module is version v2 or higher, the major version of the module must be included as a /vN at the end of the module paths used in go.mod files (e.g., module github.com/my/mod/v2, require github.com/my/mod/v2 v2.0.0) and in the package import path (e.g., import "github.com/my/mod/v2/mypkg").
If the module is version v0 or v1, do not include the major version in either the module path or the import path.

v2.0.0
git release ,但是  go.mod 后缀没有加/vN 

v2.0.2  go.mod 增加后缀 /v2