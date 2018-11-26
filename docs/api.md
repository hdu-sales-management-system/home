# API

## 会员

### /login

POST

request:

```js
{
  username: [string],
  password: [string], // 加密过后的字符串
}
```

response:

返回 cookie

```js
{
  state: 'success'|'failed',
  message: [string],
}
```

### /gifts

GET

params

+ count 返回的数量，默认 10 条
+ offset 偏移量
+ tags[] 礼物所有的标签
+ categories[] 礼物所属的分类
+ filter 过滤器（待定）

### /tags

所有的标签

### categorise

GET:

所有分类

POST:

对于某一特定分类下的子分类通过 URL 附加一个`id`即可。

### /carousel

首页轮播图

```js
[
  {
    url: [string],
    title: [string],
    index: [number],
  },
  // ...
]
```

### /gifts/:id

#### GET

具体的礼品请求

返回一个礼品的所有必要信息，具体信息根据实际情况确定。

### /user/:user_id/cart[/:gift_id]

#### GET

购物车

#### POST

添加一个礼品到购物车

request:

```js
{
  // 礼品对象
}
```

#### PUT

更新一个礼品信息

DELETE 

从购物车中删除一个礼品**

### /users/:user_id/orders

#### GET

所有订单

### /buy/:order_id

这里通过`id`和`session`后端完成购买过程，返回购买结果。有鉴权动作。

```js
{
  state: 'success'|'failed',
  message: [string],
}
```

### /actives

#### GET

活动

### /search

搜索

request

params

+ count 返回的数量，默认 10 条
+ offset 偏移量，默认 10 条
+ q type: string 关键字

## 经销商

前缀: `/dealer`

>前缀也就是说下面的在所有的 URL ，都加上它。如，下面的`/gifts`，实际上的 URL 是：`/dealer/gifts`。

### /login

同上

### /gifts

#### GET

返回总公司已有的礼品，可以根据礼品状态，分类返回数据

request

params

+ status 商品状态
+ category 礼物所属的分类

#### DELETE

删除

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

前缀: `/admin`

### /gifts

#### GET

礼品列表

response:

```js
[
  {
    // 礼品信息
  }，
  // ...
]
```

#### POST

新建礼品

#### PUT

request:

```js
{
  id: [number], // 礼品 ID
  // 其他的礼品属性
}
```

更新礼品信息

### /actives

POST 创建活动

request:

```js
{
  // 活动信息
}
```

## 仓库

前缀:`/depot`

### /:id

指定仓库的信息

response:

```js
{
  // 仓库信息
}
```

### /gifts

#### GET

仓库拥有的礼品

request

params

+ count 返回的数量，默认 10 条
+ offset 偏移量，默认 10 条

```js
[
  {
    // 礼品对象
  }，
  // ...
]
```

#### POST

仓库进货

request:

```js
{
  // 礼品信息
}
```

#### PUT

request:

```js
{
  id: [number], // 仓库礼品 ID
  count: [number], // 礼品的库存量
  // 其他的礼品属性
}
```

#### DELETE

删除礼品