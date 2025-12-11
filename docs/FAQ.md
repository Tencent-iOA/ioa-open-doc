### Q：如何获取 iOA 侧的账号组织架构及账号信息
如果使用的私有化 iOA（版本>=7.x），可按如下方法获取：
> a. 调用接口 [DescribeAccountGroups](https://tencent-ioa.github.io/ioa-open-doc/#/%E5%BC%80%E6%94%BEAPI/%E4%BA%91%E8%A7%84%E8%8C%83%E6%8E%A5%E5%8F%A3/%E7%89%88%E6%9C%AC%EF%BC%9A2022-06-01/%E8%BA%AB%E4%BB%BD%E4%B8%8E%E6%9D%83%E9%99%90%E7%AE%A1%E7%90%86%E7%9B%B8%E5%85%B3%E6%8E%A5%E5%8F%A3/%E6%9F%A5%E8%AF%A2%E8%B4%A6%E6%88%B7%E7%9B%AE%E5%BD%95%E5%88%97%E8%A1%A8) 获取账号组织架构分组列表。这里入参可以直接用空json体`{}`来获取默认的全量组织架构目录列表，但如果组织架构列表数据过多，就需要结合分页请求参数与接口响应的分页数据来获取。<br/>
> b. 依次根据账号组织架构的分组Id，调用 [DescribeLocalAccounts]()，入参的ShowFlag传2，获取该账号分组下的所有直接账户<br/>
> c. 综合上述 a 获取的账号组织分组结构，和 b 获取的账号信息，按树结构组织后，即为 iOA 侧全量的账号组织架构和账号信息

如果使用的 SaaS iOA，可按如下方法获取：
> a. 调用接口 [DescribeRootAccountGroup](https://cloud.tencent.com/document/api/1092/107709) 获取账号组织架构的根分组Id<br/>
> b. 调用接口 [DescribeAccountGroups](https://cloud.tencent.com/document/api/1092/107711)，传入根分组Id，分页逐层获取整颗账号组织架构分组树<br/>
> c. 依次根据账号组织架构的分组Id，调用 [DescribeLocalAccounts](https://cloud.tencent.com/document/api/1092/107710)，获取该分组下的直接账号
<br/>

### Q：iOA 目录的概念是什么，如何通过账号信息判定属于哪个目录
iOA 支持多目录，这里的目录对应的是账号组织架构根分组下的一级分组。

如：某客户，自建了一个目录，叫“自建账号源”，用于在 iOA 体系里由管理员新建账密账号；<br/>
同时，该客户自建了另一个目录，叫“企微账号源”，用于导入该企业的企业微信账号。
此时，该客户下，就有两个目录，iOA 客户端登录时，要先选择登录哪个目录，再进一步登录该目录下的账号。

若期望通过账号信息，反查该账号属于哪个目录，可以按以下方法进行：
>a. 根据账号，调用DescribeLocalAccounts，获取账号对应的GroupId<br/>
b. 根据GroupId，调用DescribeAccountGroups，获取分组对应的IdPathArr<br/>
c. 账号menu均挂载在一个共同的根下（如1.x.y），IdPathArr[1]即为menu Id
<br/>

### Q：API 请求体中的非对称加密字段如何加密，如 [CreateLocalAccount](https://tencent-ioa.github.io/ioa-open-doc/#/开放API/云规范接口/版本：2022-06-01/身份与权限管理相关接口/创建本地账号?id=创建本地账号) 中的 Password 字段
> a. 调用接口 [DescribePublicEncryptKey](https://tencent-ioa.github.io/ioa-open-doc/#/开放API/云规范接口/版本：2022-06-01/公共模块相关接口/获取加密公钥)，获取公钥<br/>
> b. 对要加密的字段，如`Password`字段进行 rsa 加密<br/>

以下是一段`python`示例代码：
```
def encyptPassword(password):
	data = DoApiRequest(action='DescribePublicEncryptKey')
	PublicEncryptKey = data[0]["Response"]["Data"]["PublicEncryptKey"]
	public_key = base64.b64decode(PublicEncryptKey.encode("utf-8"))
	if public_key.startswith("\n".encode("utf-8")) and not public_key.endswith("\n".encode("utf-8")):
		public_key = (public_key + "\n".encode("utf-8"))[1:]
	rsa_pubkey = RSA.import_key(public_key)
	cipher_pub = PKCS1_v1_5.new(rsa_pubkey)
	ciphervalue_enc = base64.b64encode(cipher_pub.encrypt(password.encode("utf-8")))
	return ciphervalue_enc.decode()
```

### Q：如何获取`云规范接口`签名所需的 Secret 信息
Secret信息，等价于相应的管理员权限，注意保密防泄露。
获取Secret方法如下：
> a. 检查控制台左边栏菜单"系统设置-第三方对接"下，是否展示有"API接口管理"页面，如无有两种可能：<br/>
	1）当前登录控制台的管理员是非超管，而超管又未给当前管理员分配"API接口管理员"页面权限 - 联系超管授权<br/>
	2）部分历史版本，该页面是隐藏不开放页面 - 联系 iOA 侧放通<br/>
b. 在"系统设置-第三方对接-API接口管理"页面，点击"添加API凭证"，从而生成与当前管理员权限绑定的SecretId和SecretKey信息

注：iOA 侧服务人员，如何开放"API接口管理"页面，参见内部文档：https://iwiki.woa.com/p/4010953746

### Q：云规范接口API调用，如何判断接口响应是成功，还是出错
* `Response.Error.Code`非空<br/>
表示出错。此时先结合`Response.Error.Code`和`Response.Error.Message`的提示排查错误，若仍无法定位，可提供`Response.RequestId`，与相关服务日志进一步定位出错原因。
* `Response.Error.Code`空<br/>
表示成功。若该接口有额外数据响应，数据位于`Response.Data`。

### Q：API调用，HTTP码返回`401`的常见原因
#### 1）common_rsp.msg 返回 `Missing related consumer`
提供的SecretId、SecretKey与连接的控制台服务器不相配，登录控制台去检查提供的AKSK信息是否正确。
#### 2）common_rsp.msg 返回 `Invalid signature`
按SDK文档，检查传入的信息是否充分，如API版本号（X-TC-Version）、时间戳（X-TC-Timestamp）等字段。
#### 3）common_rsp.msg 返回 `timestamp is timeout`
可能原因有：
* a. 调用端与服务端时钟不同步
* b. 调用端HTTP请求头里的X-TC-Timestamp，没有按实际调用时间（UNIX时间戳格式）来传递<br/>

排查方法：
针对时钟不同步问题，检查总控集群root角色的所有服务器时钟，这些服务器的时钟需要一致，且发起API调用的客户机时钟也需要与服务器保持一致。
同时，调用端，打印下出错时HTTP请求头信息，并提供RequestId，以便与服务器请求对账，进一步定位问题。

### Q：API调用，接口返回的响应格式与预期的不一致
针对云API规范的接口，预期的响应格式为：
```json
// 成功
{
    "Response": {
        "Data": {
            "ServiceId": 4391
        },
        "RequestId": "20a21cd8-cbc5-4d70-a14d-9c6aafcbd8ab"
    }
}
// 失败
{
    "Response": {
        "Error": {
            "Message": "名称不能超过20个字符",
            "Code": "InvalidParameter.NameToLong"
        },
        "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
    }
}
```
若出现云API规范的接口，返回响应非以上格式，如：
```
{
	"CommonRsp": {}
}
```
请排查下请求的API接口Path、API版本号是否与API文档一致，如检查是否请求时，正确的传递了API版本号2022-06-01。

### Q：如何根据终端mid获取关联的终端自定义组
iOA支持通过接口DescribeDeviceVirtualGroups查询到所有终端自定义组，再通过接口DescribeVirtualDevices查询到某个终端自定义组下的终端设备。通过反映射的方式，可组织起终端mid→终端自定义组的映射关系。