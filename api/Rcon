# Rcon API 接口文档

## 概述
公开访问的 Rcon API，允许您使用 Rcon 命令与服务器交互。该脚本接受多个参数，并以指定格式返回服务器的响应。脚本使用 Bash 编写，并使用 Python 进行 URL 解码。

## 端点
`http://api.bctc-squad.cn:8088/api/Rcon.sh`

## HTTP 方法
GET

## 查询参数

| 参数     | 类型   | 是否必需 | 描述                                  | 默认值        |
|----------|--------|----------|---------------------------------------|---------------|
| ip       | string | 是       | 服务器的 IP 地址                      | 无            |
| port     | int    | 否       | 连接的端口号                          | 21114         |
| passwd   | string | 是       | Rcon 验证密码                         | 无            |
| cmd      | string | 否       | 要执行的 Rcon 命令                    | showserverinfo|

## 使用方法
### 示例请求
```
GET http://api.bctc-squad.cn:8088/api/Rcon.sh?ip=127.0.0.1&port=21114&passwd=yourpassword&cmd=yourcommand
```

### 示例响应
#### 对于 `showserverinfo` 命令（JSON 格式）
```json
Content-type: application/json

{
    "server_name": "我的服务器",
    "map": "示例地图",
    "players": 10,
    "max_players": 64,
    ...
}
```

#### 对于其他命令（纯文本格式）
```
Content-type: text/plain

命令执行成功。
```

## 错误响应
以下是一些可能的错误响应及其描述：

- **缺少必要的参数**：
  ```plaintext
  Content-type: text/plain
  
  缺少必要的参数。用法：
  http://api.bctc-squad.cn:8088/api/Rcon.sh?ip=IP地址&port=端口号&passwd=密码&cmd=命令
  ```

- **执行结果返回为空**：
  ```plaintext
  Content-type: text/plain
  
  执行结果返回为空，请检查您传入IP以及端口是否正确，或对端服务器能否被正确访问。
  ```

- **Rcon 密码错误**：
  ```plaintext
  Content-type: text/plain
  
  Rcon密码错误！
  ```

- **Rcon 访问被对端拒绝**：
  ```plaintext
  Content-type: text/plain
  
  Rcon访问被对端拒绝！
  ```

该文档提供了关于如何使用 Rcon API 的详细说明，包括可用的参数、示例请求和响应，以及可能的错误信息。
