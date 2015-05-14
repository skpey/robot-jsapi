### JS API
* HOST为约定的主机名
* 微信API以用户的OpenID作为认证鉴权

### 一。签名

1. 签名 `/weixin/jsapi/signature.json`
	* 方法：GET
	* 参数：无，服务器获取Referer作为参数
	* 返回：
			
			{
				"appid" : "xxx1111",
				"timestamp" : 1431530352,
				"noncestr" : "xxx333",
				"signature" : "xxx4444"
			}
	* 示例
		
			curl --header "Referer: http://127.0.0.1/app.html" http://HOST/weixin/jsapi/signature.json
		
### 二。群组
1. 群组基本信息 `/weixin/jsapi/group/info.json`
	* 方法：GET
	* 参数：无
	* 说明：用于页面【群成员】
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data": {
					"gid":123456,
					"qrcode_image":"二维码图片URL",
					"my_nick":"我的昵称",
					"is_group_owner":false,
					"members":[
						{"uid":1234,"name":"奶爸","avatar":"头像URL"},
						{"uid":1235,"name":"爷爷","avatar":"头像URL"},
						{"uid":1236,"name":"奶奶","avatar":"头像URL"}
					]
				}
			}
			
1. 退出群组 `/weixin/jsapi/group/quit.json` 	
	* 方法： POST
	* 参数：gid -- 群组ID
	* 返回：
		
			// 非群主退出
			{
				"code":200,
				"message":"你已退出群组"
			}
			
			// 群主退出
			{
				"code":200,
				"message":"群组已解散"
			}
		
2. 把成员踢出群组 `/weixin/jsapi/group/kick.json` 	
	* 方法： POST
	* 参数：
		* gid -- 群组ID
		* uid -- 被踢用户的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}
			
3. 修改昵称 `/weixin/jsapi/user/modify_nick.json` 	
	* 方法： POST
	* 参数：
		* uid -- 用户的ID
		* nick -- 新的昵称
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}
			
### 三。故事点播

4. 点播首页 `/weixin/jsapi/vod/index.json` 	
	* 方法：GET
	* 参数：无
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":{
					"categories":[
						{
							"id":6778,
							"name":"国学",
							"icon":"图标URL"
						},
						{
							"id":6776,
							"name":"故事",
							"icon":"图标URL"
						},
						{
							"id":6779,
							"name":"儿歌",
							"icon":"图标URL"
						}
					],
					"recommend":[
						{
							"id":16778,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"国学",
							"icon":"图标URL"
						},
						{
							"id":16776,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"故事",
							"icon":"图标URL"
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL"
						}
					]
				}
			}
1. 搜索提示 `/weixin/jsapi/vod/search_suggest.json`

	* 方法：GET
	* 参数：keyword -- 已输入关键词
	* 返回：
		
			{
				// TODO:
			}  1. 搜索提示 `/weixin/jsapi/vod/search.json`

	* 方法：GET
	* 参数：keyword -- 已输入关键词
	* 返回：
		
			{
				// TODO:
			}

### 四。讲故事 
2. 待补充，随时更新