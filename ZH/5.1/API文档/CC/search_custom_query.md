
### 请求地址

/api/c/compapi/v2/cc/search_custom_query/



### 请求方法

POST


### 功能描述

查询自定义api

### 请求参数


#### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用ID -&gt; 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| bk_supplier_account | string     | 否     | 开发商账号 |
| bk_biz_id |  int     | 是     | 业务ID |
| condition |  dict    | 否     | 查询条件，condition 字段为自定义api的属性字段, 可以是create_user,modify_user, name |
| start     |  int     | 是     | 记录开始位置 |
| limit     |  int     | 是     | 每页限制条数,最大200 |

### 请求参数示例

```python
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_supplier_account": "123456789",
    "bk_biz_id": 1,
    "condition": {
        "name": "api1"
    },
    "start": 0,
    "limit": 200
}
```

### 返回结果示例

```python

{
    "result": true,
    "code": 0,
    "message": "",
    "data": {
        "count": 1,
        "info": [
            {
                "bk_biz_id": 1,
                "id": "bacfet4kd42325venmcg",
                "name": "api1",
                "info": "{\"condition\":[{\"bk_obj_id\":\"biz\",\"condition\":[{\"field\":\"default\",\"operator\":\"$ne\",\"value\":1}],\"fields\":[]},{\"bk_obj_id\":\"set\",\"condition\":[],\"fields\":[]},{\"bk_obj_id\":\"module\",\"condition\":[],\"fields\":[]},{\"bk_obj_id\":\"host\",\"condition\":[{\"field\":\"bk_host_innerip\",\"operator\":\"$eq\",\"value\":\"127.0.0.1\"}],\"fields\":[\"bk_host_innerip\",\"bk_host_outerip\",\"bk_agent_status\"]}]}",
                "create_user": "admin",
                "create_time": "2018-03-27T16:22:43.271+08:00",
                "modify_user": "admin",
                "last_time": "2018-03-27T16:29:26.428+08:00"
            }
        ]
    }
}
```

### 返回结果参数说明

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| result    | bool      | 请求成功与否，true:请求成功，false:请求失败 |
| code      | string    | 组件返回错误编码，0表示success，>0表示失败错误 |
| message   | string    | 请求失败返回的错误消息 |
| data      | object    | 请求返回的数据 |

#### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| count     | int          | 记录条数 |
| info      | array        | 自定义api数据 |

#### data.info

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| bk_biz_id    | int          | 业务ID |
| create_time  | string       | 创建时间 |
| create_user  | string       | 创建者 |
| id           | string       | 自定义api主键ID |
| info         | string       | 自定义api信息 |
| last_time    | string       | 更新时间 |
| modify_user  | string       | 修改者 |
| name         | string       | 自定义api命名 |

#### data.info.info

| 字段      |  类型     |  描述      |
|-----------|------------|--------------------|
| bk_obj_id |  string   | 对象名,可以为biz,set,module,host,object |
| fields    |  array    | 查询输出字段 |
| condition |  array    | 查询条件 |

#### data.info.info.condition

| 字段      |  类型     |  描述      |
|-----------|------------|--------------------|
| field     |  string    | 对象的字段 |
| operator  |  string    | 操作符, $eq为相等，$neq为不等，$in为属于，$nin为不属于 |
| value     |  string    | 字段对应的值 |
