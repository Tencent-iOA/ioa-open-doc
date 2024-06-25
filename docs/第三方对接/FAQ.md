
# 1、如何获取 iOA 侧的账号组织架构及账号信息
如果使用的私有化 iOA（版本>=7.x），可按如下方法获取：
> a. 调用接口 [DescribeAccountGroups](https://tencent-ioa.github.io/ioa-open-doc/#/%E5%BC%80%E6%94%BEAPI/%E4%BA%91%E8%A7%84%E8%8C%83%E6%8E%A5%E5%8F%A3/%E7%89%88%E6%9C%AC%EF%BC%9A2022-06-01/%E8%BA%AB%E4%BB%BD%E4%B8%8E%E6%9D%83%E9%99%90%E7%AE%A1%E7%90%86%E7%9B%B8%E5%85%B3%E6%8E%A5%E5%8F%A3/%E6%9F%A5%E8%AF%A2%E8%B4%A6%E6%88%B7%E7%9B%AE%E5%BD%95%E5%88%97%E8%A1%A8) 获取账号组织架构分组列表。这里入参可以直接用空json体`{}`来获取默认的全量组织架构目录列表，但如果组织架构列表数据过多，就需要结合分页请求参数与接口响应的分页数据来获取。<br/>
> b. 依次根据账号组织架构的分组Id，调用 [DescribeLocalAccounts]()，入参的ShowFlag传2，获取该账号分组下的所有直接账户<br/>
> c. 综合上述 a 获取的账号组织分组结构，和 b 获取的账号信息，按树结构组织后，即为 iOA 侧全量的账号组织架构和账号信息

如果使用的 SaaS iOA，可按如下方法获取：
> a. 调用接口 [DescribeRootAccountGroup](https://cloud.tencent.com/document/api/1092/107709) 获取账号组织架构的根分组Id<br/>
> b. 调用接口 [DescribeAccountGroups](https://cloud.tencent.com/document/api/1092/107711)，传入根分组Id，分页逐层获取整颗账号组织架构分组树<br/>
> c. 依次根据账号组织架构的分组Id，调用 [DescribeLocalAccounts](https://cloud.tencent.com/document/api/1092/107710)，获取该分组下的直接账号

# 2、iOA 目录的概念是什么，如何通过账号信息判定属于哪个目录
iOA 支持多目录，这里的目录对应的是账号组织架构根分组下的一级分组。

如：某客户，自建了一个目录，叫“自建账号源”，用于在 iOA 体系里由管理员新建账密账号；<br/>
同时，该客户自建了另一个目录，叫“企微账号源”，用于导入该企业的企业微信账号。
此时，该客户下，就有两个目录，iOA 客户端登录时，要先选择登录哪个目录，再进一步登录该目录下的账号。

若期望通过账号信息，反查该账号属于哪个目录，可以按以下方法进行：
>a. 根据账号，调用DescribeLocalAccounts，获取账号对应的GroupId<br/>
b. 根据GroupId，调用DescribeAccountGroups，获取分组对应的IdPathArr<br/>
c. 账号menu均挂载在一个共同的根下（如1.x.y），IdPathArr[1]即为menu Id