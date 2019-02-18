## ONTID综合账户管理接口
* 获取验证码
* 注册
* 登录
* 修改手机号或密码
* 导入
* 导出keystore或wif

### 获取验证码
注意： 需要添加HMAC认证方案。

请求：

```json
url：/api/v1/ontid/getcode/phone
method：POST

{
			"number":"+86*15821703553",
}

```

返回：
```json

{
	"action":"getCode",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": true
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    number|   String|  手机号码（带上区号）  |
|    result|   bool|  发送成功  |

### 注册

请求：

```json
url：/api/v1/ontid/register/phone
method：POST

{
			"number":"+86*15821703553",
			"verifyCode": "123456",
			"password":"123456"
}

```

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

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    number|   String|  手机号码（带上区号）  |
|    verifyCode|   String|  验证码  |
|    password|   String|  密码  |
|    result|   String|  ontid  |


### 登录
请求：

* 验证码登录

1. 先获取校验码
2. 验证校验码
```json
url：/api/v1/ontid/login/phone
method：POST

{
			"phone":"+86*15821703553",
			"verifyCode": "123456"
}

```
* 密码登录
```json
url：/api/v1/ontid/login/password
method：POST

{
			"phone":"+86*15821703553",
			"password": "123456"
}
```

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

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|  手机号码（带上区号）  |
|    verifyCode|   String|  验证码  |
|    password|   String|  密码  |
|    result|   String|  ontid  |



### 修改手机号

1. 先获取新手机校验码

2. 请求：

```json
url：/api/v1/ontid/edit/phone 
method：POST

{
			"newPhone": "+86*15821703552",
			"verifyCode": "123456",
			"oldphone":"+86*15821703553",
			"password":"123456",
}


```
返回：
```json

{
	"action":"editPhone", 
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
    "result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    newPhone|   String|   新手机号  |
|    verifyCode|   String|   新手机号验证码  |
|    oldphone|   String|   旧手机号  |
|    password|   String|   密码  |
|    result|   String|   ontid  |
### 修改密码（忘记密码）
1. 先获取手机校验码
2. 修改密码
```
/api/v1/ontid/edit/password

{
			"phone":"+86*15821703553",
			"verifyCode":"123456",
			"newPassword":"12345678",
}
```

返回：
```json

{
	"action":"editPassword",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
    "result": "did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    phone|   String|   手机号  |
|    verifyCode|   String|   手机号验证码  |
|    newPassword|   String|   新密码  |
|    result|   String|   ontid  |


### 托管

1.获取手机验证码
2.请求：
```json
url：/api/v1/ontid/binding 
method：POST

{
		    "phone":"+86*15821703553",
			"verifyCode":"123456",
			"data":"keystore",
			"password":"123456"
			
}

```

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

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    data|   string|     keystore|
|    phone|   String|   手机号  |
|    verifyCode|   String|   手机号验证码  |
|    password|   String|   密码  |
|    result|   String|   ontid  |


### 导出

请求：
```json
url：/api/v1/ontid/export/keystore 
method：POST

{
			"ontid":"did:ont:AcrgWfbSPxMR1BNxtenRCCGpspamMWhLuL"
			"password":"12345678"
}

```

返回：
```json

{
	"action":"export",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": {
	    "keystore"：""
	    "phone":"+86 1231231231"
	}
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    ontid|   string|     ontid|
|    password|   String|   密码  |
|    phone|   String|   手机号  |
|    keystore|   String|   ontid  |


