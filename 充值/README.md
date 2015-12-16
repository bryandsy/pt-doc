---
date: 2015-12-15 14:59
status: public
title: 平台游戏接入流程
---

#平台游戏接入流程
##平台接入介绍
    为方便游戏接入平台，游戏接入时需 提供以下接口

##平台接口
###  平台订单验证
> 功能

    用于游戏币接口兑换时验证平台订单是否有效

> 访问方式
  
    http get/post
> 必要参数

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 平台用户 | uid | 
| 游戏角色 | role_id |  
| 游戏ID | gkey |  
| 游戏区服ID | skey  | 
| 充值订单号 |  order_id  | 
| 游戏元宝 | coins |  
| 时间戳 | time | 必须 |
| 签名 | sign | 必须 |

> URL示例 

    https://domain/[recharge-validate-url]?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&time=1342345467890&sign=sign_str

> sign签名

    sha256( uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&time=1342345467890)
    
> 返回结果

      {
            "status": 1,//状态 1：成功，0 ：失败
            "msg": null//信息
        }  
    
##游戏接口
###   平台玩家角色接口

> 功能

   用于平台查询平台用户游戏角色

> 访问方式
  
    http get/post
> 必要参数

| 名称 | 名称ID  |说明 |
| ---- | ---- | ---- |
| 平台用户 | uid | 
| 游戏ID | gkey |  
| 游戏区服ID | skey  | 
| 时间戳 | time  |   
| 签名 | sign  |  

> URL示例 

    https://domain/[getPlayerId]?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&gkey=1&skey=1time=1342345467890&sign=sign_str

> sign签名

    sha256( uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&gkey=1&skey=1time=1342345467890)
    
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
  
    http get/post
> 必要参数

| 名称 | 名称ID  |说明 |
| ---- | ---- | ---- |
| 平台用户 | uid | 
| 游戏角色 | role_id |  
| 游戏ID | gkey |  
| 游戏区服ID | skey  | 
| 平台订单号 | order_id  | 
|游戏币数额 | coins  | 
| 人民币数额 | moneys  |  单位：分 
| 时间戳 | time  |   
| 签名 | sign  |  

> URL示例 

    https://domain/[game-recharge-url]?参数

> 参数示例

    uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&moneys=1&time=1342345467890&sign=sign_str

> sign签名

    sha256(uid=47502ea6-d2be-4f52-bf12-9b0652a0409c&role_id=-1&gkey=1&skey=1&order_id=47502ea6&coins=100&moneys=1&time=1342345467890)
    
> 返回结果

      {
            "status": 1,//是否成功 1：成功，0 ：失败
            "msg": null//信息
        }  
 