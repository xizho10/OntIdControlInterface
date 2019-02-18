## ONTID综合账户管理接口

* 注册
* 登录
* 修改手机号或密码
* 导入
* 导出keystore或wif

### 注册

注意： 需要添加HMAC认证方案。

请求：

```json
url：/api/v1/ontid/registry
method：POST

{
	"action":"registry",
	"version":"1.0",
	"params": {
			"phone":"15821703553",
			"verifyCode": 123456,
			"password":"123456"
	}
}

```

返回：
```json

{
	"action":"registry",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": true
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    result|   bool|   true 或false  |


### 登录
请求：

```json
url：/api/v1/ontid/login
method：POST

{
	"action":"login",
	"version":"1.0",
	"params": {
			"phone":"15821703553",
			"verifyCode": 123456
	}
}

```

返回：
```json

{
	"action":"login",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": true
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    result|   bool|   true 或false  |



### 修改手机号或密码

请求：

```json
url：/api/v1/ontid/edit/phone 或 /api/v1/ontid/edit/password
method：POST

{
	"action":"editPhone", 
	"version":"1.0",
	"params": {
			"phone":"15821703553",
			"newPhone": "15821703552",
			"password":"123456"
	}
}

或

{
	"action":"editPassword", 
	"version":"1.0",
	"params": {
			"phone":"15821703553",
			"oldPassword": "123456",
			"newPassword":"12345678",
			"comfirmPassword":"12345678"
	}
}
```

返回：
```json

{
	"action":"editPhone", // or editPassword
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": true
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    result|   bool|   true 或false  |


### 导入

请求：
```json
url：/api/v1/ontid/import 
method：POST

{
	"action":"import ", 
	"version":"1.0",
	"params": {
			"type":"keystore" //or wif
			"data":"......"
	}
}

```

返回：
```json

{
	"action":"import",
	"version":"1.0",
	"error":0,
	"desc":"SUCCESS",
	"result": true
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    keystore|   string|     |


### 导出

请求：
```json
url：/api/v1/ontid/export/keystore 或  /api/v1/ontid/export/wif
method：POST

{
	"action":"export", 
	"version":"1.0",
	"params": {
			"phone":"15821703553"
			"password":"12345678"
	}
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
        "keystore": "......"  // 或 wif
    }
}
```

| RequestField|     Type |   Description   | 
| :--------------: | :--------:| :------: |
|    keystore|   string|     |


