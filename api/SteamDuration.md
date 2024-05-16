# SteamDuration API 接口文档

## 概述
一个用于查询 Steam 用户 Squad 游戏时长的 API 接口。该脚本通过 CGI 对外提供 API 开放能力，以保护查询密钥的安全性。它接受一个 Steam ID 作为输入参数，并返回用户在指定游戏上的累计游戏时长（以分钟为单位）。如果未找到相关信息，则返回 `null`。

## 端点
`http://api.bctc-squad.cn:8088/api/SteamDuration.sh`

## HTTP 方法
GET

## 查询参数

| 参数      | 类型   | 是否必需 | 描述                   | 默认值 |
|-----------|--------|----------|------------------------|--------|
| steamid   | string | 是       | 要查询的 Steam 用户 ID | 无     |

## 使用方法
### 示例请求
```
GET http://api.bctc-squad.cn:8088/api/SteamDuration.sh?steamid=76561197960435530
```

### 示例响应
#### 成功响应
```
Content-type: text/plain; charset=UTF8

1200
```

#### 空响应（资料未公开）
```
Content-type: text/plain; charset=UTF8

null
```

## 注意事项
- 请确保在执行该脚本的服务器上已安装并配置了 `curl` 和 `jq` 命令。
- 确保正确设置了 Steam API 密钥，并将其替换为您的实际密钥。
- 该脚本缓存的查询结果会保存在 `/var/www/api/tmp/SteamDuration/` 目录下，请确保该目录存在并具有适当的权限。
