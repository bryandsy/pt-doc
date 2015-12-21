---
date: 2015-12-15 14:59
status: public
title: 平台游戏接入流程
---

#平台游戏网页接入流程
##平台接入介绍
    为方便游戏接入平台，游戏接入时需 提供以下接口
> 接口使用场景

1.  平台充值时，调用游戏玩家角色接口，用于查询玩家角色，以完成平台充值
2. 兑换游戏币接口，使用时
 
*  平台与游戏签名使用共同协商好的校验码(即SIGN_KEY)
*  平台订单验证接口
     *  为了防止伪造平台订单支付成功通知, 游戏兑换接口可以使用本接口做通知数据的校验，验证平台是否存在这个订单，保证平台充值和游戏币兑换过程及状态是正常的
* 游戏币兑换接口
     * 使用时，必须检测订单是否在平台有效（即调用平台订单验证接口），有效的状态下才能进行游戏币兑换，否则，终止游戏币兑换，并通知平台方

*平台游戏校验码接口和订单验证接口详细信息，查看具体接口描述*

满足以上，即可完成平台充值与游戏对接

##游戏接口
###   游戏玩家角色接口

> 功能

   用于平台查询游戏玩家游戏角色

> 访问方式
  
    https/http [get/post]
> 必要参数

| 名称 | 名称ID  |类型 | 示例  | 备注  |
| ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid | string | 47502ea6-d2be-4f52-bf12-9b0652a0409c | 必须 |
| 游戏ID | gkey | string | 1 | 必须 |
| 游戏区服ID | skey  | string | 1 | 必须 |
| 时间戳 | time  |  string | 1450251211782 | 必须 |
| 签名 | sign  |  string | 4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072  | 必须 |

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
  
    https/http [get/post]
> 必要参数

| 名称 | 名称ID  | 类型  | 示例  | 备注 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid | string | 47502ea6-d2be-4f52-bf12-9b0652a0409c | 必须 |
| 游戏角色 | role_id | string  |  999 | 必须 |
| 游戏ID | gkey |  string | 1  | 必须 |
| 游戏区服ID | skey  | string |  1 | 必须 |
| 平台订单号 | order_id  | string | 9e3e0a99a48647418476eeb0634f0eb7  | 必须 |
|游戏币数额 | coins  | string |  1 | 必须 |
| 人民币数额 | moneys  |  string | 100 (单位：分) | 必须 | 
| 时间戳 | time  |   string | 1450251211782(单位 : milliseconds）  | 必须 |
| 签名 | sign  |  string | 4ab2e6c59b3043ca3c51207b99dda19044093d18c153f97c6abd1e5138b1072 |  必须 |

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
  
   https/http [get/post]
> 必要参数

| 名称 | 名称ID | 类型  | 示例 | 备注 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 平台用户 | uid |  string | 47502ea6-d2be-4f52-bf12-9b0652a0409c |必须 |
| 游戏角色 | role_id |  string |234 |  必须 |
| 游戏ID | gkey |  string | 1 |  必须 |
| 游戏区服ID | skey  |  string  | 1 | 必须 |
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
        
#平台游戏客户端接入流程
##客户端接入
###  游戏内充值功能
   > 功能

    用于游戏内部充值功能调用，充值功能与页面效果相同

> 所需资源
  
  ```pre   
<link rel="stylesheet" type="text/css" 
href=https://cdn-prod.36b.me/recharge/static/css/box/box.css />
<script type="application/javascript" 
src="https://cdn-prod.36b.me/recharge/static/js/jquery-2.1.4.min.js"></script>
<script type="application/javascript" 
src="https://cdn-prod.36b.me/recharge/static/js/box/moklin.box.plugin.js"></script>
```

> 调用方法

  ```pre 
  $(document).ready(function(){
                   //isFrame表示页面控制的ID，可以自行更 改
                    $("#isFrame").BOX({
                        pttype: "iframe", //加载页面组件方式
                        iwh: {
                            w: 800, //弹出层在页面的宽度
                            h: 500  ///弹出层在页面的高度
                        },
                        target: "recharge-url" //调用平台充值页面
                    });
            });  
  ```
  
     
> 必要参数

| 名称 | 名称ID | 类型  | 示例 | 备注 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 游戏角色 | iPlayerId |  string |234 |  必须 |
| 游戏ID | iGameId |  string | 1 |  必须 |
| 游戏区服ID | iWorldId  |  string  | 1 | 必须 |

> URL示例

    https://recharge-url?iPlayerId=234&iGameId=1&iWorldId=1
    
> 场景使用

```pre
<!-- 加载所需 资源-->
<link rel="stylesheet" type="text/css" 
href=https://cdn-prod.36b.me/recharge/static/css/box/box.css />
<script type="application/javascript" 
src="https://cdn-prod.36b.me/recharge/static/js/jquery-2.1.4.min.js"></script>
<script type="application/javascript" 
src="https://cdn-prod.36b.me/recharge/static/js/box/moklin.box.plugin.js"></script>
<!-- 加载控件-->
<script type="application/javascript" >
    $(document).ready(function(){
           //isFrame表示页面控制的ID，可以自行更 改为当前的充值按钮
                    $("#isFrame").BOX({
                        pttype: "iframe", //加载页面组件方式
                        target:  https://recharge-url?iPlayerId=234&iGameId=1&iWorldId=1//调用平台充值页面
                    });
            });  
</script>
```
