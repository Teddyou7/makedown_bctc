### API 接口文档

#### 概述

此API提供了三个主要的端点，用于检索服务器信息、获取战斗列表和战斗详细信息。所有请求和响应均为JSON格式。

### 端点

#### 1. 检索服务器信息

- **URL:** `/userinfo/api?mode=retrieve_servers`
- **方法:** `GET`
- **请求参数:** 无
- **响应格式:**

```json
[
    "dnz1",
    "hongjing1",
    ...
]
```

- **说明:** 返回所有包含 `_combat_info` 表的服务器名称。

#### 2. 获取战斗列表

- **URL:** `/userinfo/api?mode=battle_list`
- **方法:** `GET`
- **请求参数:**

  | 参数名      | 类型   | 必填 | 示例值          | 描述                               |
  | ----------- | ------ | ---- | --------------- | ---------------------------------- |
  | steamid     | string | 是   | 76561199105097854 | 用户的 SteamID                      |
  | server      | string | 是   | dnz1            | 服务器名称                         |
  | data        | string | 是   | last_round      | 数据类型（`last_round`, `second_last_round`, `all_data`） |
  | limit       | int    | 否   | 200             | 返回的数据条数，默认 200，最大 2000 |
  | token       | string | 否   | xxx             | 预定义的令牌（当查询时间超过7天时需要） |
  | time        | int    | 否   | 3               | 查询最近几天的数据，默认3天 |

- **响应格式:**

```json
[
    {
        "id": 551942,
        "operator_steamid": "76561199105097854",
        "operator_nickname": " 雪狼001",
        "action": "ActualDamage",
        "target_steamid": "76561199105097854",
        "target_nickname": " 雪狼001",
        "weapon": "Soldier_RU_Marksman_Desert",
        "health": 135,
        "action_time": "2024-05-16 13:11:13.806"
    },
    ...
]
```

- **说明:** 返回匹配查询条件的战斗记录。

#### 3. 获取战斗详细信息

- **URL:** `/userinfo/api?mode=battle_details`
- **方法:** `GET`
- **请求参数:**

  | 参数名      | 类型   | 必填 | 示例值          | 描述                               |
  | ----------- | ------ | ---- | --------------- | ---------------------------------- |
  | steamid     | string | 是   | 76561199105097854 | 用户的 SteamID                      |
  | server      | string | 是   | dnz1            | 服务器名称                         |
  | data        | string | 是   | last_round      | 数据类型（`last_round`, `second_last_round`, `all_data`） |
  | limit       | int    | 否   | 200             | 返回的数据条数，默认 200，最大 2000 |
  | token       | string | 否   | xxx             | 预定义的令牌（当查询时间超过7天时需要） |
  | time        | int    | 否   | 3               | 查询最近几天的数据，默认3天 |

- **响应格式:**

```json
{
    "bayonet_kills": 0,
    "grenade_kills": 0,
    "light_rocket_kills": 0,
    "heavy_rocket_kills": 0,
    "explosive_kills": 0,
    "rifle_grenade_kills": 0,
    "rifle_kills": 0,
    "light_machine_gun_kills": 0,
    "universal_machine_gun_kills": 0,
    "precision_shooter_kills": 0,
    "pistol_kills": 0,
    "headshots": 0,
    "total_kills": 0,
    "total_deaths": 0,
    "total_hits": 0,
    "total_hits_taken": 0,
    "total_rescues": 0,
    "total_rescued": 0,
    "total_entries": 0,
    "headshot_rate": 0
}
```

### 字段说明

- `bayonet_kills`: 匕首击杀次数
- `grenade_kills`: 手榴弹击杀次数
- `light_rocket_kills`: 轻型火箭筒击杀次数
- `heavy_rocket_kills`: 重型火箭筒击杀次数
- `explosive_kills`: C4或IED击杀次数
- `rifle_grenade_kills`: 枪械榴弹击杀次数
- `rifle_kills`: 步枪击杀次数
- `light_machine_gun_kills`: 班用轻机枪击杀次数
- `universal_machine_gun_kills`: 通用机枪击杀次数
- `precision_shooter_kills`: 狙击枪击杀次数
- `pistol_kills`: 手枪击杀次数
- `headshots`: 爆头次数
- `total_kills`: 击杀总次数
- `total_deaths`: 阵亡总次数
- `total_hits`: 命中总次数
- `total_hits_taken`: 被命中总次数
- `total_rescues`: 救护总次数
- `total_rescued`: 被救护总次数
- `total_entries`: 数据条目总数
- `headshot_rate`: 爆头率
