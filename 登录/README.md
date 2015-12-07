###游戏接入参数
<pre>本条为新游戏接入需要提供的必备参数列表</pre>
参数名称|参数类型|填写类型|参数说明
| --------   | -----:  | :----:  |:----:  |
gid|int|必填|游戏ID
gtag|string|必填|游戏标示
gname|string|必填|游戏名称
gurl|string|必填|游戏主页地址
opentime|date|必填|游戏开始时间(yyyy-MM-dd HH:mm:ss)
recharge_url|string|必填|游戏充值地址
recharge_token|string|必填|游戏充值秘钥（充值验证用）
recharge_ratio|int|必填|游戏充值比率
login_token|string|必填|游戏登录秘钥(登入验证用)

###服务器接入参数
<pre>本条为新服务器接入需要提供的必备参数列表</pre>
参数名称|参数类型|填写类型|参数说明
| --------   | -----:  | :----:  |:----:  |
gid|int|必填|游戏ID
sid|string|必填|区服ID
sname|string|必填|区服名称
surl|string|必填|区服登录地址
opentime|date|必填|区服开服时间(yyyy-MM-dd HH:mm:ss)

###服务器请求参数
<pre>本条为平台用户进行登录游戏服务器的操作后发送至服务器登录地址的请求参数</pre>
参数名称|参数类型|参数说明
| --------   | -----:  |:----:  |
uid|string|用户ID
sid|int|服务器ID
time|long|时间戳 毫秒
logintype|int|登录状态 0网页 1微端
is_adult|int|防沉迷 0否 1是
pt_vip|int|平台vip等级
sign|string|验证秘钥 SHA256（uid=xxx&sid=xxx&time=xxx&logintype=xxx&is_adult=xxx&pt_vip=xxx+login_token）
