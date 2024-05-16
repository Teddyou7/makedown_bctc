以下是完整的API文档，包括`retrieve_servers`、`battle_list`和`battle_details`模式的说明、请求参数及响应内容的详细说明。

## API文档

### 基础信息
- **URL**: `/userinfo/api`
- **方法**: `GET`
- **支持的模式**: `retrieve_servers`, `battle_list`, `battle_details`

### 请求模式

#### 1. 检索服务器 (`retrieve_servers`)

##### 请求
- **模式**: `retrieve_servers`
- **请求参数**: 无

##### 响应
- **响应内容**: 服务器名称列表

```json
[
    "server1",
    "server2",
    ...
]
```

#### 2. 战斗列表 (`battle_list`)

##### 请求
- **模式**: `battle_list`
- **请求参数**:
  - `steamid` (必需): 用户的Steam ID
  - `server` (必需): 服务器名称
  - `data` (必需): 数据类型 (`last_round`, `second_last_round`, `all_data`)
  - `limit` (可选): 返回数据条目数，默认200，最大值200
  - `token` (可选): 用于请求超过7天的数据
  - `time` (可选): 天数范围，默认为3天

##### 响应
- **响应内容**: 包含各种击杀和统计数据的JSON对象

```json
{
    "bayonet_kills": 3,
    "grenade_kills": 0,
    "light_rocket_kills": 0,
    "heavy_rocket_kills": 0,
    "explosive_kills": 0,
    "rifle_grenade_kills": 0,
    "rifle_kills": 8,
    "light_machine_gun_kills": 49,
    "universal_machine_gun_kills": 1,
    "precision_shooter_kills": 51,
    "pistol_kills": 3,
    "headshots": 10,
    "total_actual_damage_hits": 102,
    "total_deaths": 15,
    "total_hits_taken": 15,
    "total_rescues": 3,
    "total_rescued": 2,
    "total_entries": 200,
    "total_kills": 50,
    "other_kills": 30,
    "headshot_rate": 0.09803921568627451
}
```

##### 响应字段翻译
- **bayonet_kills**: 匕首击杀次数
- **grenade_kills**: 手榴弹击杀次数
- **light_rocket_kills**: 轻型火箭筒击杀次数
- **heavy_rocket_kills**: 重型火箭筒击杀次数
- **explosive_kills**: 爆炸物击杀次数（如C4或IED）
- **rifle_grenade_kills**: 枪械榴弹击杀次数
- **rifle_kills**: 步枪击杀次数
- **light_machine_gun_kills**: 轻机枪击杀次数
- **universal_machine_gun_kills**: 通用机枪击杀次数
- **precision_shooter_kills**: 狙击枪击杀次数
- **pistol_kills**: 手枪击杀次数
- **headshots**: 爆头次数
- **total_actual_damage_hits**: 实际伤害命中总次数
- **total_deaths**: 阵亡总次数
- **total_hits_taken**: 被命中总次数
- **total_rescues**: 救护总次数
- **total_rescued**: 被救护总次数
- **total_entries**: 数据条目总数
- **total_kills**: 总击杀次数
- **other_kills**: 其他击杀次数
- **headshot_rate**: 爆头率（爆头次数/实际伤害命中总次数）

#### 3. 战斗详细 (`battle_details`)

##### 请求
- **模式**: `battle_details`
- **请求参数**:
  - `steamid` (必需): 用户的Steam ID
  - `server` (必需): 服务器名称
  - `data` (必需): 数据类型 (`last_round`, `second_last_round`, `all_data`)
  - `limit` (可选): 返回数据条目数，默认200，最大值200
  - `token` (可选): 用于请求超过7天的数据
  - `time` (可选): 天数范围，默认为3天

##### 响应
- **响应内容**: 包含各种击杀和统计数据的JSON对象，结构与 `battle_list` 模式相同

### 错误响应
- **错误响应**: JSON对象，包含错误信息

```json
{
    "error": "Invalid mode"
}
```
- **错误类型**:
  - `Invalid mode`: 非法的请求模式
  - `Token required for data older than 7 days`: 请求超过7天的数据需要提供有效的token
  - `Invalid data type`: 非法的数据类型

### 示例请求
- **检索服务器**:
  ```
  GET /userinfo/api?mode=retrieve_servers
  ```

- **战斗列表**:
  ```
  GET /userinfo/api?mode=battle_list&steamid=76561198390104346&server=qingya1&data=all_data&limit=100&time=7
  ```

- **战斗详细**:
  ```
  GET /userinfo/api?mode=battle_details&steamid=76561198390104346&server=qingya1&data=last_round&limit=50
  ```

### 运行代码
确保Flask应用在指定端口运行，默认端口为4599：

```python
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=4599)
```

这份API文档涵盖了`retrieve_servers`、`battle_list`和`battle_details`模式的请求和响应详细信息，帮助开发者正确使用API并理解各字段的含义。
