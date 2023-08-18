# 零信任iOA移动端SDK接入文档说明

## 能力说明

### 零信任iOA SDK（ZTSDK，移动端）提供的能力：

1、iOA的登录能力

（1）内置iOA登录界面的形式（推荐使用此形式）。支持iOA产品主线的登录方式（包含：账密、企微（仅私有化）、飞书、钉钉等）。

注意事项：iOS端出于企微/飞书/钉钉等第三方SSO限制，需要将第三方控制台上申请的SSO配置信息（schema等）打包到最终的ipa中，详细方法见下面集成指导。

（2）第三方SSO授权登录方式，无界面。集成方应用颁发授权code给iOA进行验证登录。

2、iOA SSO能力：iOA登录后，给集成方应用发出授权code，集成方应用校验后实现无感登录。

3、iOA安全连接能力；以及安全连接异常状态通知能力（通知栏形式）

4、iOA安全检测能力。

附：内置登录页面效果

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-login-1.png" alt="image-login-1" style="zoom:20%;border:1px solid #ddd;"/><img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-login-2.png" alt="image-login-2" style="zoom:20%;border:1px solid #ddd;"/><img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-login-3.png" alt="image-login-3" style="zoom:20%;border:1px solid #ddd;"/>

## 集成指导

### SDK功能集成流程示例

（以Android为例）

![sdk.drawio](https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/sdk.drawio.png)



### Android集成步骤

**1、引入ZTSDK库**

将ZTSDK的aar包放在接入方项目工程的libs下，然后通过gradle的implementation fileTree()引用。如下：

~~~groovy
dependencies {
  // 引入ZTSDK库，一般将ZTSDK的aar库入在app模块的libs目录下
  implementation fileTree(dir: 'libs', include: ['*.aar '])
}
~~~

**2、配置ZTSDK的依赖库**

由于androidx和kotlin是Android系统提供的，为了避免可能与接入方已有的相关库有冲突，ZTSDK的库并没有androidx和kotlin的代码，所以需要接入方单独配置。在build.gradle文件中加入以下配置：

~~~groovy
dependencies {
  // 引入ZTSDK库，一般将ZTSDK的aar库入在app模块的libs目录下
  implementation fileTree(dir: 'libs', include: ['*.aar '])
  // ZTSDK库依赖库配置                                               
  implementation "androidx.room:room-runtime:2.1.0"
  implementation 'androidx.appcompat:appcompat:1.2.0'
  implementation "androidx.core:core-ktx:1.3.1"
  implementation "org.jetbrains.kotlin:kotlin-stdlib:1.4.10"
  implementation "org.jetbrains.kotlin:kotlin-android-extensions-runtime:1.4.10"
  implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.3.6"
  implementation "org.jetbrains.kotlinx:kotlinx-coroutines-play-services:1.3.6"
  implementation "com.squareup.okhttp3:okhttp:3.11.0"
  implementation "com.squareup.okio:okio:1.14.0"
  implementation "io.reactivex.rxjava2:rxandroid:2.1.0"
  implementation "io.reactivex.rxjava2:rxjava:2.2.6"
  implementation "org.reactivestreams:reactive-streams:1.0.2"
  implementation "com.google.code.gson:gson:2.8.1"
  implementation "com.google.android.material:material:1.0.0"
  implementation "com.githang:status-bar-compat:latest.integration"
}
~~~

**3、配置DDShareActivity**

使用iOA内置登录界面，进行钉钉登录时，需要配置DDShareActivity。配置步骤如下：需要在应用包名.ddshare目录下创建DDShareActivity，并将如下代码复制到DDShareActivity中。

```java
import android.app.Activity;
import android.os.Bundle;
import com.android.dingtalk.share.ddsharemodule.IDDAPIEventHandler;
import com.android.dingtalk.share.ddsharemodule.message.BaseReq;
import com.android.dingtalk.share.ddsharemodule.message.BaseResp;
import com.tencent.temm.mummodule.login.v2.thirdparty.ddshare.DDShareAPI;

/**
 * 钉钉登录回调页面。包路径受钉钉登录SDK限制必须为：包名.ddshare。
 */
public class DDShareActivity extends Activity implements IDDAPIEventHandler {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        DDShareAPI.onCreate(this, getIntent(), this);
    }

    @Override
    public void onReq(BaseReq baseReq) {
    }

    @Override
    public void onResp(BaseResp baseResp) {
        boolean isAbort = DDShareAPI.onResp(baseResp);
        if (isAbort) {
            return;
        }
        finish();
    }
}
```

注：更详细集成方法见AndroidSDK.zip压缩包Demo目录内的ZTSDKDEMO工程

### iOS集成步骤

#### 证书准备

申请主App和Network Extension证书，同时**Capabilities** 一项至少需要开启`App Groups`和`Network Extensions`
，前者用以主App和NE进程间数据共享交换，后者用以App开启代理能力。

> 注：Demo工程不提供接入需要的签名证书和App Groups，接入方需自行申请开发和发布证书。另外，VPN应用上架需要有资质证明，所以接入方应提前规划好交付方式和证书申请。

#### 工程配置

**1、创建Network Extension**

主工程新建一个Target，选择`Network Extension` ， 同时`Provider Type`选择**Packet Tunnel**

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-20211206105954801.png" alt="image-20211206105954801" style="zoom:50%;" />

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-20211206110032298.png" alt="image-20211206110032298" style="zoom:50%;" />

**2、关闭Bitcode**

主工程和Network Extension的`Build Settings` - `Build Options`中，将`Enable Bitcode`设置为**No**

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/image-20211206110211986.png" alt="image-20211206110211986" style="zoom:50%;" />

**3、配置Capabilities**

在主工程和Network Extension的`Signning & Capabilities`中，添加App Groups和Network Extensions的`Capability` :

- App Groups内容为申请时定义好的group
- Network Extensions一项中，开启**Packet Tunnel**

![](https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/capability.png)

**4、配置Info.plist**

在主工程和Network Extension的`Info.plist`文件中，添加字段CFBundle_application_groups，Value为App Groups的内容。

<font color=#FF000>特别地：使用iOA 内置登录页面，进行企微/飞书/钉钉等第三方授权登录时，出于第三方授权平台的要求，需要进行以下配置；配置不支持动态下发，因而需要在具体项目的**
安装包打包前完成配置**。</font>

企业微信/政务微信配置

- 配置企微/政微回跳 URL：URL types Key 下添加创建应用时返回的schema。

飞书配置

- 说明：如果宿主是纯 OC 项目，大概率没有 Swift 编译环境，创建一个空的 Swift 文件即可，这样 Xcode 会增加 Swift 的编译环境（LarkSSO 使用 Swift 5）。

- 配置跳转 Scheme: LSApplicationQueriesSchemes Key 下添加 lark

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/larksso1.png" alt="larksso1" style="zoom:50%;" />

- 配置飞书回跳 URL：URL types Key 下添加注册时申请到的 app_id （例如：clia0988c0addf81013），注意需要去掉 app_id 中的下划线

<img src="https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/larksso2.png" alt="larksso2" style="zoom:50%;" />

钉钉配置

- 配置跳转 Scheme: LSApplicationQueriesSchemes Key
  下添加dingtalk（查询是否安装钉钉）、dingtalk-open（查询是否支持开放平台接口调用，不需要查询开放平台接口可不填）、dingtalk-sso（查询是否支持授权登录）。
- 配置钉钉回跳 URL：URL types Key 下添加创建应用时返回的AppKey。

#### 导入SDK

ZTSDK提供两种方式将 SDK 导入到您的项目中：

- 通过 `CocoaPods` 管理依赖 (推荐使用)
- 手动导入 SDK 并管理依赖

##### Cocoapods导入SDK

ZTSDK支持的是Local Pods的方式集成，集成方式如下：

1、项目中profile文件所在目录下新建Frameworks文件夹（目录名可更改）

2、拷贝ZTSDK/Lib目录下的ZTSDK和ZTTunnelSDK到第一步建立的文件夹中

3、Podfile中主工程Target下配置：

```ruby
  pod 'Masonry'
  pod 'AFNetworking'
  pod "MBProgressHUD"
  pod 'SSZipArchive'
  pod 'MMKV'
  pod 'LarkSSO' #飞书登录 可选配置
  pod 'ZTSDK',                    :path => './Frameworks/ZTSDK' #NGN SDK
  pod 'MMWormhole',               :path => './Frameworks/MMWormhole'
  pod 'DTShareKit',		          :path => './Frameworks/DTShareKit' #钉钉登录 可选配置
  pod 'WXWork',		              :path => './Frameworks/WXWork' #企业微信登录 可选配置
```

4、Podfile中的Extension Target中配置：

```ruby
pod 'AFNetworking'
pod 'SSZipArchive'
pod 'ZTTunnelSDK',          :path => './Frameworks/ZTTunnelSDK'
```

5、Terminal 执行 `pod install` 即可完整集成零信任SDK。

```shell
pod install
```

##### 手动导入SDK

- 主工程

  1、主工程中导入以下SDK文件(ZTSDK/Frameworks目录下)

  | 文件                 | 说明                            | 注意事项     |
  | -------------------- | ------------------------------- | ------------ |
  | Core.framework       | 零信任的framework库             | Do Not Embed |
  | NGNCoreSDK.framework | 零信任的framework库             | Do Not Embed |
  | ZTSDK.framework      | 零信任的framework库             | Do Not Embed |
  | TPNResource.bundle   | 零信任SDK的资源                 |              |
  | ZTResource.bundle   | 零信任SDK的资源                 |              |
  | MMWormhole.framework | 虫洞的framework库，用于进程通信 | Do Not Embed |

  2、手动集成了零信任 SDK 之后，您需要在您的主工程中导入以下库 <font color=#FF000>（需导入Cocoapods集成方式中Podfile中所有依赖的库）</font>

    - libz.tbd
    - libc++.tbd
    - CoreMotion.framework
    - CoreTelephony.framework
    - AFNetworking.framework
    - NetworkExtension.framework
- Network Extension工程

  1、Network Extension工程中导入以下SDK文件(ZTTunnelSDK/Frameworks目录下)

  | 文件                  | 说明                            | 注意事项     |
  | --------------------- | ------------------------------- | ------------ |
  | Stack.framework       | 零信任的framework库             | Do Not Embed |
  | NGNStackSDK.framework | 零信任的framework库             | Do Not Embed |
  | ZTTunnelSDK.framework | 零信任的framework库             | Do Not Embed |
  | MMWormhole.framework  | 虫洞的framework库，用于进程通信 | Do Not Embed |

  2、手动集成了零信任 SDK 之后，您需要在您的Network Extension工程中导入以下库

    - libz.tbd
    - libc++.tbd
    - libresolv.9.tbd
    - CoreMotion.framework
    - AFNetworking.framework
    - NetworkExtension.framework

#### 集成SDK

##### 主工程

详见接口说明。

##### Network Extension工程

新建立的Network Extension工程中,PacketTunnelProvider类继承ZTPacketTunnelProvider类即可。

```objective-c
#import <ZTTunnelSDK/ZTPacketTunnelProvider.h>

@interface PacketTunnelProvider : ZTPacketTunnelProvider

@end
```

## 接口说明

### Android接口说明

#### 一、初始化SDK

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
    	<td colspan="4">void initSDK(Context context, String edition);</td>
		</tr>
    <tr>
      <th>功能</th>
      <td colspan="4">初始化SDK</td>
    </tr>
    <tr>
      <th>前置条件</th>
      <td colspan="4">无</td>
    </tr>
    <tr>
      <th>后置条件</th>
      <td colspan="4">无</td>
    </tr>
    <tr>
      <th rowspan="3">参数</th>
      <td width="15%">参数名</td>
      <td width="15%">类型</td>
      <td width="5%">方向</td>
      <td>说明</td>
    </tr>
    <tr>
      <td>context</td>
      <td>Context</td>
      <td>IN</td>
      <td>上下文环境</td>
    </tr>
    <tr>
      <td>edition</td>
      <td>String</td>
      <td>IN</td>
      <td>SDK版本，用于区分私有化和saas。一经设置后不可切换</td>
  	</tr>
    <tr>
      <th rowspan="1">说明</th>
      <td colspan="4">初始化SDK，此接口在所有接口调用前调用。该接口只可调用一次，多次调用无效。该值详见<a href="#android_Edition">Edition</a>。</td>
    </tr>
   <tr>
      <th rowspan="1">返回值</th>
      <td colspan="4">无</td>
    </tr>
</tbody>
</table>


##### 参数说明

- <span id='android_Edition'>Edition</span>

  该接口位于ZTConstant下，其提供安全检测状态枚举值，各值如下：

  | 属性       | 类型   | 值         | 说明                        |
    | ---------- | ------ | ---------- | --------------------------- |
  | SAAS       | String | saas       | 指定sdk初始化为saas形态。   |
  | ENTERPRISE | String | enterprise | 指定sdk初始化为私有化形态。 |

#### 二、隧道、登录等状态、修改密码及申请票据等事件的监听

##### 1、注册ZTSDK回调

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody><tr>
    <th width="10%">名称 </th>
    <td colspan="4">void registerListener(ZTListener listener);</td>
  </tr>
  <tr>
    <th>功能</th>
    <td colspan="4">注册ZTSDK回调</td>
  </tr>
  <tr>
    <th>前置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th>后置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th rowspan="2">参数</th>
    <td width="15%">参数名</td>
    <td width="15%">类型</td>
    <td width="5%">方向</td>
    <td>说明</td>
  </tr>
    <tr>
    <td>listener</td>
    <td>ZTListener</td>
    <td>IN</td>
    <td>需要反注册的ZTSDK回调对象</td>
  </tr>
  <tr>
    <th rowspan="1">说明</th>
    <td colspan="4">此接口在所有接口调用前调用（除initSDK接口之外）</td>
  </tr>
 <tr>
    <th rowspan="1">返回值</th>
    <td colspan="4">无</td>
  </tr>
</tbody>
</table>

##### 2、反注册ZTSDK回调

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody><tr>
    <th width="10%">名称 </th>
    <td colspan="4">void unregisterListener(ZTListener listener);</td>
  </tr>
  <tr>
    <th>功能</th>
    <td colspan="4">反注册ZTSDK回调</td>
  </tr>
  <tr>
    <th>前置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th>后置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th rowspan="2">参数</th>
    <td width="15%">参数名</td>
    <td width="15%">类型</td>
    <td width="5%">方向</td>
    <td>说明</td>
  </tr>
    <tr>
    <td>listener</td>
    <td>ZTListener</td>
    <td>IN</td>
    <td>需要反注册的ZTSDK回调对象</td>
  </tr>
  <tr>
    <th rowspan="1">说明</th>
    <td colspan="4">无</td>
  </tr>
 <tr>
    <th rowspan="1">返回值</th>
    <td colspan="4">无</td>
  </tr>
</tbody></table>
##### 参数说明

`ZTListener` ZTSDK回调监听器，接口参<a href="#android_status_listener">状态回调监听器</a>

##### 3、<span id="android_status_listener">状态回调监听器</span>

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void onCallback(Bundle bundle);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">ZTSDK回调接口</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>bundle</td>
      <td><a href="#android_bundle">Bundle</a></td>
    	<td>IN</td>
      <td>无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">回调内容封装在Bundle中。一级属性有值的情况下，再获取同功能下的二级属性值。</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 参数说明

- <span id="android_bundle">`Bundle`</span> 提供如下属性：

  | 一级属性        | 二级属性      | 类型                        | 值                                                           | 说明                                                         |
    | :-------------- | ------------- | :-------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
  | LOGIN_STATUS    |               | int                         | NOT_LOGGED = 1, // 未登录<br/>LOGGING = 2, // 登录中<br/>LOGGED = 3, // 已登录<br/>LOGGING_CANCEL = 4, // 取消登录，在未登录情况退出登录页时触发。仅使用iOA内置登录页登录时有效（即使用loginWithInnerPage方法登录时）。 | 登录状态码                                                   |
  |                 | RESULT_CODE   | int                         | NONE = 0, // 无错误<br/>RESET_PSW = 333333, // 重置密码      | 零信任SDK状态码                                              |
  |                 | RESULT_MSG    | String                      | ---                                                          | 状态码处理消息                                               |
  | TUNNEL_STATUS   |               | int                         | NOT_CONNECTED = 1, // 未连接<br/>CONNECTING = 2, // 连接中<br/>CONNECTED = 3, // 已连接 | 隧道状态码                                                   |
  |                 | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
  |                 | RESULT_MSG    | String                      | ---                                                          | 状态码处理消息                                               |
  | IOA_CODE        |               | String                      | ---                                                          | iOA颁发的票据                                                |
  |                 | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
  |                 | RESULT_MSG    | String                      | ---                                                          | 状态码处理消息                                               |
  |                 | IOA_USER_ID   | String                      | ---                                                          | 用户UserId                                                   |
  |                 | IOA_UID       | int                         | ---                                                          | 用户UID                                                      |
  |                 | IOA_MENU_ID   | String                      | ---                                                          | 组织域即用户目录ID                                           |
  |                 | IOA_DEVICE_ID | String                      | ---                                                          | IOA设备ID                                                    |
  | LOGIN_CHECK     |               | int                         | CHECK_LOGGED = 1, // 已登录<br>CHECK_NOT_LOGGED = 2, // 未登录 | 登录检查状态码                                               |
  |                 | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
  |                 | RESULT_MSG    | String                      | ---                                                          | 状态码处理消息                                               |
  | SD_STATUS       |               | int                         | 详见<a href="#android_SDStatus">SDStatus</a>。               | 安全检测状态                                                 |
  |                 | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
  |                 | RESULT_MSG    | String                      | ---                                                          | 状态码处理消息                                               |
  |                 | SD_RISK_INFO  | ArrayList&lt;SDRiskInfo&gt; | 详见<a href="#android_SDRiskInfo">SDRiskInfo</a>。           | 当安全检测不合规时，该属性会返回风险信息。具体风险项包装为SDRiskInfo，所有风险项包装为ArrayList。 |
  | RES_ACCESS_DENY |               | int                         | 详见<a href="#android_ResAccessDenyCode">ResAccessDenyCode</a>。 | 资源访问失败错误码                                           |
  |                 | RESULT_MSG    | String                      | ---                                                          | 资源访问失败的原因                                           |

- <span id='android_SDStatus'>SDStatus</span>

  该接口提供安全检测状态枚举值，各状态值如下：

  | 属性          | 类型 | 值   | 说明         |
        | ------------- | ---- | ---- | ------------ |
  | COMPLIANT     | int  | 1    | 合规状态     |
  | NON_COMPLIANT | int  | 2    | 不合规状态   |
  | TO_BE_CHECKED | int  | 3    | 待检测状态   |
  | NO_COMPLIANCE | int  | 4    | 合规策略为空 |

- <span id="android_SDRiskInfo">SDRiskInfo</span>

  该类提供了安全检测风险项的数据模型，具体如下：

  | 属性        | 类型   | 说明                                                         |
        | ----------- | ------ | ------------------------------------------------------------ |
  | mScanType   | int    | 风险类型，对应控制台的合规检测大项。扫描类型见：<a href="#android_SDScanType">SDScanType</a>。 |
  | mRiskName   | String | 威胁事件，对应控制台的威胁事件。                             |
  | mRiskDes    | String | 威胁事件描述。                                               |
  | mRiskLevel  | int    | 威胁事件评估，对应控制台的威胁事件评估。事件等级详见：<a href="#android_SDRiskLevel">SDRiskLevel</a>。 |
  | mDangerType | int    | 不合规等级，对应控制台的不合规操作。不合规等级见：<a href="#android_SDDangerType">SDDangerType</a>。 |
  | mAppName    | String | 应用名称，只在软件基线检测有用，即ScanType=4。               |
  | mAppVersion | String | 应用版本，只在软件基线检测有用，即ScanType=4。               |

- <span id="android_SDScanType">SDScanType</span>

  该接口提供合规检测大项的枚举值，各值如下：

  | 属性       | 类型 | 值   | 说明             |
    | ---------- | ---- | ---- | ---------------- |
  | APP        | int  | 1    | 病毒防护         |
  | NET        | int  | 2    | 网络防护         |
  | SYSTEM     | int  | 3    | 系统防护         |
  | BLACK_APPS | int  | 4    | 软件安全基线检测 |

- <span id='android_SDRiskLevel'>SDRiskLevel</span>

  该接口提供威胁事件评估枚举值，各值如下：

  | 属性   | 类型 | 值   | 说明   |
        | ------ | ---- | ---- | ------ |
  | LOW    | int  | 1    | 低风险 |
  | MIDDLE | int  | 2    | 中风险 |
  | HIGH   | int  | 3    | 高风险 |

- <span id='android_SDDangerType'>SDDangerType</span>

  该接口提供安全检测状态枚举值，各值如下：

  | 属性        | 类型 | 值   | 说明              |
        | ----------- | ---- | ---- | ----------------- |
  | ONLY_REMIND | int  | 1    | 不合规仅提醒      |
  | DISABLE_NGN | int  | 2    | 不合规禁用ngn连接 |

- <span id='android_ResAccessDenyCode'>ResAccessDenyCode</span>

  该接口提供资源访问失败枚举值，各值如下：

  | 属性                             | 类型 | 值    | 说明                       |
    | -------------------------------- | ---- | ----- | -------------------------- |
  | ERR_CODE_VPN_EXCEPTION           | int  | -100  | VPN异常断开                |
  | ERR_CODE_CLIENT_MTD_DETECT_BREAK | int  | -101  | 未进行合规检测             |
  | ERR_CODE_CLIENT_MTD_UPDATE_BREAK | int  | -102  | 合规测试已更新，需重新检测 |
  | ERR_CODE_CLIENT_MTD_DANGER_BREAK | int  | -103  | 合规检测发现风险           |
  | ERR_CODE_IOA_TICKET_EXPIRED      | int  | 10008 | 登录态失效                 |
  | ERR_CODE_DEVICE_IN_BLACKLIST     | int  | 10012 | 设备被加入黑名单           |
  | ERR_CODE_CONCURRENCY_EXCESS      | int  | 40001 | License并发数超限          |
  | ERR_CODE_NGN_RISK_SITE_ACCESS    | int  | 50001 | 风险资源禁止访问           |

#### 三、检查登录状态

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">void checkLogin();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">检查登录状态</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
     <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">通过 ZTListener 的 Bundle 的 CHECK_LOGIN 键获取检测结果</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 四、无界面方式登录

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">void login(ZTConfig ztConfig);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">登录</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>ztConfig</td>
    	<td>ZTConfig</td>
    	<td>IN</td>
      <td>帐密登录时的参数，参考<a href="#android_ztconfig">ZTConfig</a></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">1、此接口是异步接口，可能等待时间较长，建议接入方增加对话框等UI展示。<br/>
2、若ZTConfig.mServerUrl或者ZTConfig.mLoginConfig传空，调用此接口前已有登录态时，会使用已有的登录态。<br/>
3、若ZTConfig.mServerUrl和ZTConfig.mLoginConfig不为空，当上述传入的值与已有登录态的不一致时，会使用传入的值登录。<br/>
<b>4、Saas版不支持企业微信、政务微信、LDAP、RADIUS认证源。</b></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>
##### 参数说明

- <span id="android_ztconfig">`ZTConfig` </span>提供如下属性：

  | 属性         | 类型        | 必须 | 说明                                                         |
    | :----------- | :---------- | :--- | :----------------------------------------------------------- |
  | mContext     | Context     | 是   | 上下文环境                                                   |
  | mServerUrl   | String      | 否   | 零信任的服务器链接(https://host:port格式)，如有登录态，可传入空。该属性仅私有化版使用。 |
  | mPinCode     | String      | 否   | 零信任pin码。如有登录态，可传入空。该属性仅Saa版使用。       |
  | mLoginConfig | LoginConfig | 否   | 零信任SDK的登录参数配置，参LoginConfig，如有登录态，可传入空 |

- `LoginConfig` 提供如下属性：

| 属性         | 类型    | 值                                                           | 说明                                                         |
| ------------ | ------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| mDomainId    | String  | --                                                           | 组织域id（从iOA控制台可得），作用于登录，如传入有值，则从该组织域中登录，否则取iOA控制台配置的组织域列表中取第一个组织域登录。可选 |
| mAuthId      | String  | --                                                           | 认证源id。可选                                               |
| mAuthType    | String  | public interface AuthType { <br/>     String LARK = "Lark"; // 飞书    <br/>  String DING_TALK = "DingTalk"; // 钉钉    <br/>  String WE_COM_PRIVATE = "WeComPrivate"; // 政务微信   <br/>   String WE_COM = "WeCom"; // 企业微信    <br/>  String LDAP = "LDAP"; // LDAP    <br/>  String IOA = "iOA"; // 帐密    <br/>  String RADIUS = "RADIUS"; // RADIUS  <br/>} | 认证源类型。可选                                             |
| mUid         | String  | --                                                           | 帐号，作用于登录。帐密登录时即是用户帐号；第三方应用票据登录时可为空 |
| mCode        | String  | --                                                           | 密码，作用于登录。帐密码登录时即是用户密码，第三方应用票据登录时，即是其对应的票据。<br/>注意：当非一次密码时，例如帐密码登录的密码时，必须加密，则使LoginConfig.mEncryptCode为true |
| mEncryptCode | boolean | --                                                           | 是否对密码进行加密。当为true时，则会对密码加密，否则不会。   |
| mRedirectUri | String  | --                                                           | 用于SSO登录的重定向地址，可选。                              |

> 认证源id与认证源类型匹配实现逻辑：
>
> ```
> 1、认证源类型为空且认证源ID为空时，则取第一个认证源
> 2、认证源类型为空且认证源ID不为空时，则与传入认证源ID匹配
> 3、认证源类型不为空且认证源ID为空时，则与传入认证源类型匹配
> 4、认证源类型不为空且认证源ID不为空时，则同时与传入认证源ID和类型匹配
> ```

#### 五、使用iOA内置登录页面登录

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void loginWithInnerPage(Activity activity, String pinOrServerUrl);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">使用iOA内置登录页面登录</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="3">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>activity</td>
    	<td>Activity</td>
    	<td>IN</td>
      <td>应用当前的activity</td>
  	</tr>
    <tr>
    	<td>pinOrServerUrl</td>
    	<td>String</td>
    	<td>IN</td>
      <td>pin码或服务器url，Saas版传pin码；私有化版传serverUrl，serverUrl为零信任的服务器链接(https://host:port格式)。</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">登录状态通过ZTListener回调，登录成功后关闭内置登录页面</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 六、第三方应用快速登录

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void ssoLogin(ZTConfig ztConfig);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">第三方应用快速登录，用与将第三方登录态同步到iOA</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>ztConfig</td>
    	<td>ZTConfig</td>
    	<td>IN</td>
      <td>详见<a href="#android_ztconfig">ZTConfig</a>参数，saas版需要设置pinCode属性，私有化版需要设置serverUrl属性。将第三应用申请到的code设置到LoginConfig的mCode属性。</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">第三方应用快速登录，用与将第三方登录态同步到iOA。<b>该接口Saas版不支持。</b></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 七、登出

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">void logout();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">登出</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在调用login接口回调登录状态为LOGGED后，即是已有登录态下调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">1、若隧道状态是已连接，此时调用该接口，会关闭隧道</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 八、修改密码

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4"> void changePsw(ChangePswConfig changePswConfig);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">修改帐密登录时的密码</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">调用login接口回调登录状态为LOGGING，或者调用startTunnel接口回调隧道状态为CONNECTING，且回调RESULT_CODE为RESET_PSW后调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>changePswConfig</td>
    	<td>ChangePswConfig</td>
    	<td>IN</td>
      <td>修改密码时的参数，参考<a href="#android_changedpswconfig">ChangePswConfig</a></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 参数说明

- <span id="android_changedpswconfig">`ChangePswConfig`</span>提供如下属性：

  | 属性     | 类型   | 值   | 说明                     |
        | :------- | :----- | :--- | :----------------------- |
  | mUid     | String | --   | 登录零信任的帐号，必须   |
  | mCode    | String | --   | 登录零信任的旧密码，必须 |
  | mNewCode | String | --   | 登录零信任的新密码，必须 |

#### 九、通知栏消息通知

##### 1、开启通知栏消息通知

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">boolean enableNotification(Context context, Class activityClazz, int notificationIcon);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">开启通知栏消息通知</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="4">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>context</td>
    	<td>Context</td>
    	<td>IN</td>
      <td>上下文环境</td>
  	</tr>
    <tr>
    	<td>activityClazz</td>
    	<td>Class</td>
    	<td>IN</td>
      <td>点击通知栏消息时，跳转到的目标activity</td>
  	</tr>
    <tr>
    	<td>notificationIcon</td>
    	<td>int</td>
    	<td>IN</td>
      <td>通知栏消息显示的icon</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">成功开启通知栏消息通知后，以下情况会发送消息：<br/> 1、登录态过期<br/>2、安全连接异常断开，如在系统设置界面断开VPN等（注意：无网络不会自动断开安全连接）<br/>3、资源访问失败（资源访问失败原因：未进行合规检测、合规测试已更新需重新检测、合规检测发现风险、设备被加入黑名单、License并发数超限、风险资源禁止访问）<br/></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：开启成功，并且应用已获得系统通知栏权限，false：开启失败，业务侧需要先根据具体机型引导用户开启系统通知栏权限</td>
  	</tr>
	</tbody>通知栏消息
</table>

##### 2、关闭通知栏消息通知

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">boolean disableNotification();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">关闭通知栏消息通知</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
      <td>无</td>
      <td></td>
			<td></td>
    </tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：关闭通知成功，false：关闭通知失败</td>
  	</tr>
	</tbody>
</table>

#### 十、开启隧道

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">void startTunnel();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">开启隧道</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在初始化sdk、注册ZTSDK回调接口和登录完成后，判断隧道在线状态接口返回不在线时调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">此接口需要在登录完成后，判断隧道在线状态isTunnelOnline接口返回false时调用；是异步接口，可能等待时间较长，建议接入方增加对话框等UI展示。<br/></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>
#### 十一、关闭隧道

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void stopTunnel();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">关闭隧道</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在判断隧道在线状态接口返回在线时调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 十二、隧道状态检查

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">boolean isTunnelOnline();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">判断隧道在线状态</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：隧道状态为在线，false：隧道在线状态为不在线</td>
  	</tr>
	</tbody>
</table>
#### 十三、安全检测

**以下接口在 ZTAPI.SecurityDetectionAPI 类中。**

##### 1、设置地址位置权限请求器

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void setSDLocationPermissionRequester(PermissionRequester requester);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">地址位置权限请求接口</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>requester</td>
    	<td>PermissionRequester</td>
    	<td>IN</td>
      <td>地址位置权限请求器，请求权限完成并且成功则对PermissionRequester.OnRequestFinish.onFinish()传入OnRequestFinish.SUCCESS，失败则传入：OnRequestFinish.FAIL</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">安全检测在进行网络检测时，需要获取地理位置权限，才能获取到Wi-Fi进行扫描，在该接口中实现地理位置权限请求逻辑，如果不设置则采用默认的权限请求器</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 2、安全检测模式切换

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void setSecurityDetectionMode(boolean isAutoMode);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4"><b>启动安全检测功能模块和切换安全检测模式</b></td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">需登录成功后调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>isAutoMode</td>
    	<td>boolean</td>
    	<td>IN</td>
      <td>true为自动模式/false为手动模式</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
      <td colspan="4"><b>该接口可用于启动安全检测功能模块和切换安全检测模式。如果不调用该接口则安全检测功能模块默认不开启，该接口可多次调用用于切换安全检测模式。</b><br/>安全检测功能有两种模式：手动模式和自动模式。自动模式有如下特点:<br/>1.登录成功后自动进行安全检测；<br/>2.应用安装卸载触发App病毒检测；<br/>3.Wi-Fi切换触发网络检测（当应用处于后台的时候，可能会因为获取地理位置权限失败导致扫描失败）；<br/>4.策略变更时，自动进行安全检测；<br/>5.切换为自动模式自动进行安全检测；<br/></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 3、获取当前安全检测模式

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">int getSecurityDetectionMode();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">获取当前安全检测模式</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">需登录成功后调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
      <td colspan=4>无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">该接口返回当前安全检测模式</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
      <td colspan="4">返回值为int类型，int值对应的模式详见<a href="#android_SecurityDetectionMode">SecurityDetectionMode</a>。</td>
  	</tr>
	</tbody>
</table>

参数说明

- <span id='android_SecurityDetectionMode'>SecurityDetectionMode</span>

该接口提供安全检测模式枚举值，各值如下：

| 属性           | 类型 | 值   | 说明                                       |
| -------------- | ---- | ---- | ------------------------------------------ |
| SD_MODE_NONE   | int  | 0    | 安全检测模式未设置即安全检测功能模块未启用 |
| SD_MODE_AUTO   | int  | 1    | 自动模式                                   |
| SD_MODE_MANUAL | int  | 2    | 手动模式                                   |

##### 4、<span id="android_startSecurityDetection">开始安全检测</span>

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void startSecurityDetection();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">开始安全检测</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">需登录成功后调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">开始安全检测</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 5、停止安全检测

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">void stopSecurityDetection();</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">停止安全检测</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
      <td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">停止安全检测</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 十三、其它

##### 1、运行日志

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">File getLogZipFile(Context context);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">同步接口，获取ZTSDK的日志包，包格式为zip</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>context</td>
    	<td>Context</td>
    	<td>IN</td>
      <td>无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">此接口为同步接口，会卡住UI界面，需要接入业务自己实现异步调用</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">File</td>
  	</tr>
	</tbody>
</table>
##### 2、票据申请

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">void applyIOACode(String appId);</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">申请iOA票据</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在调用login接口回调登录状态为LOGGED或者调用startTunnel接口回调隧道状态为CONNECTED后，即是已有登录态下调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
     <tr>
    	<td>appId</td>
    	<td>String</td>
    	<td>IN</td>
      <td>appId需要在iOA控制台上申请，申请路径为：iOA控制台-策略中心-身份安全策略-认证安全-SSO管理</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">通过ZTListener回调code、userid、uid、groupid等信息。<b>该接口Saas版不支持。</b></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

### iOS接口说明

#### 一、隧道、登录等状态、修改密码和申请票据等事件的监听

##### 1、初始化SDK

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody><tr>
    <th width="10%">名称 </th>
    <td colspan="4">+(void)initSDK:(SdkVersion)sdkVersion;</td>
  </tr>
  <tr>
    <th>功能</th>
    <td colspan="4">初始化ZTSDK，确定SDK版本</td>
  </tr>
  <tr>
    <th>前置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th>后置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th rowspan="2">参数</th>
    <td width="15%">参数名</td>
    <td width="15%">类型</td>
    <td width="5%">方向</td>
    <td>说明</td>
  </tr>
    <tr>
    <td>sdkVersion</td>
    <td>SdkVersion</td>
    <td>IN</td>
    <td>私有化版：ZTSDK_ENTERPRISE <br/> SAAS版：ZTSDK_SAAS<br/>一经设置后不支持切换</td>
  </tr>
  <tr>
    <th rowspan="1">说明</th>
    <td colspan="4">此接口在所有接口调用前调用，多次初始化无效</td>
  </tr>
 <tr>
    <th rowspan="1">返回值</th>
    <td colspan="4">无</td>
  </tr>
</tbody>
</table>


##### 2、注册ZTSDK回调

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody><tr>
    <th width="10%">名称 </th>
    <td colspan="4">+(void)registerListener:(ZTListener *)listener;</td>
  </tr>
  <tr>
    <th>功能</th>
    <td colspan="4">注册ZTSDK回调</td>
  </tr>
  <tr>
    <th>前置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th>后置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th rowspan="2">参数</th>
    <td width="15%">参数名</td>
    <td width="15%">类型</td>
    <td width="5%">方向</td>
    <td>说明</td>
  </tr>
    <tr>
    <td>listener</td>
    <td>ZTListener</td>
    <td>IN</td>
    <td>需要反注册的ZTSDK回调对象</td>
  </tr>
  <tr>
    <th rowspan="1">说明</th>
    <td colspan="4">调用所有功能性接口前调用，避免无法接收回调</td>
  </tr>
 <tr>
    <th rowspan="1">返回值</th>
    <td colspan="4">无</td>
  </tr>
</tbody>
</table>

##### 3、反注册ZTSDK回调

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody><tr>
    <th width="10%">名称 </th>
    <td colspan="4">+(void)unregisterListener:(ZTListener *)listener;</td>
  </tr>
  <tr>
    <th>功能</th>
    <td colspan="4">反注册ZTSDK回调</td>
  </tr>
  <tr>
    <th>前置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th>后置条件</th>
    <td colspan="4">无</td>
  </tr>
  <tr>
    <th rowspan="2">参数</th>
    <td width="15%">参数名</td>
    <td width="15%">类型</td>
    <td width="5%">方向</td>
    <td>说明</td>
  </tr>
    <tr>
    <td>listener</td>
    <td>ZTListener</td>
    <td>IN</td>
    <td>需要反注册的ZTSDK回调对象</td>
  </tr>
  <tr>
    <th rowspan="1">说明</th>
    <td colspan="4">无</td>
  </tr>
 <tr>
    <th rowspan="1">返回值</th>
    <td colspan="4">无</td>
  </tr>
</tbody></table>

##### 参数说明

`ZTListener` ZTSDK回调监听器，接口参<a href="#ios_status_listener">状态回调监听器</a>

##### 4、<span id="ios_status_listener">状态回调监听器</span>

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">- (void)onCallback:(Bundle *)bundle;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">ZTSDK回调接口</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>bundle</td>
    	<td><a href="#ios_bundle">Bundle</a></td>
    	<td>IN</td>
      <td>无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">回调内容封装在Bundle中</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>
##### 参数说明

- <span id="ios_bundle">`Bundle`</span> 提供如下属性：

| 一级属性      | 二级属性      | 类型                        | 值                                                           | 说明                                                         |
| :------------ | ------------- | :-------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| LOGIN_STATUS  |               | int                   | NOT_LOGGED = 1, // 未登录<br/>LOGGING = 2, // 登录中<br/>LOGGED = 3, // 已登录<br/>LOGGING_CANCEL = 4, // 取消登录，在未登录情况退出登录页时触发。 | 登录状态码，通过getLoginStatus方法获取                       |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误<br/>RESET_PSW = 333333, // 重置密码      | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                    | ---                                                          | 状态码处理消息                                               |
| TUNNEL_STATUS |               | int                         | NOT_CONNECTED = 1, // 未连接<br/>CONNECTING = 2, // 连接中<br/>CONNECTED = 3, // 已连接 | 隧道状态码，通过getTunnelStatus方法获取                      |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                      | ---                                                          | 状态码处理消息                                               |
| IOA_CODE      |               | NSString                      | ---                                                          | iOA颁发的票据，通过getIOACode方法获取                        |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                      | ---                                                          | 状态码处理消息                                               |
|               | IOA_USER_ID   | NSString                      | ---                                                          | 用户UserId,通过getIOAUserId方法获取                          |
|               | IOA_UID       | NSString                         | ---                                                          | 用户UID,通过getIOAUId方法获取                                |
|               | IOA_MENU_ID   | NSString                      | ---                                                          | 组织域即用户目录ID，通过getIOAMenuID方法获取                 |
|               | IOA_MID | NSString                      | ---                                                          | IOA设备ID，通过getIOAMID方法获取                             |
| LOGIN_CHECK   |               | int                         | CHECK_LOGGED = 1, //已登录<br/>CHECK_NOT_LOGGED = 2,//未登录 | 登录检查状态码，通过getCheckLoginResult获取                  |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                      | ---                                                          | 状态码处理消息                                               |
| SD_STATUS     |               | int                         | TO_BE_CHECKED=1,// 待检测<br/>COMPLIANT= 2,// 设备安全<br/>NON_COMPLIANT= 3,// 设备不安全<br/>NO_COMPLIANCE=4,// 空策略</br>          | 安全检测状态,通过getSecStatus方法获取                                                 |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                      | ---                                                          | 状态码处理消息                                               |
|               | SD_RISK_INFO  | NSArray&lt;SDRiskInfo&gt; | 详见<a href="#ios_SecurityInfo">SecurityInfo</a>。           | 当安全检测不合规时，该属性会返回风险信息。通过getSecResult方法获取。 |
| SD_MODE     |               | int                         | SD_MODE_AUTO = 0, //自动检测<br/>SD_MODE_MANUAL = 1, //手动发起<br/>SD_MODE_NONE = 2, //未启动安全扫描<br/> | 安全检测模式,通过getSecMode方法获取                                                 |
| RES_ACCESS_DENY     |               | int                         |     ERR_CODE_CLIENT_MTD_DETECT_BREAK = -101,  // 未进行合规检测<br/>ERR_CODE_CLIENT_MTD_UPDATE_BREAK = -102,  // 合规测试已更新，需重新检测<br/>ERR_CODE_CLIENT_MTD_DANGER_BREAK = -103,  // 合规检测发现风险<br/>ERR_CODE_IOA_TICKET_EXPIRED = 10008, // 登录态失效<br/>ERR_CODE_DEVICE_IN_BLACKLIST = 10012, // 黑名单设备阻断<br/>ERR_CODE_NGN_CONCURRENCY_EXCESS = 40001, // License并发数超限<br/>ERR_CODE_NGN_RISK_SITE_ACCESS = 50001, // 风险资源禁止访问| 访问阻拦错误吗，通过getAccessDenyCode方法获取        |
|               | RESULT_CODE   | int                         | NONE = 0, // 无错误                                          | 零信任SDK状态码                                              |
|               | RESULT_MSG    | NSString                      | ---                                                          | 状态码处理消息，携带访问阻拦原因描述                                               |

- <span id="ios_SecurityInfo">`SecurityInfo`</span> 提供如下属性：

| 属性        | 类型       | 值                                                                                 | 说明                                                          |
| ----------- | ---------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| mDangerType | DangerType | ONLY_REMIND = 0, DISABLE_NGN = 1                                                   | 危险类型，包括仅提醒和阻断安全连接                            |
| mScanType   | ScanType   | SCAN_NETWORK = 0, SCAN_SYSTEM = 1                                                  | 扫描类型，包括网络防护和系统防护                              |
| mRiskName   | RiskName   | SystemRoot = 1, ArpAttack = 2, DnsHijack = 3, PhishingWifi = 4, SSLStripAttack = 5 | 风险名称，包括越狱、ARP攻击、DNS劫持、钓鱼Wi-Fi和SSLStrip攻击 |
| mRiskLevel  | RishLevel  | MID = 0, HIGH = 1                                                                  | 风险级别，包括中和高                                          |
| mRiskDes    | NSString   | 无                                                                                 | 风险描述                                                      |

#### 二、登录

##### 1、无页面登录
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)login(ZTConfig *)ztConfig;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">登录</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>ztConfig</td>
    	<td>ZTConfig</td>
    	<td>IN</td>
      <td>帐密登录时的参数，参考<a href="#ios_ztconfig">ZTConfig</a></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">1、此接口是异步接口，可能等待时间较长，建议接入方增加对话框等UI展示。<br/>
2、若ZTConfig.mServerUrl或者ZTConfig.mLoginConfig传空，调用此接口前已有登录态时，会使用已有的登录态。<br/>
3、若ZTConfig.mServerUrl和ZTConfig.mLoginConfig不为空，当上述传入的值与已有登录态的不一致时，会使用传入的值登录。</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 参数说明

- <span id="ios_ztconfig">`ZTConfig` </span>提供如下属性：

| 属性         | 类型        | 必须 | 说明                                                            |
| :----------- | :---------- | :--- | :-------------------------------------------------------------- |
| mServerUrl   | NSString    | 否   | 私有化版：零信任的服务器链接(https://host:port格式)，如有登录态，可传入空<br />  |
| mPinCode   | NSString    | 否   | SAAS版：控制台获取的6位pin码，如有登录态，可传入空<br />|
| mLoginConfig | LoginConfig | 否   | 零信任SDK的登录参数配置，参LoginConfig，如有登录态，可传入空    |

- `LoginConfig` 提供如下属性：

  | 属性         | 类型     | 值                                                                                                                                                                                                                                                                                      | 说明                                                                                                                                                                                |
  | ------------ | -------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | mDomainId    | NSString | --                                                                                                                                                                                                                                                                                      | 组织域id（从iOA控制台可得），作用于登录，如传入有值，则从该组织域中登录，否则取iOA控制台配置的组织域列表中取第一个组织域登录。可选                                                  |
  | mAuthId      | NSString | --                                                                                                                                                                                                                                                                                      | 认证源id。可选                                                                                                                                                                      |
  | mAuthType    | NSString | NSString *const LARK = @"Lark";<br/>NSString *const DING_TALK = @"DingTalk";<br/>NSString *const WE_COM = @"WeCom";<br/>NSString *const WE_COM_PRIVATE = @"WeComPrivate";<br/>NSString *const IOA = @"iOA";<br/>NSString *const LDAP = @"LDAP";<br/>NSString *const RADIUS = @"RADIUS"; | 认证源类型。可选                                                                                                                                                                    |
  | mUid         | NSString | --                                                                                                                                                                                                                                                                                      | 帐号，作用于登录。帐密登录时即是用户帐号；第三方应用票据登录时可为空                                                                                                                |
  | mCode        | NSString | --                                                                                                                                                                                                                                                                                      | 密码，作用于登录。帐密码登录时即是用户密码，第三方应用票据登录时，即是其对应的票据。<br/>注意：当非一次密码时，例如帐密码登录的密码时，必须加密，则使LoginConfig.mEncryptCode为true |
  | mEncryptCode | BOOL     | --                                                                                                                                                                                                                                                                                      | 是否对密码进行加密。当为true时，则会对密码加密，否则不会。                                                                                                                          |
  | mSSOCode | NSString     | --                                                                                                                                                                                                                                                                                      | 第三方SSO登录Code。                                                                                                                          |
  | mRedirectURI | NSString     | --                                                                                                                                                                                                                                                                                      | 第三方SSO登录重定向地址，可选。                                                                                                                          |

  > 认证源id与认证源类型匹配实现逻辑：
  >
  > ```
  > 1、认证源类型为空且认证源ID为空时，则取第一个认证源
  > 2、认证源类型为空且认证源ID不为空时，则与传入认证源ID匹配
  > 3、认证源类型不为空且认证源ID为空时，则与传入认证源类型匹配
  > 4、认证源类型不为空且认证源ID不为空时，则同时与传入认证源ID和类型匹配
  > ```

##### 2、修改密码
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)changePsw:(ChangePswConfig *)changePswConfig;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">修改帐密登录时的密码</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">调用login接口回调登录状态为LOGGING，或者调用startTunnel接口回调隧道状态为CONNECTING，且回调RESULT_CODE为RESET_PSW后调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>changePswConfig</td>
    	<td>ChangePswConfig</td>
    	<td>IN</td>
      <td>修改密码时的参数，参考<a href="#ios_changedpswconfig">ChangePswConfig</a></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 参数说明

- <span id="ios_changedpswconfig">`ChangePswConfig`</span>提供如下属性：

  | 属性     | 类型     | 值   | 说明                     |
  | :------- | :------- | :--- | :----------------------- |
  | mUid     | NSString |      | 登录零信任的帐号，必须   |
  | mCode    | NSString |      | 登录零信任的旧密码，必须 |
  | mNewCode | NSString |      | 登录零信任的新密码，必须 |

##### 3、第三方App回调处理

<table id="ios_openURL" width="1000" border="1" style="margin-bottom:40px">
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+ (BOOL)applicationDidOpenURL:(NSURL *)url;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">第三方App回调处理</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>url</td>
    	<td>NSURL</td>
    	<td>IN</td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">若使用第三方登录，需要在AppDelegate中- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary *)options函数中调用此接口</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">BOOL</td>
  	</tr>
	</tbody>
</table>

##### 4、私有化版带界面登录
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+ (void)loginWithInnerPage:(UIViewController *)currentVC host:(NSString *)host port:(NSString *)port;
		</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">拉起内置登录页面</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">若使用第三方登录，务必按照<a href="#ios_openURL">2.3</a>完成回调处理</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="4">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>currentVC</td>
    	<td>UIViewController</td>
    	<td>IN</td>
      <td>当前页面ViewController</td>
  	</tr>
	<tr>
    	<td>host</td>
    	<td>NSString</td>
    	<td>IN</td>
      <td>服务器地址</td>
  	</tr>
	<tr>
    	<td>port</td>
    	<td>NSString</td>
    	<td>IN</td>
      <td>服务器端口</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">登录状态通过ZTListener回调</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 5、SAAS版带界面登录
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+ (void)loginWithInnerPage:(UIViewController *)currentVC pinCode:(NSString *)pinCode;
		</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">拉起内置登录页面</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">若使用第三方登录，务必按照<a href="#ios_openURL">2.3</a>完成回调处理</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="3">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>currentVC</td>
    	<td>UIViewController</td>
    	<td>IN</td>
      <td>当前页面ViewController</td>
  	</tr>
	<tr>
    	<td>pinCode</td>
    	<td>NSString</td>
    	<td>IN</td>
      <td>pin码</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">登录状态通过ZTListener回调</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 6、第三方快速登录
<table width="1000" border="1" style="margin-bottom:40px"> <tbody> <tr> <th width="10%">名称 </th> <td colspan="4">+ (void)loginWithSSOConfig:(ZTConfig *)ztConfig;</td> </tr> <tr> <th>功能</th> <td colspan="4">第三方SSO授权code登录</td> </tr> <tr> <th>前置条件</th> <td colspan="4">无</td> </tr> <tr> <th>后置条件</th> <td colspan="4">无</td> </tr> <tr> <th rowspan="2">参数</th> <td width="15%">参数名</td> <td width="15%">类型</td> <td width="5%">方向</td> <td>说明</td> </tr> <td>ztConfig</td>
    	<td>ZTConfig</td>
    	<td>IN</td>
      <td>帐密登录时的参数，参考<a href="#ios_ztconfig">ZTConfig</a></td> <tr> <th rowspan="1">说明</th> <td colspan="4">登录状态通过ZTListener回调。<font color=#FF000>SAAS版暂未提供该功能。</font></td> </tr> <tr> <th rowspan="1">返回值</th> <td colspan="4">无</td> </tr> </tbody> </table>

##### 7、登出
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)logout;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">登出</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在调用login接口回调登录状态为LOGGED后，即是已有登录态下调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">1、若隧道状态是已连接，此时调用该接口，会关闭隧道</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 8、检测登录状态

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)checkLogin;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">检查登录状态</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
     <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">通过 ZTListener 的 Bundle 的 getCheckLoginResult 获取检测结果</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

#### 三、隧道
##### 1、开启隧道
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)startTunnel;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">开启隧道</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在注册ZTSDK回调接口和判断隧道在线状态接口返回不在线时调用,开启隧道前用户需已登录</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td><a href="#ios_ztconfig"></a></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">1、此接口需要在判断隧道在线状态isTunnelOnline接口返回false时调用；是异步接口，可能等待时间较长，建议接入方增加对话框等UI展示。<br/>
        2、需要用户为已登录状态
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 2、关闭隧道
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+(void)stopTunnel;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">关闭隧道</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在判断隧道在线状态接口返回在线时调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 3、关闭隧道-同步阻塞接口
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+(BOOL)stopTunnelSync;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">关闭隧道</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在判断隧道在线状态接口返回在线时调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

##### 4、隧道状态检测
<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+(BOOL)isTunnelOnline;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">判断隧道在线状态</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：隧道状态为在线，false：隧道在线状态为不在线</td>
  	</tr>
	</tbody>
</table>

##### 5、开启隧道连接异常状态通知

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+ (BOOL)enableNotification;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">开启隧道连接异常状态通知</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">成功开启通知栏消息通知后，以下情况会发送消息：<br/>1、登录态过期 <br/>2、资源访问失败（资源访问失败原因：未进行合规检测、合规测试已更新需重新检测、合规检测发现风险、设备被加入黑名单、License并发数超限、风险资源禁止访问）<br/><font color=#FF000>注：未开启通知时，若发生访问拦截无法通知用户，ZTSDK回到前台时可通过<font color=#FF000><a href="#ios_bundle">Bundle</a></font>中RES_ACCESS_DENY属性获取拦截原因</font></td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：开启成功，并且应用已获得系统通知栏权限，false：开启失败，业务侧需要先根据具体机型引导用户开启系统通知栏权限</td>
  	</tr>
	</tbody>
</table>


##### 6、关闭隧道连接异常状态通知

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+ (BOOL)disableNotification;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">关闭隧道连接异常状态通知</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td></td>
    	<td></td>
      <td></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">true：关闭通知成功，false：关闭通知失败</td>
  	</tr>
	</tbody>
</table>

#### 四、安全扫描

##### 1、启用安全扫描功能

<table width="1000" border="1" style="margin-bottom:40px"> <tbody> <tr> <th width="10%">名称 </th> <td colspan="4">+(BOOL)setSecurityDetectionMode:(BOOL)isAutoMode;</td> </tr> <tr> <th>功能</th> <td colspan="4">1、启用安全扫描<br/>2、设置是否自动发起安全扫描</td> </tr> <tr> <th>前置条件</th> <td colspan="4">账号已登录</td> </tr> <tr> <th>后置条件</th> <td colspan="4">无</td> </tr> <tr> <th rowspan="2">参数</th> <td width="15%">参数名</td> <td width="15%">类型</td> <td width="5%">方向</td> <td>说明</td> </tr> <tr> <td>isAutoMode</td> <td>BOOL</td> <td>输入</td> <td>自动扫描</td> </tr> <tr> <th rowspan="1">说明</th> <td colspan="4"><font color=#FF000>默认不启用安全扫描功能，若需启用请调用此接口并设置扫描模式<font/></td> </tr> <tr> <th rowspan="1">返回值</th> <td colspan="4">是否设置成功：账号未登录时失败</td> </tr> </tbody> </table>

##### 2、发起安全扫描

<table width="1000" border="1" style="margin-bottom:40px"> <tbody> <tr> <th width="10%">名称 </th> <td colspan="4">+ (BOOL)startSecurityDetection;</td> </tr> <tr> <th>功能</th> <td colspan="4">请求安全扫描</td> </tr> <tr> <th>前置条件</th> <td colspan="4">账号已登录且启用安全扫描功能</td> </tr> <tr> <th>后置条件</th> <td colspan="4">无</td> </tr> <tr> <th rowspan="2">参数</th> <td width="15%">参数名</td> <td width="15%">类型</td> <td width="5%">方向</td> <td>说明</td> </tr> <tr> <td>无</td> <td></td> <td></td> <td></td> </tr> <tr> <th rowspan="1">说明</th> <td colspan="4"><font color=#FF000>未启用安全扫描功能时候调用此接口无效<font/></td> </tr> <tr> <th rowspan="1">返回值</th> <td colspan="4">是否发起安全扫描：账号未登录时失败</td> </tr> </tbody> </table>

##### 3、获取安全扫描功能开启状态

<table width="1000" border="1" style="margin-bottom:40px"> <tbody> <tr> <th width="10%">名称 </th> <td colspan="4">+(int)getSecurityDetectionMode;</td> </tr> <tr> <th>功能</th> <td colspan="4">当前账号安全扫描功能状态</td> </tr> <tr> <th>前置条件</th> <td colspan="4">账号已登录</td> </tr> <tr> <th>后置条件</th> <td colspan="4">无</td> </tr> <tr> <th rowspan="2">参数</th> <td width="15%">参数名</td> <td width="15%">类型</td> <td width="5%">方向</td> <td>说明</td> </tr> <tr> <td>无</td> <td></td> <td></td> <td></td> </tr> <tr> <th rowspan="1">说明</th> <td colspan="4">无</td> </tr> <tr> <th rowspan="1">返回值</th> <td colspan="4">    SD_MODE_AUTO = 0, //自动检测<br/>SD_MODE_MANUAL = 1, //手动发起<br/>SD_MODE_NONE = 2, //未启动安全扫描</td> </tr> </tbody> </table>

#### 五、其它

##### 1、运行日志

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
   		<td colspan="4">+(NSString *)getLogZipFile;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">同步接口，获取ZTSDK的日志包，包格式为zip</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
    <tr>
    	<td>无</td>
    	<td>无</td>
    	<td>IN</td>
      <td>无</td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">此接口为同步接口，会卡住UI界面，需要接入业务自己实现异步调用</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">NSString</td>
  	</tr>
	</tbody>
</table>

##### 2、票据申请

<table width="1000" border="1" style="margin-bottom:40px">
  <tbody>
    <tr>
    	<th width="10%">名称 </th>
      <td colspan="4">+(void)applyIOACode:(NSString *)appId;</td>
  	</tr>
  	<tr>
    	<th>功能</th>
    	<td colspan="4">申请iOA票据</td>
  	</tr>
  	<tr>
    	<th>前置条件</th>
    	<td colspan="4">在调用login接口回调登录状态为LOGGED或者调用startTunnel接口回调隧道状态为CONNECTED后，即是已有登录态下调用</td>
  	</tr>
  	<tr>
    	<th>后置条件</th>
    	<td colspan="4">无</td>
  	</tr>
  	<tr>
    	<th rowspan="2">参数</th>
    	<td width="15%">参数名</td>
    	<td width="15%">类型</td>
    	<td width="5%">方向</td>
    	<td>说明</td>
  	</tr>
     <tr>
    	<td>appId</td>
    	<td>NNString</td>
    	<td>IN</td>
      <td>appId需要在iOA控制台上申请，申请路径为：iOA控制台-策略中心-身份安全策略-认证安全-SSO管理。<font color=#FF000>SAAS版暂未提供该功能。</font></td>
  	</tr>
  	<tr>
    	<th rowspan="1">说明</th>
    	<td colspan="4">无</td>
  	</tr>
 		<tr>
    	<th rowspan="1">返回值</th>
    	<td colspan="4">无</td>
  	</tr>
	</tbody>
</table>

###  

#### 附件
1、[内置登录页面效果演示](https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/%E9%99%84%EF%BC%9A%E5%86%85%E7%BD%AE%E7%99%BB%E5%BD%95%E9%A1%B5%E9%9D%A2%E6%95%88%E6%9E%9C%E6%BC%94%E7%A4%BA.mp4)

2、[身份认证服务接口文档](https://github.com/Tencent-iOA/ioa-open-doc/raw/master/resource/mobilesdk/%E9%99%84%EF%BC%9A%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81%E6%9C%8D%E5%8A%A1%E6%8E%A5%E5%8F%A3%E6%96%87%E6%A1%A3.pdf)
