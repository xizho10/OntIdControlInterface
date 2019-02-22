# App唤醒Cyano App进行支付

此文档为原生DApp唤醒Cyano App进行支付的流程设计和接口定义。

## 流程设计

数据内容仿造[Cyano二维码](https://github.com/ontio-cyano/CEPs/blob/master/CEPS/CEP1.mediawiki#Invoke_a_Smart_Contract-2)
```
{
	"action": "invoke",  
	"version": "v1.0.0",
	"id": "10ba038e-48da-487b-96e8-8d3b99b6d18a",
	"params": {
		"login": true,
		"qrcodeUrl": "http://101.132.193.149:4027/qrcode/AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ",
		"message": "will pay 1 ONT in this transaction",
		"callback": "http://101.132.193.149:4027/invoke/callback",
	}
}
```
1. 将交易内容放在qrcodeUrl链接中，参考[Cyano二维码](https://github.com/ontio-cyano/CEPs/blob/master/CEPS/CEP1.mediawiki#Invoke_a_Smart_Contract-2)
2. 判断本地是否安装Cyano App，例如:
```
 public static boolean checkInstallCynoApp(Context context) {
        final PackageManager packageManager = context.getPackageManager();// 获取packagemanager
        List<PackageInfo> pinfo = packageManager.getInstalledPackages(0);// 获取所有已安装程序的包信息
        if (pinfo != null) {
            for (int i = 0; i < pinfo.size(); i++) {
                String pn = pinfo.get(i).packageName.toLowerCase(Locale.ENGLISH);
                if (pn.equals("com.github.ont.cyanowallet")) {
                    return true;
                }
            }
        }
        return false;
    }
```

Cyano下载地址为
```
http://101.132.193.149/files/app-debug.apk
```
2. 拼接传递内容，启动交易,例如：
```
    String data = "{\"action\":\"invoke\",\"version\":\"v1.0.0\",\"id\":\"10ba038e-48da-487b-96e8-8d3b99b6d18a\",\"params\":{\"login\":true,\"qrcodeUrl\":\"http://101.132.193.149:4027/qrcode/AUr5QUfeBADq6BMY6Tp5yuMsUNGpsD7nLZ\",\"message\":\"will pay 1 ONT in this transaction\",\"callback\":\"http://101.132.193.149:4027/invoke/callback\"}";

    Intent intent = new Intent("android.intent.action.VIEW");
    intent.setData(Uri.parse("cyano://com.github.cyano?data=" + data ));
    intent.addCategory("android.intent.category.DEFAULT");
    startActivity(intent);
```

