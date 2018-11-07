# API

## 会员

### /login

###  /gifts
GET

params
+ count 
+ offset
+ tags[]
+ categories[]
+ filter
### /tags

所有的标签

### cateogries

所有分类

### /carousel

首页轮播图

###   /gifts/:id 

GET 具体的礼品请求

### /user/:user_id/cart[/:gift_id]

GET 购物车

POST 添加一个礼品到购物车

PUT 更新一个礼品信息

DELETE 从购物车中删除一个礼品

### /users/:user_id/orders

GET 所有订单

### /buy/:order_id

直接买

### /actives
GET 活动

### /search
搜索

## 经销商

前缀: `/dealer`

+ GET /login

### /gifts

GET 列表

params

+ status 商品状态

POST 
## 总公司

前缀: `/admin`

### /gifts

GET 礼品列表

POST 新建礼品

PUT 更新礼品信息

### /actives

POST 创建活动

## 仓库

前缀:`/depot`

### /:id

指定仓库的信息

### /gifts

GET 仓库拥有的礼品

POST

PUT 

DELETE