---
date: 2015-12-15 14:59
status: public
title: 平台游戏充值流程
---

#平台游戏充值流程
##平台充值介绍
> 进入平台首页选择充值功能，进入充值流程（必须检测是否登陆）,如下示例页面

---------------------------------------------------------------------
> 登陆平台首页

<p><img  alt="platform" src="https://github.com/szmolin/pt-doc/blob/master/%E5%85%85%E5%80%BC/game_platform_index.jpg" title="platform" height="475" width="583"></p>

>  点击游戏充值进入充值页面

<p><img alt="recharge" src="https://github.com/szmolin/pt-doc/blob/master/%E5%85%85%E5%80%BC/game_recharge_form.jpg" title="recharge" height="475" width="583"> </p>

##平台充值

    登陆平台后点击游戏充值，进入充值页面，选择支付类型和充值金额，生成二维码直接扫描支付即可
    
- 充值示例

_默认以JSONP方式请求和返回数据（get/post）_

 > 充值URL
   
      https://domain/recharge-url?function=jQuery18106264256320428103_1445247783992&iGameId=1&iWorldId=1&vUserId=47502ea6-d2be-4f52-bf12-9b0652a0409c&iPlayerId=-1&iRmb=10&iDiscount=1&iGameCurrency=100&_=1445247788405
      
  *recharge-url为平台提供*

> 充值表单参数

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 平台用户 | vUserId | 
| 游戏角色 | iPlayerId |  
| 游戏平台 | iGameId |  
| 游戏区服 | iWorldId  | 
| 充值数额 | iRmb  | 
| 游戏元宝 | iGameCurrency |  

公共参数

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 函数 | function | 必须 

  
-  返回结果

> 成功
 
        {
            "success": true, //是否成功标识
            "status": 1,//是否成功标识状态
            "msg": null,//错误信息
            "data": {"result":null}
        }  

> 失败

    {
        "success": false,//是否成功标识
        "status": 0,//是否成功标识状态
        "msg": null,//错误信息
        "data": {"result":null}
    }  
    
- 示例说明

        当返回status为1或者success为true时，说明充值成功

## ***内部游戏充值***

游戏充值元宝时，需验证订单是否有效

 _默认以JSONP方式请求和返回数据（get/post）_

 > 验证URL 
   
     https:/domain/[validateorder-url]?iGameId=1&iWorldId=1&vUserId=47502ea6-d2be-4f52-bf12-9b0652a0409c&iPlayerId=-1&iRmb=10&iDiscount=1&iGameCurrency=100&sign=sign_str&time=1342345467890   
     
   *validateorder-url为平台提供*

> 验证参数

| 名称 | 名称ID | 说明 |
| ---- | ---- | ---- |
| 平台用户 | vUserId | 
| 游戏角色 | iPlayerId |  
| 游戏平台 | iGameId |  
| 游戏区服 | iWorldId  | 
| 充值订单号 |  vOrderNo  | 
| 游戏元宝 | iGameCurrency |  

公共参数

| 名称 | 名称ID | 名称 |
| ---- | ---- | ---- |
| 函数 | function | 必须 |
| 签名 | sign | 必须 |
| 时间戳 | time | 必须 |

> sign签名

    sha256(vOrderNo=xxx&iGameID=fff&www=xxx ...+gamesalt(游戏验证码))

-  返回结果
     
> 成功
 
        {
            "success": true, //是否成功标识
            "status": 1,//是否成功标识状态
            "msg": null,//错误信息
            "data": {"result":null}
        }  

> 失败

    {
        "success": false,//是否成功标识
        "status": 0,//是否成功标识状态
        "msg": null,//错误信息
        "data": {"result":null}
    }  

 
- 示例说明
    * 当返回status为1时，说明订单有效
