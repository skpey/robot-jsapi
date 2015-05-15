### JS API
* HOST为约定的主机名
* 微信API以用户的OpenID作为认证鉴权
* 返回值中的code为200调用成功，其他值失败，message可以参考错误原因

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
		
1. 把成员踢出群组 `/weixin/jsapi/group/kick.json`
	* 方法： POST
	* 参数：
		* gid -- 群组ID
		* uid -- 被踢用户的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}
			
1. 修改昵称 `/weixin/jsapi/user/modify_nick.json` 	
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

1. 点播首页 `/weixin/jsapi/vod/index.json` 	
	* 方法：GET
	* 参数：无
	* 返回字段说明： is_collected -- 是否已收藏
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
							"icon":"图标URL",
							"is_collected":true,
						},
						{
							"id":16776,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"故事",
							"icon":"图标URL",
							"is_collected":false,
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
						}
					]
				}
			}
			
	
1. 排行榜 `/weixin/jsapi/vod/ranklist.json`
	* 方法：GET
	* 参数：
		* (可选参数)limit -- 获取排名前几，默认前10
	* 返回字段说明：
		* order -- 排名 
	* 返回： 			
			
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":1
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":2
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":3
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":4
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":5
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":6
						}
				]
			}
1. 我的收藏 `/weixin/jsapi/vod/my_collections.json`
	* 方法：GET
	* 参数：无
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}
1. TODO: 点播的分类列表 `/weixin/jsapi/vod/categories.json`
1. 获取某个分类下点播列表 `/weixin/jsapi/vod/list.json` 	
	* 方法：GET
	* 参数：category_id -- 分类ID
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}
			

1. 搜索提示 `/weixin/jsapi/vod/search_suggest.json`

	* 方法：GET
	* 参数：keyword -- 已输入关键词
	* 返回：
		
			{
				"code":200,
				"message":"OK",
				"data":[
					{"name":"兔子去"},
					{"name":"芭比去哪儿"},
					{"name":"芭比"},
					{"name":"芭比去"}
				]
			}  
1. 搜索 `/weixin/jsapi/vod/search.json`

	* 方法：GET
	* 参数：keyword -- 已输入关键词
	* 返回：
		
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}


1. 添加到故事机 `/weixin/jsapi/playlist/add.json`
	* 方法：POST
	* 参数：
		* media_id -- 故事儿歌的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}
1. 加入到我的收藏 `/weixin/jsapi/collections/add.json`
	* 方法：POST
	* 参数：
		* media_id -- 故事儿歌的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}
1. 从我的收藏中删除 `/weixin/jsapi/collections/remove.json`
	* 方法：POST
	* 参数：
		* media_id -- 故事儿歌的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}

### 四。讲故事
1. TODO: 讲故事首页 `/weixin/jsapi/story/index.json`
1. TODO: 故事文本的分类列表 `/weixin/jsapi/story/categories.json`
1. TODO: 某个分类下所有的故事文本列表 `/weixin/jsapi/story/list.json`
1. 故事文本 `/weixin/jsapi/story/{story_id}.json`
	* 方法：GET
	* 参数：
		* story_id -- 故事文本的ID，放在URL中，比如ID为1234，则请求`story/1234.json`
	* 返回：
			
			{
				//TODO:
			} 
			
1. 保存已上传到微信服务器的录音文件 `/weixin/jsapi/story/save_voice.json`
	* 方法：POST
	* 参数：
		* story_id -- 故事文本的ID  
		* voice_id -- 上传完微信后得到的serverId（服务器返回音频的服务器端ID）
	* 返回：
			
			{
				"code":200,
				"message":"OK"
			}

### 五。网络故事机
1. TODO:

### 六。XX设置
1. TODO:
 