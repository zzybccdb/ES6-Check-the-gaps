# npmrc 学习

npm 是用于管理依赖包, yarn 是作为改进 npm 缺点的进阶工具, 算是一个新的 cli 工具

npmrc 是 npm 运行时的读取的配置文件

有四种可配置 npmrc 的地方
1. 项目配置文件: 在项目中存在的 npmrc, 用于项目的 npm 配置
2. 用户配置文件: 在系统用户目录下, 存在的 npm 配置, 用于区隔不同系统用户, 可以使用 npm config get userconfig 查询该位置
3. 全局配置文件: 系统公共 npm 配置, 默认不存在
4. 内嵌配置文件：最后还有npm内置配置文件，基本上用不到，不用过度关注。

## registry (String) 
源地址配置

```bash
# 将源地址配置为阿里镜像
engine-strict=true
```
## _auth (String | null)
对源地址的验证

```bash
# 将源地址配置为阿里镜像
_auth="xxxxxxxxxxxxx"
```

## access (null, "restricted", or "public")
用于设置私有包的访问控制

## all (Boolean) false
是否显示所有过期或者以安装的包, 而不仅仅只是当前依赖的包

## allow-same-version (Boolean) false
防止 npm version 中内容升级后前后版本一致引发的错误

## audit (Boolean) true
允许开发人员分析复杂的代码，并查明特定的漏洞和缺陷。

## before (null or Date) null

## bin-links

## browser (null, Boolean, or String)  Default: OS X: "open", Windows: "start", Others: "xdg-open"


## engine-strict (Boolean)
用于是否开启严格控制 node 版本

```bash
# package.json
"engines": {"node" : " >= 14"}

# npmrc 
engine-strict=true
```


