# SetCasterConfig {#reference2997 .reference}

配置导播台，全量覆盖配置信息，若指定参数置为空则清除导播台该项配置。

## 请求参数 {#section_k4f_qm1_dfb .section}

|参数|类型|是否必选|描述|
|:-|:-|:---|:-|
|Action|String|是|操作接口名，系统规定参数，取值：SetCasterConfig|
|CasterId|String|是|导播台Id|
|CasterName|String|否|导播台名称|
|DomainName|String|否|域名，请您在导播台启动前完成域名配置。若该参数为空，默认清除导播台域名配置。

|
|TranscodeConfig|String|否|转码配置。JSON格式字符串，结构体内部字段请按首字母大写，驼峰格式输入。

若该参数设置为空，默认清除转码配置。

|
|RecordConfig|String|否|录制配置，参数设置为空时表示不启用录制功能。JSON格式字符串，结构体内部字段请按首字母大写，驼峰格式输入。

若该参数置为空，默认清除录制配置。

|
|Delay|Float|否|延时播放。-   默认：禁用延播
-   0：禁用延时
-   大于0：为启用延时
-   时间单位：秒
-   若该参数置为空，默认清除延播配置。

|
|UrgentMaterialId|String|否|备播视频，媒资库素材Id若该参数置为空，默认清除备播配置。|
|SideOutputUrl|String|否|用户自定义导播台旁路输出地址。若该参数为空，则默认使用阿里云自动生成的输出地址。

|
|CallbackUrl|String|否|用户回调地址。若需要接收回调通知，请输入可用的接收地址，接受http协议。若该参数置为空，默认取消导播台回调通知。

|
|ProgramName|String|否|轮播台名称，若使用轮播功能时可配置。|
|ProgramEffect|Integer|否|轮播生效标志。-   0-不生效，
-   1-生效

|
|ChannelEnable|Integer|否|是否启用Channel。-   0-不启用Channel,
-   1-启用Channel。

默认不启用，且启用后不可取消；不启用channel时Resource直接被布局引用，首次开启Channel需要在导播台停止的状态下进行，之前已存在的布局将被废弃，Resource需要首先设置到Channel中，新增的布局直接引用Channel，通过Channel可调整视频源播放进度和播放状态，该模式下视频源、PVW、PGM三区域若引用同一Resource，则对应画面将保持同步。|

RecordConfig

|参数|类型|是否必选|描述|
|:-|:-|:---|:-|
|VideoFormat|VideoFormat\[\]|是|录制格式配置|
|OssBucket|String|是|存储位置|
|OssEndpoint|String|是|oss endpoint|

VideoFormat

|参数|类型|是否必选|描述|
|:-|:-|:---|:-|
|Format|String|是|录制格式|
|OssObjectPrefix|String|是|录制文件名|
|SliceOssObjectPrefix|String|是|切片名称|
|CycleDuration|Integer|是|录制时长|

TranscodeConfig

|参数|类型|是否必选|描述|
|:-|:-|:---|:-|
|CasterTemplate|String|否|导播台转码配置。-   lp\_ld：流畅
-   lp\_sd：标清
-   lp\_hd：高清
-   lp\_ud：超清
-   lp\_ld\_v：竖屏流畅
-   lp\_sd\_v：竖屏标清
-   lp\_hd\_v：竖屏高清
-   lp\_ud\_v：竖屏超清
-   采用后付费方式时为必输参数。
-   采用预付费方式时如果未输入参数，默认使用创建导播台时预设的导播台转码配置。

|
|LiveTemplate|\[\]String|否|直播转码配置。-   lsd：标清
-   lld：流畅
-   lud：超清
-   lhd：高清

为保证转码输出与导播输出一致，推荐使用宽高自适应转码模板。

-   daobo-lsd：标清
-   daobo-lld：流畅
-   daobo-lud：超清
-   daobo-lhd：高清

|

## 返回参数 {#section_p4f_qm1_dfb .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|该条任务请求Id|
|CasterId|String|导播台Id|

## 示例 {#section_zcx_4j1_dfb .section}

请求示例

```
https://live.aliyuncs.com?Action=SetCasterConfig&DomainName=XXXXXX&UrgentMaterialId=6cf724c6ebfd4a59b5b3cec6f10d5ecf&TranscodeConfig=%7B%22casterTemplate%22%3A%22test_tpl%22%2C%22liveTemplate%22%3A%5B%22lld%22%2C%22lld%22%5D%7D&Timestamp=2017-09-30T03%3A22%3A32Z&Delay=30.0&SignatureVersion=1.0&CasterName=coco&Format=XML&SignatureNonce=0ec1a85d-8bcb-4af1-9c46-3a56acf8ba91&Version=2016-11-01&AccessKeyId=LTAIiu0F8jaIh6GM&Signature=YGM4MEfXqZ7sigu4fe%2F6zmljONE%3D&SignatureMethod=HMAC-SHA1&RegionId=cn-shanghai&CasterId=9751573c-a3c2-4093-b302-c80986f0e4a8&RecordConfig=%7B%22endpoint%22%3A%22XXXXXX%22%2C%22videoFormat%22%3A%5B%7B%22prefix%22%3A%22record%2F%7BAppName%7D%2F%7BStreamName%7D%2F%7BStartTime%7D_%7BEndTime%7D%22%2C%22format%22%3A%22flv%22%2C%22interval%22%3A900%7D%2C%7B%22prefix%22%3A%22record%2F%7BAppName%7D%2F%7BStreamName%7D%2F%7BStartTime%7D_%7BEndTime%7D%22%2C%22format%22%3A%22m3u8%22%2C%22slicePrefix%22%3A%22record%2F%7BAppName%7D%2F%7BStreamName%7D%2F%7BUnixTimestamp%7D%22%2C%22interval%22%3A900%7D%5D%2C%22ossBucket%22%3A%22record-bucket-test%22%2C%22interval%22%3A%225%22%7D
```

返回示例

```
{
    "RequestId": "16A96B9A-F203-4EC5-8E43-CB92E68F4CD8",
    "casterId": "b4810848-bcf9-4aef-bd4a-e6bba2d966c8"
}
```

## 特殊错误码 {#section_w32_ln3_dfb .section}

|错误代码|描述|Http 状态码|语义|
|:---|:-|:-------|:-|
|IllegalOperation|Permission Denied|401|无权访问导播台|
|InvalidCaster.NotFound|Caster is not found.|404|指定导播台不存在|
|CasterTemplateUnavailable|CasterTemplate exceeded norms|401|当前导播台分辨率不可用|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误|

