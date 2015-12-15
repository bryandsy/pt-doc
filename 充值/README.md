#平台游戏充值流程
##平台充值介绍
> 进入平台首页选择充值功能，进入充值流程（必须检测是否登陆）,如下示例页面
<p><img  alt="platform" src="https://github.com/szmolin/pt-doc/blob/master/%E5%85%85%E5%80%BC/game_platform_index.jpg" title="platform" height="475" width="583"><img alt="recharge" src="https://github.com/szmolin/pt-doc/blob/master/%E5%85%85%E5%80%BC/game_recharge_form.jpg" title="recharge" height="475" width="583"> </p>


## 充值表单必须的参数

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 用户ID | vUserId | 
| 玩家ID | iPlayerId |  
| 游戏ID | iGameId |  
| 区服ID | iWorldId  | 
| 充值数额 | iRmb  | 
| 元宝 | iGameCurrency |  
| 支付类型 |  payType  | 1. ALIPAY (支付宝) </br>2. WEICHAT (微信) |

##平台充值
+ 充值URL：

  * 支付宝
    * https://recharge-url/recharge/alipay/initOrder
  * 微信
    * https://recharge-url/recharge/weichat/initOrder

>  以微信示例：

- 充值URL示例

_页面需 增加payType字段，以支持支付类型URL选择_
* 
   * https://recharge-url/recharge/weichat/initOrder?function=jQuery18106264256320428103_1445247783992&iGameId=1&iWorldId=1&vUserId=47502ea6-d2be-4f52-bf12-9b0652a0409c&iPlayerId=-1&iRmb=10&iDiscount=1&iGameCurrency=100&_=1445247788405
  
-  返回结果

   * {"success": true,"status": 1,"msg": null,"data": {"result":null}}  
- 示例说明

  * 当返回status为1时，说明充值成功

> ***内部游戏充值***

充值元宝时，需 验证订单是否有效

- 验证平台订单是否有效
  
   * https://recharge-url/validateorder?iGameId=1&iWorldId=1&vUserId=47502ea6-d2be-4f52-bf12-9b0652a0409c&iPlayerId=-1&iRmb=10&iDiscount=1&iGameCurrency=100&sign=sign_str&time=1342345467890

-  返回结果
   
    * {"success": true,"status": 1,"msg": null,"data": {"result":null}}  
 
- 示例说明
    * 当返回status为1时，说明订单有效

##平台充值接口详细说明
### 1. 微信充值接口
- 扫码支付接口URL :
     https://domain/recharge/weichat/initOrder
-  请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| iGameId | int | 必填 | 游戏ID |
| iWorldId | int | 必填 | 区服ID |
| vUserId | int | 必填 | 用户ID |
| iPlayerId | int | 必填 | 玩家ID |
| iRmb | int | 必填 | 充值金额 |
| iDiscount | int | 必填 | 折扣 |
| iGameCurrency | int | 必填 | 元宝 |

- 返回结果

<pre>JSON示例</pre>
```
{
    "success": true,
    "status": 1,
    "msg": null,
    "data": {"result":null}
}
```

#### 微信订单查询接口URL:
    https://domain/recharge/weichat/queryOrder
- 请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| vOrderNo | String | 必填 | 订单号 |

- 返回结果

<pre>JSON示例</pre>
```
{
    "success": true,
    "status": 1,
    "msg": null,
    "data": {"result":null}
}
```
### > __微信充值示例__


## 2. 支付宝充值接口
- 扫码支付接口URL
     https://domain/recharge/alipay/initOrder
- 请求参数列表

| 参数名称 | 参数类型 | 填写类型 | 参数说明 |
| ------- | --- |---- |---- |
| iGameId | int | 必填 | 游戏ID |
| iWorldId | int | 必填 | 区服ID |
| vUserId | int | 必填 | 用户ID |
| iPlayerId | int | 必填 | 玩家ID |
| iRmb | int | 必填 | 充值金额 |
| iDiscount | int | 必填 | 折扣 |
| iGameCurrency | int | 必填 | 元宝 |

- 返回结果

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
|sign|String|必填|效验码</br>sha256(vOrderNo=xxx&iGameID=fff&www=xxx ...</br>+gamesalt(游戏验证码))|
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
