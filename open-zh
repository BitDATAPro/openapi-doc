# BiKi Open API

简体中文 | [English](./README.us-en.md)

- [**入门指引**](#入门指引)

  - [**创建API Key**](#创建api-key)
  - [**接口调用方式说明**](#接口调用方式说明)
  - [**服务器**](#服务器)

- [**REST API**](#rest-api)

  - [**接入 URL**](#接入-url)
  - [**请求交互**](#请求交互)
  - [**签名认证**](#签名认证)
  - [**REST API列表**](#rest-api列表)
  - [**查询系统支持的所有交易对及精度**](#查询系统支持的所有交易对及精度)
  - [**获取所有交易对行情**](#获取所有交易对行情)
  - [**获取各个币对最新成交价**](#获取各个币对最新成交价)
  - [**获取指定币对当前行情**](#获取指定币对当前行情)
  - [**获取K线数据**](#获取k线数据)
  - [**获取买卖盘深度**](#获取买卖盘深度)
  - [**获取资产余额**](#获取资产余额)
  - [**获取当前委托**](#获取当前委托)
  - [**获取全部委托**](#获取全部委托)
  - [**获取订单详情**](#获取订单详情)
  - [**创建订单**](#创建订单)
  - [**取消委托单**](#取消委托单)

- [**Websocket API**](#websocket-api)

  - [**接入 URL**](#host-url)
  - [**请求交互**](#请求交互)
  - [**订阅实时成交信息**](#订阅实时成交信息)
  - [**订阅深度盘口**](#订阅深度盘口)
  - [**订阅K线数据**](#订阅k线数据)

## 入门指引

**欢迎使用开发者文档，bitdata提供了简单易用的API接口，通过API可以获取市场行情数据、进行交易、管理订单**

### 创建API Key

邮箱：bd@bitdata.pro  说明用途 进行申请
> **请不要泄露Secret Key信息，以免造成资产损失,建议用户为API绑定IP地址**

### 接口调用方式说明

**bitdata提供两种调用接口方式，用户可根据使用场景和偏好选择适合自己的方式来调用。**

- REST API

  提供行情查询、余额查询、币币交易、订单管理功能，建议用户使用REST API进行账户余额查询、币币交易及订单管理等操作

- Websocket API

  提供市场行情、买卖深度、实时成交信息，建议用户使用Websocket API获取市场行情类信息

<br>

## REST API

### 接入 URL

- **[https://open.bitdata.com](https://open.bitdata.com) [推荐]**

### 请求交互

#### 介绍

REST API 提供行情查询、余额查询、币币交易、订单管理功能

所有请求基于Https协议，请求头信息中content-type需要统一设置为表单格式:

- **content-type:application/x-www-form-urlencoded**

#### 状态码

code 200 成功  其余都是失败

### 签名认证

#### 签名说明

API 请求在通过网络传输的过程中极有可能被篡改，为了确保请求未被更改，所有接口必须使用您的 secret_key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。

#### 签名步骤

get 参数参与签名，post参数不参与签名认证比填写参数
-  (1) 必填字段 timestamp:当前时间戳  apikey:用户key 
-  (2) 根据参数得key 进行ASCII码顺序进行排序。
-  (3) 对参数进行拼接比如 a=1&b=2&c=3
-  (4) 将生成的字符串与api私钥做为参数调用HmacSHA256哈希函数获得哈希值，
-  (5) 最后signature=(4) 加入到url 里面

php 例子：
```php
<?php
 $data = ["apikey" => "apikey", "timestamp"  =>  now()];
 ksort($data);
 $query = http_build_query($params);
 $signature = hash_hmac('sha256', $query, $this->userInfo['secret_key']); 
?>
```



### REST API列表

API                                              |  说明
------------------------------------------------ |  ---------------
[GET /market/symbols](#查询系统支持的所有交易对及精度) |  查询系统支持的所有交易对及精度
[GET /market/list](#获取所有交易对行情)       | 获取所有交易对行情
[GET /market/price-all](#获取各个币对的最新成交价)           | 获取各个币对的最新成交价
[GET /market/info](#获取指定币对当前行情)            | 获取指定币对当前行情
[GET /market/line](#获取K线数据)              | 获取K线数据
[GET /market/dept](#获取买卖盘深度)       | 获取买卖盘深度
[GET /user/balance](#获取资产余额)           | 获取资产余额
[GET /order/list](#获取当前委托或全部委托)              | 获取当前委托或全部委托
[GET /order/detail](#获取订单详情)                | 获取订单详情
[POST /order/create](#创建订单)           |  创建订单
[POST /order/cancel](#取消委托单)           | 取消委托单

### 查询系统支持的所有交易对及精度

#### GET [/market/symbols]

#### 输入参数: 无

#### 返回示例:

```
{
    'status':200,
    'code':0,
    'message': "success",
    'data': {
        'list':[
            {
                'base_currency':"BTC",//基础币
                'quote_currency':"USDT",//计价币
                'symbol': "BTC-USDT",//交易对
                'is_support_stop_limit': true,//是否支持止盈止损
                'price_precision': 1,//价格精度
                'amount_precision': 6,//数量精度
                'min_order_amt': "0.001",//最小挂单量
                'min_order_value': "10.00",//最小挂单额
                'status': "online"//状态
            },
            {
                'base_currency': "ETH",
                'quote_currency': "USDT",
                'symbol': "ETH-USDT",
                'is_support_stop_limit': true,
                'price_precision': 2,
                'amount_precision': 4,
                'min_order_amt': "0.001",
                'min_order_value': "10.00",
                'status': "online"
            },
        ]
    }
}
```

### 获取所有交易对行情

#### GET [/market/list]

#### 输入参数: 无


#### 返回示例:

```python
{
  "status": 200,
  "code": 0,
  "message": "success",
  "data": [{
    "buy": 111, //买1
    "sell": 22, //卖1
    "symbol": "DDAM-USDT", //配对
    "high": 0.01, //最高价
    "vol": 1468201, //成交量
    "last": 0.0087, //最新价
    "low": 0.0082, //最低价
    "change": -11.22,//涨跌幅
    "rose": 0.0087 //涨跌比
  }]
}
```

### 获取各个币对最新成交价

#### GET [/market/price-all]

#### 输入参数: 无


#### 返回示例:

```python
{
    "status": 200,
    "code": 0,
    "message": "success",
    "data": {
        "BDT-USDT": "0.033358531887466646",
        "BTC-USDT": "11735.358977320047",
        "EOS-BTC": "3.1926928552906544",
        "ETH-USDT": "389.7322956286041",
        "ETH-BTC": "395.2097568531904",
        "XRP-BTC": "0.30127377345186107",
        "XRP-ETH": "0.30227162486732795",
        "XRP-USDT": "0.29770663595506375",
        "BCH-BTC": "301.29813279391743",
        "BCH-USDT": "296.4067069406598",
        "LTC-USDT": "57.71297590815923",
        "LTC-ETH": "58.63137862146134",
        "LTC-BTC": "58.48261262270383",
        "BNB-BTC": "22.49385089956827",
        "BNB-ETH": "22.25178292335382",
        "BNB-USDT": "22.22232915109006",
    }
}
```

### 获取指定币对当前行情

#### GET [/market/info]

#### 输入参数:

参数名称   | 是否必须 | 数据类型   | 描述  | 取值范围
------ | ---- | ------ | --- | -----------------------------
symbol | true | string | 交易对 | ddam-usdt

#### 返回示例:

```python
{
	"status": 200,
	"code": 0,
	"message": "success",
	"data":[{
			"OKB-BTC": 5.760656 //币- 最新价
		}]

}
```


### 获取K线数据

#### GET [/market/line]

#### 输入参数:

参数名称   | 是否必须 | 数据类型   | 描述                        | 取值范围
------ | ---- | ------ | ------------------------- | -----------------------------
symbol | true | string | 交易对                       | ddam-usdt
period | true | number | K线周期 单位为分钟,1代表1分钟 1天为1440 | 1m 15m  1h  1d   获取多久得行情


#### 返回示例:

```python
{
  "status": 200,
  "code": 0,
  "message": "success",
  "data": {
    "fields": [
      "time", //时间
      "open", //开盘价
      "close",//收盘价
      "low", //最低价
      "high",//最高价
      "volume"//成交量
    ],
    "values": [
        [
            1595977200,
            "0.032251",
            "0.032273",
            "0.03222",
            "0.032273",
            "39102.00"
        ],
        [
            1595980800,
            "0.032257",
            "0.032235",
            "0.032224",
            "0.032282",
            "299901.00"
        ],
        [
            1595984400,
            "0.032244",
            "0.032252",
            "0.03216",
            "0.0323",
            "328776.00"
        ],
    ]
  }
}
```

### 获取买卖盘深度

#### GET [/market/dept]

#### 输入参数:

参数名称   | 是否必须 | 数据类型   | 描述                      | 取值范围
------ | ---- | ------ | ----------------------- | -----------------------------
symbol | true | string | 交易对                     | 	btc-usdt
type   | true | string | 深度 | 支持5和10   不填默认为5


#### 返回示例:

```python
{
    'status':200,
    'code':0,
    'message': "success",
    'data': {
            'bids':[//卖单
                [
                "11154.48",//价格
                "2.703338"//数量
                ],
                [
                "11154.43",
                "0.425628"
                ],
                [
                "11154.24",
                "0.008848"
                ],
                [
                "11154.11",
                "0.014589"
                ],
                [
                "11153.96",
                "0.156964"
                ]
            ],
            'asks':[//买单
                [
                "11151.9",//价格    
                "1.73709396"//数量
                ],
                [
                "11152.4",
                "0.5"
                ],
                [
                "11152.6",
                "0.03018122"
                ],
                [
                "11152.94",
                "0.02176891343448454"
                ],
                [
                "11152.95",
                "0.12"
                ]
        ]
    }
}
```

### 获取资产余额

#### GET [/user/balance]


#### 返回示例:

```python
{
    "status": 200,
    "code": 0,
    "message": "success",
    "data": [
        {
            "coin": "BDT",    //币种
            "freeze": "150",   //冻结
            "balance": "100005.09514946"  //余额
        },
        {
            "coin": "ETH",
            "freeze": "0",
            "balance": "4.99505"
        }
    ],
}
```

### 获取委托

#### GET [/order/list]


#### 输入参数:

参数名称     | 是否必须  | 数据类型   | 描述         | 取值范围
-------- | ----- | ------ | ---------- | ----
pageSize | false | string | 每页数据数      |
page     | false | string | 页码         |
symbol   | true  | string | 币对         |
action   | true  |  int   |  委托类型   | 1当前委托  2所有委托

#### 返回示例:

```python
{
  "status": 200,
  "code": 0,
  "message": "success",
  "data": {
      "list":[
          {
                "order_id": "201910241622591738949826",
                "amount": "0.001000000000000",
                "price": "7406.700000000000000",
                "vol": "0.000000000000000",
                "field_amount": "0.000000000000000",
                "avg_price": "0.000000000000000",
                "fee": "0.000000000000000",
                "side": "buy",
                "status": "cancelled",
                "created_at": "2019-10-24 08:23:00",
                "updated_at": "2020-08-03 07:51:41",
                "symbol": "BTC-USDT",
                "trigger_condition": "",
                "type": "limit",
                "finished_at": "2020-08-03 07:51:41"
          },
          {
                "order_id": "201910241622591738949826",
                "amount": "0.001000000000000",
                "price": "7406.700000000000000",
                "vol": "0.000000000000000",
                "field_amount": "0.000000000000000",
                "avg_price": "0.000000000000000",
                "fee": "0.000000000000000",
                "side": "buy",
                "status": "cancelled",
                "created_at": "2019-10-24 08:23:00",
                "updated_at": "2020-08-03 07:51:41",
                "symbol": "BTC-USDT",
                "trigger_condition": "",
                "type": "limit",
                "finished_at": "2020-08-03 07:51:41"
          }
       ],
    "pagination": {
        "page": 1,  //当前几页
        "pageSize": 20,  //每页多少条
        "totalRaws": 26,  //总用多少条
        "totalPage": 2    //总用多少页
    }
  }
}
```

### 获取订单详情

#### GET [/order/detail]

#### 输入参数:

参数名称     | 是否必须 | 数据类型   | 描述         | 取值范围
-------- | ---- | ------ | ---------- | ----
order_id | true | string | 订单号        |


#### 返回示例:

```python
{
  "status": 200,
  "code": 0,
  "message": "success",
  "data": {
    "order_id": "201910241622591738949826",
    "amount": "0.001000000000000",
    "price": "7406.700000000000000",
    "vol": "0.000000000000000",
    "field_amount": "0.000000000000000",
    "avg_price": "0.000000000000000",
    "fee": "0.000000000000000",
    "side": "buy",
    "status": "cancelled",
    "created_at": "2019-10-24 08:23:00",
    "updated_at": "2020-08-03 07:51:41",
    "symbol": "BTC-USDT",
    "trigger_condition": "",
    "type": "limit",
    "finished_at": "2020-08-03 07:51:41"
  }
}
```

### 创建订单

#### POST [/order/create]


#### 输入参数:

参数名称    | 是否必须  | 数据类型   | 描述             | 取值范围
------- | ----- | ------ | -------------- | ------------------------------------
side    | true  | string | 买卖方向           | BUY/SELL
type    | true  | string | 挂单类型           | 交易类型（limit 限价 market 市价 stop-limit 止盈止损）
amount  | true  | string | 购买数量(多义, 复用字段) | 订单交易量（市价买单此字段为订单交易额）
price   | false | string | 委托单价           | 
symbol  | true  | string | 币对             |
time    | true  | string | 时间戳            |
sign    | true  | string | 签名             |



#### 返回示例:

```python
{
    "status": 200,
    "code": 0,
    "message": "success",
    "data": {
        "order_id": "202008051739201020469932"
    }
}
```

### 取消委托单

#### POST [/order/cancel]

#### 输入参数:

参数名称     | 是否必须 | 数据类型   | 描述         | 取值范围
-------- | ---- | ------ | ---------- | ----
contents | true | string |  订单号列表 |  42040201,421421,421421|BTC-USDT |  1 就是订单号逗号隔开，2是交易对
type     | true | int    |  | 1为根据订单 取消 2为根据交易对进行取消 

#### 返回示例:

```python
{
    "status": 200,
    "code": 0,
    "message": "success",
    "data": {}
}
```

## Websocket API

### 接入 URL

#### [wss://ws.biki.com/kline-api/ws]((https://www.biki.com)) [推荐]

#### [wss://ws.bikicoin.pro/kline-api/ws](https://www.biki.com)

### 请求交互

#### 数据压缩

- WebSocket API 返回的所有数据都进行了 GZIP 压缩，需要客户端在收到数据之后解压

#### 心跳消息

- 当用户的Websocket客户端连接到Websocket服务器后，服务器会定期向其发送ping消息并包含一整数值如下： {"ping": 156200607000}

- 当用户的Websocket客户端接收到此心跳消息后，应返回pong消息并包含同一整数值： {"pong": 156200607000}

> 当Websocket服务器连续多次发送了`ping`消息却没有收到任何一次`pong`消息返回后，服务器将主动断开与此客户端的连接

### 订阅实时成交信息

#### 连接成功后发送请求:

```python
{
    "event": "sub",
    "params": {
        "channel": "market_$base$quote_trade_ticker",
        "cb_id": "自定义"
    }
}
```

> 其中$base$quote 为交易对信息<br>
> channel 示例 "channel": "market_btcusdt_trade_ticker"

#### 返回订阅成功消息

```python
{
    "event_rep": "subed",
    "channel": "market_$base$quote_trade_ticker",
    "cb_id": "原路返回",
    "ts": 1506584998239,
    "status": "ok"
}
```

#### 每当有新的成交信息后，服务器端自动推送消息如下:

```python
{
    "channel":"market_$base$quote_trade_ticker", // 订阅的交易对行情channel
    "ts":1506584998239,                         // 请求时间
    "tick":{
        "id":12121,                             // data中最大交易ID
        "ts":1506584998239,                     // data中最大时间
        "data":[
            {
                "id":12121,                     // 交易ID
                "side":"buy",                   // 买卖方向buy,sell
                "price":32.233,                 // 单价
                "vol":232,                      // 数量
                "amount":323,                   // 总额
                "ts":1506584998239,             // 数据产生时间
                "ds":'2017-09-10 23:12:21'
            },
            {
                "id":12120,                     // 交易ID
                "side":"buy",                   // 买卖方向buy,sell
                "price":32.233,                 // 单价
                "vol":232,                      // 数量
                "amount":323,                   // 总额
                "ts":1506584998239,             // 数据产生时间
                "ds":'2017-09-10 23:12:21'
            }
        ]
    }
}
```

### 订阅深度盘口

#### 连接成功后发送请求:

```python
{
    "event": "sub",
    "params": {
        "channel": "market_$base$quote_depth_step[0-2]",
        "cb_id": "自定义",
        "asks": 150,
        "bids": 150
    }
}
```

> $base$quote表示btcusdt等币对,step[0-2]表示深度有3个维度，0、1、2<br>
> channel 示例 "channel": "market_btcusdt_depth_step0"

#### 返回订阅成功消息

```python
{
    "event_rep": "subed",
    "channel": "market_$base$quote_depth_step[0-2]",
    "cb_id": "原路返回",
    "asks": 150,
    "bids": 150,
    "ts": 1506584998239,
    "status": "ok"
}
```

#### 每当深度数据有更新时，服务器端自动推送消息如下:

```python
{
    "channel": "market_$base$quote_depth_step[0-2]",
    "ts": 1506584998239,
    "tick": {
        "asks": [
            [22112.22,0.9332],      // 价格，数量
            [22112.21,0.2]
        ],
        "buys": [
            [22111.22,0.9332],
            [22111.21,0.2]
        ]
    }
}
```

### 订阅K线数据

#### 连接成功后发送请求:

```python
{
    "event": "sub",
    "params": {
        "channel": "market_$base$quote_kline_[1min/5min/15min/30min/60min/1day/1week/1month]",
        "cb_id": "自定义"
    }
}
```

> channel 示例 "channel": "market_btcusdt_kline_1min"

#### 返回订阅成功消息

```python
{
    "event_rep": "subed",
    "channel": "market_$base$quote_kline_[1min/5min/15min/30min/60min/1day/1week/1month]",
    "cb_id": "原路返回",
    "ts": 1506584998239,
    "status": "ok"
}
```

#### 每当K线数据更新时，服务器端自动推送消息如下:

```python
{
    "channel": "market_$base$quote_kline_[1min/5min/15min/30min/60min/1day/1week/1month]",
    "ts": 1506584998239,
    "tick": {
        "id": 1506602880,
        "amount": 123.1221,
        "vol": 1212.12211,
        "open": 2233.22,
        "close": 1221.11,
        "high": 22322.22,
        "low": 2321.22
    }
}
```

[^_^]: aadf4
