## 冲锋衣战术分综合评估系统接口文档

### 基本信息
- **URL**:

 `https://bctc-squad.cn/api`
- **方法**: `GET`
- **响应格式**: `JSON`

### 参数说明

#### 公共参数
- `mode`: 请求模式，决定查询的类型。可选值：
  - `overall`: 获取总排名
  - `steamid`: 根据SteamID查询
  - `nickname`: 根据昵称查询
  - `realtime`: 实时数据查询
- `token`: （可选）用于请求超过默认数量限制时的身份验证令牌
- `sort`: 排序方法。可选值：
  - `asc`: 升序（默认）
  - `desc`: 降序

#### 总排名模式
- **请求路径**: `https://bctc-squad.cn/api?mode=overall&count=<数量>&sort=<排序方法>&token=<令牌>`
- **特定参数**:
  - `count`: （可选）返回记录数量，默认为200，超过500需要提供令牌。

#### SteamID查询模式
- **请求路径**: `https://bctc-squad.cn/api?mode=steamid&steamid=<SteamID>&match_mode=<匹配模式>&count=<数量>&sort=<排序方法>&token=<令牌>`
- **特定参数**:
  - `steamid`: 需要查询的SteamID
  - `match_mode`: （可选）匹配模式。可选值：
    - `exact`: 精确匹配（默认）
    - `fuzzy`: 模糊匹配
  - `count`: （可选）返回记录数量，默认为10，超过100需要提供令牌。

#### 用户昵称查询模式
- **请求路径**: `https://bctc-squad.cn/api?mode=nickname&nickname=<昵称>&match_mode=<匹配模式>&count=<数量>&sort=<排序方法>&token=<令牌>`
- **特定参数**:
  - `nickname`: 需要查询的用户昵称
  - `match_mode`: （可选）匹配模式。可选值：
    - `exact`: 精确匹配（默认）
    - `fuzzy`: 模糊匹配
  - `count`: （可选）返回记录数量，默认为10，超过100需要提供令牌。

#### 实时数据查询模式
- **请求路径**: `https://bctc-squad.cn/api?mode=realtime&steamid=<SteamID>&sort=<排序方法>`
- **特定参数**:
  - `steamid`: 需要查询的SteamID

### 响应格式

所有模式下的响应格式为JSON，具体字段如下：

- `SteamID`: 玩家SteamID
- `NickName`: 玩家昵称
- `SeasonRating`: 赛季评分
- `SeasonRanking`: 赛季排名
- `DataTime`: 数据时间（仅实时数据查询模式）

#### 示例响应
```
[
    {
        "SteamID": "76561198000000000",
        "NickName": "Player1",
        "SeasonRating": 1500.0,
        "SeasonRanking": 1,
        "DataTime": "2024-05-16 03:03:30"
    },
    {
        "SteamID": "76561198000000001",
        "NickName": "Player2",
        "SeasonRating": 1450.0,
        "SeasonRanking": 2,
        "DataTime": "2024-05-16 03:03:30"
    }
]
```

### 示例请求

#### 获取总排名
```
curl -X GET "https://bctc-squad.cn/api?mode=overall&count=100&sort=asc"
```

#### 根据SteamID查询
```
curl -X GET "https://bctc-squad.cn/api?mode=steamid&steamid=76561198000000000&match_mode=exact&count=10&sort=asc"
```

#### 根据用户昵称查询
```
curl -X GET "https://bctc-squad.cn/api?mode=nickname&nickname=Player1&match_mode=exact&count=10&sort=asc"
```

#### 实时数据查询
```
curl -X GET "https://bctc-squad.cn/api?mode=realtime&steamid=76561198000000000"
```

### 错误响应
当请求参数不正确或发生错误时，API会返回错误信息，格式如下：

#### 示例错误响应
```
{
    "error": "请求超过500条记录需要提供令牌"
}
```

### 注意事项

- 所有请求的排序方法都是基于玩家的得分排名。
- 适当使用令牌以请求超过默认数量的记录。
- `mode`参数决定了API的查询类型，不同模式下需要提供相应的特定参数。
