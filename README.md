#ONT ID托管设计概要和接口

## 设计背景

### 扩展应用场景
基础的ONT ID是基于密码学公私钥体系设计的非中心化账户体系。在更多的实际运用场景中，我们要求ONT ID的开通和管理需要扩展嵌入到各种场景，同时包括PC端、移动端等各种渠道，我们需要一个更完善、更接地气的综合账户体系，综合账户体系支持把数字身份、数字资产、中心账户一并管理和管理。为便于理解，以下列举部分非常典型和具体的场景应用： 
* 在AAPP Store PC端应用中，用户需要在PC页面中及时开通ONT ID；
* 在各种营销活动中，移动端H5页面随处需要开通ONT ID;
* 在一些移动端钱包中，可以支持用户使用WIF私钥导入创建ONTID；
* 在CandyBox应用中，ONT ID可以关联各种Candy，这些Candy是以中心化账户系统管理；
* 更多场景......

### 强化用户标志
同时，我们需要让用户对ONT ID更方便管理且更有辨识度，互联网用户将不必记忆自己复杂的WIF私钥或者Keystore , ONT ID将关联用户手机或者和第三方账户体系关联。 用户非常容易记忆和管理。

### 统一应用标准
以上的扩展应用方案，我们仍旧需要纳入ONT ID标准体系，便于用户在跨应用、跨终端使用。 比如，用户在AAPP Store中开通的ONT ID，仍旧可以导入到ONTO或者麦子钱包中去管理其资产和数据。

### 目标
ONT ID快速开通模式应用在H5或嵌入页面式的应用场景中，在这类场景中，用户的特点是无任何区块链背景知识，没有密钥管理经验；同时页面在微信/Facebook等社媒中传播，没有任何私钥管理的基础设施（没有集成CyanoMobile）。

## ONTID综合账户管理接口
注意： 需要添加HMAC认证方案。
管理接口如下：
+ 注册ONT ID
    + [手机注册](#手机注册)
    + [keystore注册](#keystore注册)
+ 登录ONT ID
    + [手机验证码登录](#手机验证码登录)
    + [手机密码登录](#手机密码登录)
+ [导出](#导出)
+ 修改
    + [修改手机号](#修改手机号)
    + [修改密码](#修改密码)
+ [校验密码](#校验密码)
+ [获取验证码](#获取验证码)


### 手机注册
1. [获取验证码](#获取验证码)
2. 提交号码，验证码，密码
3. 返回ontid
```text
url：/api/v1/ontid/register/phone
method：POST
```

请求：
```json
{
	"number":"+86*15821703553",
	"verifyCode": "123456",
	"password":"123456"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    number|   String|  手机号码  |
|    verifyCode|   String|  手机验证码  |
|    password|   String|  设置密码  |

返回：
```json
{
	"action":"register",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### keystore注册
1. [获取验证码](#获取验证码)
2. 提交号码，验证码，keystore，keystore对应的密码
3. 返回ontid（该ontid和keystore的ontid一致）
```text
url：/api/v1/ontid/binding 
method：POST
```

请求：
```json
{
	"phone":"+86*15821703553",
	"verifyCode":"123456",
	"keystore":"keystore",
	"password":"123456"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码  |
|    verifyCode|   String|  手机验证码  |
|    keystore|   String|  keystore  |
|    password|   String|  设置密码  |

返回：
```json
{
	"action":"binding",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### 手机验证码登录
1. [获取验证码](#获取验证码)
2. 提交号码，验证码
3. 返回ontid（该ontid和keystore的ontid一致）
```text
url：/api/v1/ontid/login/phone
method：POST
```

请求：
```json
{
	"phone":"+86*15821703553",
	"verifyCode": "123456"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码  |
|    verifyCode|   String|  手机验证码  |

返回：
```json
{
	"action":"login",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### 手机密码登录
1. 提交号码，密码
2. 返回ontid
```text
url：/api/v1/ontid/login/password
method：POST
```

请求：
```json
{
    "phone":"+86*15821703553",
    "password": "123456"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码  |
|    password|   String|  用户密码  |

返回：
```json
{
    "action":"login",
    "version":"1.0",
    "error":0,
    "desc":"SUCCESS",
    "result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### 导出
1. 提交ontid和密码
2. 返回所需要的结果
```text
导出 keystore
url：/api/v1/ontid/export/keystore 

导出 wif
url：/api/v1/ontid/export/wif 

导出 手机号
url：/api/v1/ontid/export/phone 

method：POST
```

请求：
```json
{
   	"ontid":"did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL",
   	"password":"12345678"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    ontid|   String|  ontid  |
|    password|   String|  ontid密码  |

返回：
```json
{
	"action":"export",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": "请求的对应值"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  keystore请求返回keystore，wif请求返回wif,phone请求返回phone，失败返回""  |

### 修改手机号
1. 新的手机[获取验证码](#获取验证码)
2. 提交新手机号码，验证码，旧手机号码和密码
3. 返回ontid（该ontid和keystore的ontid一致）
```text
url：/api/v1/ontid/edit/phone 
method：POST
```

请求：
```json
{
    "newPhone": "+86*15821703552",
    "verifyCode": "123456",
    "oldPhone":"+86*15821703553",
    "password":"123456"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码  |
|    verifyCode|   String|  手机验证码  |

返回：
```json
{
    "action":"edit",
    "version":"1.0",
    "error":0,
    "desc":"SUCCESS",
    "result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### 修改密码
1. [获取验证码](#获取验证码)
2. 提交号码，验证码，新的密码
3. 返回ontid（该ontid和原来的不一致）
```text
url：/api/v1/ontid/edit/password
method：POST
```

请求：
```json
{
    "phone":"+86*15821703553",
    "verifyCode":"123456",
    "newPassword":"12345678"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码  |
|    verifyCode|   String|  手机验证码  |

返回：
```json
{
    "action":"edit",
    "version":"1.0",
    "error":0,
    "desc":"SUCCESS",
    "result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   String|  成功返回ontid，失败返回""  |

### 校验密码
1. 提交ontid和密码
2. 返回所需要的结果
```text
url：/api/v1/ontid/verify

method：POST
```

请求：
```json
{
   	"ontid":"did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL",
   	"password":"12345678"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    ontid|   String|  ontid  |
|    password|   String|  ontid密码  |

返回：
```json
{
    "action":"verify",
    "version":"1.0",
    "error":0,
    "desc":"SUCCESS",
    "result": true
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   bool| 成功返回true，失败返回false  |

### 获取验证码
```text
url : /api/v1/ontid/getcode/phone
method:POST
```

请求：
```json
{
    "number":"+86*15821703553"
}
```
| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    number|   String|  手机号码  |

返回：
```json
{
    "action":"getVerifyCode",
    "version":"1.0",
    "error":0,
    "desc":"SUCCESS",
    "result": true
}
```

| Field_Name|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    action|   String|  动作标志  |
|    version|   String|  版本号  |
|    error|   int|  错误码  |
|    desc|   String|  成功为SUCCESS，失败为错误描述  |
|    result|   bool|  发送结果（成功，失败）  |
