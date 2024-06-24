# 1 SSO登录证书
## 1.1 配置路径
### 1.1.1 6.x版本
位置：系统设置 - 系统通用设置 - 证书管理 - SSO登录证书
![SSO登录证书](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO登录证书.png)

### 1.1.2 7.x及以上版本
位置：策略中心 - 身份安全策略 - 认证安全 - SSO管理
![SSO管理](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO管理.png)

### 1.1.3 SaaS 版本
位置：策略中心 - 身份安全策略 - 认证安全 - SSO管理

## 1.2 证书获取
如果客户需要自己的业务系统也通过ioa进行快速sso单点登陆，那么需要客户提供一个解析到127.0.0.1的域名，并申请有效的ca认证证书提供给ioa。注意：域名和证书由用户提供，腾讯只提供技术支持。
## 1.3 证书格式修改
证书名字必须改为service\_cert.crt和service\_key.key，否则iOA后台无法读取和识别

![证书配置名](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/证书配置名.png)

例子：客户提供证书为[xxxxxx.com](http://xxxxxx.com).key和[xxxxxx.com](http://xxxxxx.com).pem

- key文件为key后缀时直接改名，[xxxxxx.com](http://xxxxxx.com).key直接重命名为service\_key.key
- key文件为pem格式时，需要转换成key后缀，转换代码：openssl rsa -in xxxxkey.pem -out service.key
- cer格式转换crt方式，转换代码：openssl x509 -in [xxxxxx.com](http://xxxxxx.com).pem -out service\_cert.crt
- pem格式转换crt方式：openssl x509 -in [xxxxxx.com](http://xxxxxx.com).pem -out service\_cert.crt
## 1.4 证书导入
点击导入证书

![导入证书](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/导入证书.png)

服务端证书是必须导入的，根证书一般不建议导入

【根证书说明】

![SSO根证书](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO根证书.png)

客户端起的监听是HTTPS的，导入根证书会校验第三方的请求证书。

https请求SSL握手有单向和双向。如果不导入根证书则是单向的，导入根证书就会走双向认证逻辑，会要求第三方调用者发送客户端证书过来，然后用根证书校验。

# 2 添加应用
## 2.1 配置路径
### 2.1.1 6.x版本
位置：系统设置 - 系统通用设置 - SSO登录应用管理

![SSO登录应用管理](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO登录应用管理.png)
### 2.1.1 7.x版本
位置：策略中心 - 身份安全策略 - 认证安全 - SSO管理

![SSO管理](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO管理.png)
## 2.2 开启SSO服务，并添加应用
![SSO服务开关](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/SSO服务开关.png)
## 2.3 配置应用

|<p></p><p>配置字段说明</p>||
| :- | :- |
|<p></p><p>应用ID</p>|<p></p><p>自动生成，需要复制出此ID 到第三方系统下发IOA登录配置里和配置登录方式里的应用ID字段</p>|
|<p></p><p>应用名称</p>|<p></p><p>起别名</p>|
|<p></p><p>应用类型</p>|<p></p><p>必选其一（桌面应用：例如通过客户端访问的系统；浏览器应用：通过浏览器访问的系统）</p>|
|<p></p><p>校验配置</p>|<p></p><p>可选（勾选对应校验项以执行相应校验，确保应用安全性。）</p>|
|<p></p><p>SSO登录票据校验</p>|<p></p><p>可选，勾选后出现秘钥（适用于无IAM系统的快速登录场景）</p>|
## 2.4 复制应用ID和公钥
- 复制应用ID

点击编辑

![编辑应用ID1](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/编辑应用ID1.png)

![编辑应用ID2](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/编辑应用ID2.png)

- 复制公钥

点击复制公钥（需勾选SSO登录票据校验才会出现）

![复制公钥](https://github.com/pengfeihuu/ioa-open-doc/raw/master/resource/sso/client/复制公钥.png)

