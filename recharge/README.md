# 充值公共域名
  domain : recharge-dev.36b.me
  
# 外部接口
## 1. 在线充值页面表单元素

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 用户ID | vUserId | 
| 玩家ID | iPlayerId |  
| 游戏ID | iGameId |  
| 区服ID | iWorldId  | 
| 充值数额 | iRmb  | 
| 元宝 | iGameCurrency |  
| 支付类型 |  payType  | 1. ALIPAY (支付宝) </br>2. WEICHAT (微信) |

## 2. 微信充值接口
### 扫码支付接口URL :
     https://domain/recharge/weichat/initOrder
#### 请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| iGameId | int | 必填 | 游戏ID |
| iWorldId | int | 必填 | 区服ID |
| vUserId | int | 必填 | 用户ID |
| iPlayerId | int | 必填 | 玩家ID |
| iRmb | int | 必填 | 充值金额 |
| iDiscount | int | 必填 | 折扣 |
| iGameCurrency | int | 必填 | 元宝 |

#### 返回结果

<pre>JSON示例</pre>
```
{
    "success": true,
    "status": 1,
    "msg": null,
    "data": {"result":null}
}
```

###订单查询接口URL:
    https://domain/recharge/weichat/queryOrder
#### 请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| vOrderNo | String | 必填 | 订单号 |

## 3. 支付宝充值接口
#### 扫码支付接口URL
     https://domain/recharge/alipay/initOrder
#### 请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| iGameId | int | 必填 | 游戏ID |
| iWorldId | int | 必填 | 区服ID |
| vUserId | int | 必填 | 用户ID |
| iPlayerId | int | 必填 | 玩家ID |
| iRmb | int | 必填 | 充值金额 |
| iDiscount | int | 必填 | 折扣 |
| iGameCurrency | int | 必填 | 元宝 |

#### 返回结果

<pre>JSON示例</pre>
```
{
    "success": true,
    "status": 1,
    "msg": null,
    "data": {"result":null}
}
```

## 4. 验证充值订单是否有效
#### URL
     https://domain/recharge/validateorder
#### 请求参数列表

|参数名称|参数类型|填写类型|参数说明|
|---- |---- |---- |---- |
|vOrderNo|String|必填|充值订单号|
|iGameID|int|必填|游戏ID|
|iWorldID|int|必填|区服ID|
|iUserId|String|必填|账号ID|
|iPlayerId|int|必填|角色ID|
|iGameCurrency|int|必填|元宝/钻石数量|
|其他公共字段|
|sign|String|必填|效验码</br>sha1(vOrderNo+iWorldID+iUserId+iPlayerId</br>+iGameCurrency+iGameID+time+salt)|
|time|long|必填|当前时间戳|

#### 返回字段说明

|参数名称|参数类型|参数说明
|---- |---- |---- |
公共字段|

#### 返回结果

<pre>JSON示例</pre>
```
{
    "success": true,
    "status": 1,
    "msg": null,
    "data": {}
}
```

## 充值公共信息
###充值订单表描述
|字段名称 |字段类型 |字段说明 |
|---- |---- |---- |
|`id` |int(11) | |
|`vOrderNo` |varchar(255) |订单编号 |
|`vUserIp` |varchar(255) |用户IP |
|`vUserId` |varchar(255) |用户ID |
|`iPlayerId` |int(11) |角色ID |
|`iRmb` |int(11) |充值的RMB |
|`iGameCurrency` |int(11) |游戏元宝/钻石 |
|`iDiscount` |int  |折扣 |
|`iGameId` |int(11) |游戏ID |
|`iWorldId` |int(11) |区ID |
|`bValidated` |tinyint(1) |是否已验证 |
|`bSuccess` |tinyint(1) |是否充值成功 |
|`dtCreateTime` |datetime |创建时间 |
|`dtUpdateTime` |datetime |更新时间 |




