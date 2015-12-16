---
date: 2015-12-15 14:59
status: public
title: 平台游戏接入流程
---

#平台游戏接入流程
##平台接入介绍
    为方便游戏接入平台，游戏接入时需 提供以下接口
> 接口使用场景

1.  平台充值时，调用游戏玩家角色接口，用于查询玩家角色，以完成平台充值
2. 兑换游戏币接口，使用时
 
*  平台与游戏签名使用的校验码，从游戏校验码接口查询 
* 需在游戏币兑换前，调用平台订单验证接口，验证订单是否有效，有效的状态下才能进行游戏币兑换

满足以上，即可完成平台充值与游戏对接

##游戏接口
###   游戏玩家角色接口

> 功能

   用于平台查询游戏玩家游戏角色

> 访问方式
  
    https get/post
> 必要参数

| 名称 | 名称ID  |类型 | 示例  | 备注  |
| ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid | string | 47502ea6-d2be-4f52-bf12-9b0652a0409c | |
| 游戏ID | gkey | string | 1
| 游戏区服ID | skey  | string | 1
| 时间戳 | time  |  string | 1450251211782
| 签名 | sign  |  string | 4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072 |

> URL示例 

    https://domain/[getPlayerId]?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&gkey=1&skey=1time=1450251211782&sign=4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072

> sign签名

    sha256( uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&gkey=1&skey=1&time=1342345467890SIGN_KEY)
    
> 返回结果

 {
        "status": 0,//是否成功标识状态
        "msg": null,//错误信息
        "data": [
                     {"role_id":"id","role_name":"name"}, 
                     {"role_id":"id","role_name":"name"}
                     ]
    }  


###   兑换游戏币接口
> 功能

    游戏币发放

> 访问方式
  
    https get/post
> 必要参数

| 名称 | 名称ID  | 类型｜示例  | 备注 |
| ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid | string | 47502ea6-d2be-4f52-bf12-9b0652a0409c | 必须 |
| 游戏角色 | role_id | string  |  999 | 必须 |
| 游戏ID | gkey |  string | 1  | 必须 |
| 游戏区服ID | skey  | string |  1 | 必须 |
| 平台订单号 | order_id  | string | 9e3e0a99a48647418476eeb0634f0eb7  | 必须 |
|游戏币数额 | coins  | string |  1 | 必须 |
| 人民币数额 | moneys  |  string | 100 (单位：分) | 必须 | 
| 时间戳 | time  |   string | 1450251211782(单位 : milliseconds）  | 必须 |
| 签名 | sign  |  string | 4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072 | | 必须 |

> URL示例 

    https://domain/[game-recharge-url]?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&moneys=1&time=1342345467890&sign=sign_str

> sign签名

    sha256(uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&moneys=1&time=1342345467890SIGN_KEY)
    
> 返回结果

      {
            "status": 1,//是否成功 1：成功，0 ：失败
            "msg": null//信息
        }  


##平台接口
###  平台订单验证
> 功能

    用于游戏币接口兑换时验证平台订单是否有效

> 访问方式
  
    http get/post
> 必要参数

| 名称 | 名称ID | 类型  | 示例 | 备注 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid |  string | 47502ea6-d2be-4f52-bf12-9b0652a0409c |必须 |
| 游戏角色 | role_id |  string | |  必须 |
| 游戏ID | gkey |  string | |  必须 |
| 游戏区服ID | skey  |  string  | | 必须 |
| 充值订单号 |  order_id  |  string  | | 必须 | 9e3e0a99a48647418476eeb0634f0eb7 | 必须 |
| 游戏元宝 | coins |  string |   100  | 必须 |
| 时间戳 | time  |   string | 1450251211782(单位 : milliseconds）  | 必须 |
| 签名 | sign |  string |  4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072 | 必须

> URL示例 

    https://domain/recharge/validateorder?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&time=1342345467890&sign=sign_str

> sign签名

    sha256( uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&time=1342345467890SIGN_KEY)
    
> 返回结果

      {
            "status": 1,//状态 1：成功，0 ：失败
            "msg": null//信息
        }  
###  游戏校验码
> 功能

    用于游戏和平台签名时所用的key

> 访问方式
  
    https get/post
> 必要参数

| 名称 | 名称ID | 类型 | 示例 | 备注 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 游戏ID | gkey |  string | 1 | 必须 | 
| 时间戳 | time  |  string | 1450251211782 | 必须 |
| 签名 | sign  |  string | 4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072 |必须 |

> URL示例 

    https://domain/recharge/getGameSalt?参数

> 参数示例

gkey=1&time=1450251211782&sign=sign_str

> sign签名

    sha256(gkey=1&time=1450251211782SIGN_KEY)
    
> 返回结果

    {
      "status" : 1,
      "data" : {
           "gid" : 1,
           "recharge_token" : "hwuehf2394ffa"  //游戏验证码
       }
    }
    
 