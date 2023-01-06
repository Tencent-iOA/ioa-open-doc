## 1. 接口描述


获取rsa的公钥，对数据进行加密


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
            </div>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
            </div>
        </div>
    </div>
</div>

## 2. 输入参数


| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | [DescribePublicEncryptKeyData](/document/api/-1/##DescribePublicEncryptKeyData) | 获取公钥加密的key数据<br/>注意：此字段可能返回 null，表示取不到有效值。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 获取加密公钥

#### 输入示例

```
Path : /capi/common/DescribePublicEncryptKey 

<body>
{
}
```

#### 输出示例

```
{
    "Response": {
        "Data": {
            "PublicEncryptKey": "Ci0tLS0tQkVHSU4gUFVCTElDIEtFWS0tLS0tCk1JSUNJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBZzhBTUlJQ0NnS0NBZ0VBdGl3VUcwQytzV202ejdhb"
        },
        "RequestId": "1658370135.3057716"
    }
}
```












## 5. 错误码


| 错误码 | 描述 |
|---------|---------|
| InternalError.Unknown | 内部未知错误。 |
