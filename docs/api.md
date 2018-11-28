# API

## 会员

### /login

####POST

用于用户登陆

#####request:

```js
{
  name: [string],
  password: [string] 
}
```

#####response:

````json
//if login sucessed
{
    "log_status": 1,
    "user_id": 1
}
//else
{
    "log_status": 0,
    "user_id": -1
}

````

### /logout

####GET

#####request:

none

#####response:

```json
//if logout succeed
{
    "IS_LOGOUT": 1
}
//else
{
    "IS_LOGOUT": 0
}

```

### /register

####POST

#####request

```js
{
  name: [string],
  password: [string], 
  address:[string],
  birthday:[Date],
  nickname:[string],
  gender:[Integer],
  phone:[string]
}
```

#####response

```json
//if register succeed
{
    "re_true": 1
}
//else
{
    "re_true": 0
}

```

### /user/:user_id
####GET

#####request:

none

#####response:
````json
//if succeed 
{
    "error": 0,
    "user": [
        {
            "model": "shopping.user",
            "pk": 1,
            "fields": {
                "name": "b",
                "password": "b",
                "address": "b",
                "birthday": "2000-01-01T00:00:00Z",
                "nickname": "b",
                "gender": 1,
                "phone": "122"
            }
        }
    ]
}
//else
{
    "error": 1
}
````

### /gifts

####GET

#####params

| name | comment |
| --- | --- |
| count | 返回的数量，默认 10 条 |
| offset | 偏移量 |
| tags[] | 礼物所有的标签 |
| categories[] | 礼物所属的分类 |
| filter | 过滤器（待定）|

#####response

```json
[
    {
        "model": "shopping.present",
        "pk": 1,
        "fields": {
            "name": "s",
            "on_date": "2018-01-01T00:00:00Z",
            "store_num": 10,
            "status": 1,
            "cost": "10.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": null
        }
    },
    {
        "model": "shopping.present",
        "pk": 2,
        "fields": {
            "name": "ss",
            "on_date": "2018-02-01T00:00:00Z",
            "store_num": 1,
            "status": 0,
            "cost": "10.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": null
        }
    }
]
```

### /tags
####GET
所有的标签

#####response

```json
[
    {
        "model": "shopping.tag",
        "pk": 1,
        "fields": {
            "name": "分类1",
            "hot": 0
        }
    },
    {
        "model": "shopping.tag",
        "pk": 2,
        "fields": {
            "name": "分类2",
            "hot": 0
        }
    }
]
```

### /categorise

####GET

所有分类

#####response

```json
[
    {
        "model": "shopping.category",
        "pk": 1,
        "fields": {
            "name": "1",
            "hot": 0,
            "categoryP": null
        }
    },
    {
        "model": "shopping.category",
        "pk": 2,
        "fields": {
            "name": "2",
            "hot": 0,
            "categoryP": 1
        }
    },
    {
        "model": "shopping.category",
        "pk": 3,
        "fields": {
            "name": "3",
            "hot": 0,
            "categoryP": 1
        }
    }
]
```
####POST:

#####request

```js
{
    id:[Integer]
}
```

#####response

```json
[
    {
        "model": "shopping.category",
        "pk": 1,
        "fields": {
            "name": "1",
            "hot": 0,
            "categoryP": null
        }
    }
```

### /carousel

首页轮播图

####GET

#####response

```json
[
    {
        "model": "shopping.crousel",
        "pk": 1,
        "fields": {
            "url": "www.ddd",
            "title": "title1",
            "index": 111
        }
    }
]
```

### /gifts/:id

#### GET

具体的礼品请求

返回一个礼品的所有必要信息，具体信息根据实际情况确定。
#####response
```json
//if succeed
{
    "gift_status": 1,
    "gift": [
        {
            "model": "shopping.present",
            "pk": 1,
            "fields": {
                "name": "s",
                "on_date": "2018-01-01T00:00:00Z",
                "store_num": 10,
                "status": 1,
                "cost": "10.00",
                "hot": 0,
                "off": 0,
                "off_cost": "0.00",
                "url": null
            }
        }
    ]
}
//else
{
    "gift_status": 0
}
```

### /user/:user_id/car

#### GET

购物车
#####response
```json
//if succeed
{
    "error": 0,
    "car": [
        {
            "url": null,
            "present_id": 1,
            "off_cost": 0,
            "store_num": 10,
            "status": 1,
            "on_date": "2018-01-01 00:00:00",
            "cost": 10,
            "hot": 0,
            "number": 1,//这个就是数量
            "name": "s",
            "off": 0
        }
    ]
}
//else
{
    "error": 1
}
```
#### POST

添加一个礼品到购物车

#####request:

```js
{
  present_id: [number],
  number: [number]
}
```
#####response
```json
//if succeed(也只有成功一种可能)
{
    "error": 0
}
```

#### PUT

更新一个礼品信息
#####request
```js
{
  present_id: [number],
  number: [number]
}
```
#####response
```json
{
    "error": 0
}
```

#### DELETE

从购物车中删除一个礼品
#####request
```js
{
  present_id: [number]
}
```
#####response
```json
//if succeed
{
    "error": 2
}
//else
{
    "error": 3
}
```

### /user/:user_id/orders

#### GET

获取所有订单

这里先不做分页

#####response
```json
{
    "error": 0,
    "car": [
        {
            "model": "shopping.order",
            "pk": 1,
            "fields": {
                "status": "创建成功",
                "receive_mark": 0,
                "user": 1,
                "logistics": "aaaaa",
                "begin_date": "2018-02-01T00:00:00Z",
                "sum_money": "40.00",
                "user_feedback": "null",
                "type": 0
            }
        },
        {
            "model": "shopping.order",
            "pk": 2,
            "fields": {
                "status": "操作成功",
                "receive_mark": 0,
                "user": 1,
                "logistics": "null",
                "begin_date": "2018-11-27T14:01:52.167Z",
                "sum_money": "30.00",
                "user_feedback": "null",
                "type": 0
            }
        },
        {
            "model": "shopping.order",
            "pk": 3,
            "fields": {
                "status": "操作成功",
                "receive_mark": 0,
                "user": 1,
                "logistics": "null",
                "begin_date": "2018-11-27T14:03:01.375Z",
                "sum_money": "50.00",
                "user_feedback": "null",
                "type": 0
            }
        },
        {
            "model": "shopping.order",
            "pk": 4,
            "fields": {
                "status": "操作成功",
                "receive_mark": 0,
                "user": 1,
                "logistics": "null",
                "begin_date": "2018-11-27T14:04:56.621Z",
                "sum_money": "50.00",
                "user_feedback": "null",
                "type": 0
            }
        }
    ]
}
```

### /user/:user_id/order/:order_id
获取某个特定的订单
####GET

####response
```json
//if succeed
{
    "error": 0,
    "car": [
        {
            "model": "shopping.oru",
            "pk": 2,
            "fields": {
                "count": 2,
                "price": "20.00",
                "order": 1,
                "present": 1
            }
        },
        {
            "model": "shopping.oru",
            "pk": 3,
            "fields": {
                "count": 2,
                "price": "20.00",
                "order": 1,
                "present": 2
            }
        }
    ]
}
//else
{
    "error": 1
}
```

### /buy

这里通过`id`和`session`后端完成购买过程，返回购买结果。有鉴权动作。
####POST
#####request
```json
{
  number:[list],
  present:[list]
}

```
#####response
```json
//if succeed
{
    "error": 0
}
//else
{
    "error": 1
}
```

<!-- ### /actives

#### GET

活动 -->

### /search

搜索
#### GET
#####request

params
| name | type | comment |
| --- | --- | --- |
| count | int | 返回的数量，默认 10 条 |
| offset| int | 偏移量 |
| q | string | 关键字

#####response
```json
[
    {
        "model": "shopping.present",
        "pk": 1,
        "fields": {
            "name": "s",
            "on_date": "2018-01-01T00:00:00Z",
            "store_num": 10,
            "status": 1,
            "cost": "10.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": null
        }
    },
    {
        "model": "shopping.present",
        "pk": 2,
        "fields": {
            "name": "ss",
            "on_date": "2018-02-01T00:00:00Z",
            "store_num": 1,
            "status": 0,
            "cost": "10.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": null
        }
    }
]
```

## 经销商

前缀: `/dealer`

>前缀也就是说下面的在所有的 URL ，都加上它。如，下面的`/gifts`，实际上的 URL 是：`/dealer/gifts`。

### /login

同上

### /gifts

#### GET

返回总公司已有的礼品，可以根据分类返回数据

request

params

| name | type | comment |
| --- | --- | --- |
| category | array \| string | 礼物所属的分类

### /purchase

#### POST

经销商批量性进货

request:

```js
[
  {
    id: [number], // 要买的礼品 ID
    count: [count], // 数量
  },
  // ...
]
```

response:

```js
{
  totalPrice: [number],
  giftCount: [number],
}
```

## 总公司

登录

### /login

#### POST

request:

```js
{
  name: [string],
  password: [string],
}
```

response:

```js
[
    //if login sucessed
    {
        "log_status": 1,
        "employee": [
            {
                "model": "warehouse.employee",
                "pk": 2,
                "fields": {
                    "empname": "小七",
                    "emppassword": "123",
                    "emporder": 1,
                    "empposit": "普通员工",
                    "empphone": "110"
                }
            }
        ]
    }
    //else
    {
        'log_status': 0,
    }
]
```

登出
### /logout

request:

none

response:

```js
//if login sucessed
{
    "IS_LOGOUT": 1
}
//else
{
    "IS_LOGOUT": 0
}
```

### /add

添加礼品

#### POST

request:

```js
{
  name:[string], //礼品名称
  introduction:[string], //礼品简介
  on_date:[date], //上架时间
  store_num:[int], //库存数量
  cost:[float], //礼品价格
  url:[string], //礼品图片
}
```

response:

```js
[
    //if success
    {
        "model": "warehouse.present",
        "pk": 17,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": "",
            "pdepot": 2
        }
    }
    //else:
    {
    "error": 1
    }
]
```

### /delete

删除礼品

#### DELETE

response:

```js
[
    //if success
    {
        "model": "warehouse.present",
        "pk": 15,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "",
            "pdepot": 2
        }
    }
    //else if login problem
    {
    "error": 1
    }
    //if id problem
    {
    "error": 2
    }
]
```

更新礼品信息（仓库管理员）

### /modify

#### PUT

request:

```js
{
  id:[int], //礼品ID
  name:[string], //礼品名称
  introduction:[string], //礼品简介
  on_date:[date], //上架时间
  store_num:[int], //库存数量
  cost:[float], //礼品价格
  url:[string], //礼品图片
}
```

response:

```js
[
    //if success
    {
        "model": "warehouse.present",
        "pk": 14,
        "fields": {
            "name": "商业礼品4",
            "introduction": "",
            "on_date": "2018-11-26T16:00:00Z",
            "store_num": 30,
            "status": 0,
            "cost": "30.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "123",
            "pdepot": 2
        }
    }
    //else if login problem
    {
    "error": 1
    }
    //if id problem
    {
    "error": 2
    }
]
```

### /gifts

返回礼品

#### GET

request:

none

response:

```js
[
    //if employee.emporder == 2
    {
        "model": "warehouse.present",
        "pk": 14,
        "fields": {
            "name": "商业礼品4",
            "introduction": "",
            "on_date": "2018-11-26T16:00:00Z",
            "store_num": 30,
            "status": 0,
            "cost": "30.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "123",
            "pdepot": 2
        }
    },
    {
        "model": "warehouse.present",
        "pk": 16,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "",
            "pdepot": 2
        }
    },
    {
        "model": "warehouse.present",
        "pk": 17,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": "",
            "pdepot": 2
        }
    }
    //if employee.emporder == 1
    {
        "model": "warehouse.present",
        "pk": 1,
        "fields": {
            "name": "商务礼品1",
            "introduction": "很棒",
            "on_date": "2018-11-26T00:00:00Z",
            "store_num": 20,
            "status": 2,
            "cost": "20.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": null,
            "pdepot": 1
        }
    },
    {
        "model": "warehouse.present",
        "pk": 14,
        "fields": {
            "name": "商业礼品4",
            "introduction": "",
            "on_date": "2018-11-26T16:00:00Z",
            "store_num": 30,
            "status": 0,
            "cost": "30.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "123",
            "pdepot": 2
        }
    },
    // ...
    //else
    {
    "error": 1
    }
]
```

### /sell

对礼品数据的修改,以及对礼品的查询（普通员工）

#### PUT

request:

```js
{
  id:[int], //礼品ID
  status:[int], //礼品状态（0：审核，1：上架，2：未上架）
  hot:[int], //礼品热度
  off:[int], //是否打折（0：否，1：是）
  off_cost:[float], //打折程度，数据应为长度3的小数，个位为0
}
```

response:

```js
[
    //if success
    {
        "model": "warehouse.present",
        "pk": 1,
        "fields": {
            "name": "商务礼品1",
            "introduction": "很棒",
            "on_date": "2018-11-26T00:00:00Z",
            "store_num": 20,
            "status": 1,
            "cost": "20.00",
            "hot": 90,
            "off": 0,
            "off_cost": "0.00",
            "url": null,
            "pdepot": 1
        }
    }
    //else if login problem
    {
    "error": 1
    }
    //if id problem
    {
    "error": 2
    }
]
```

#### GET

request:

```js
{
  depot_id:[int], //仓库ID
  present_status:[int], //礼品状态
}
```

response:

```js
[
    //if depot_id==2
    {
        "model": "warehouse.present",
        "pk": 14,
        "fields": {
            "name": "商业礼品4",
            "introduction": "",
            "on_date": "2018-11-26T16:00:00Z",
            "store_num": 30,
            "status": 0,
            "cost": "30.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "123",
            "pdepot": 2
        }
    },
    {
        "model": "warehouse.present",
        "pk": 16,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "",
            "pdepot": 2
        }
    },
    {
        "model": "warehouse.present",
        "pk": 17,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 0,
            "cost": "20.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": "",
            "pdepot": 2
        }
    }
    //if present_status==1
    {
        "model": "warehouse.present",
        "pk": 16,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 2,
            "cost": "20.00",
            "hot": 0,
            "off": 1,
            "off_cost": "0.21",
            "url": "",
            "pdepot": 2
        }
    },
    {
        "model": "warehouse.present",
        "pk": 17,
        "fields": {
            "name": "礼品1",
            "introduction": "厉害",
            "on_date": "2018-11-25T16:00:00Z",
            "store_num": 20,
            "status": 2,
            "cost": "20.00",
            "hot": 0,
            "off": 0,
            "off_cost": "0.00",
            "url": "",
            "pdepot": 2
        }
    }
    //else
    {
    "error": 1
    }
]
```
