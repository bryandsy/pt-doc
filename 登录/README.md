<pre>服务器需要配置为HTTPS</pre>
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
sign|string|验证秘钥 SHA256（uid=xxx&sid=xxx&time=xxx&logintype=xxx&is_adult=xxx&pt_vip=xxx+login_token 即除sign外参数子串+login_token(游戏登录秘钥)）

<pre>例子</pre>

######若 uid=testuser , sid=123 , time=1450084717290 , logintype=1 , is_adult=0 , pt_vip=0
######双方约定的 login_token 为 login_test
######则 sign 为字符串 uid=testuser&sid=123&time=1450084717290&logintype=1&is_adult=0&pt_vip=0login_test 的SHA256签名值
######为 f9aaf1a9566a4ff1e0b19e4f37e6bb66dcbcd8ff7290d9798bfe03d1f3d31ba1


