### JS API
HOST为约定的主机名

1. 签名 `/weixin/jsapi/signature.json`
	* 方法：GET
	* 参数：无，服务器获取Referer作为参数
	* 返回：
			
			{
				"appid" : "xxx1111",
				"timestamp" : xxx2222,
				"noncestr" : "xxx333",
				"signature" : "xxx4444",
			}
	* 示例
		
			curl --header "Referer: http://127.0.0.1/app.html" http://HOST/weixin/jsapi/signature.json
			
2. 待补充，随时更新