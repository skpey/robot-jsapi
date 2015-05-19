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
					"recommends":[
						{
							"id":16778,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"国学",
							"icon":"图标URL",
							"is_collected":true,
						},
						{
							"id":16776,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"故事",
							"icon":"图标URL",
							"is_collected":false,
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
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
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":1
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":2
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":3
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":4
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":5
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":false,
							"order":6
						}
				]
			}
1. 我的收藏 `/weixin/jsapi/collections/list.json`
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
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}
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
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}
			

1. 搜索提示 `/weixin/jsapi/vod/search_suggest.json`

	* 方法：POST
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

	* 方法：POST
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
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"duration":"03:12",
							"category_name":"儿歌",
							"icon":"图标URL",
							"is_collected": true
						}
				]
			}

1. 发送到设备 `/weixin/jsapi/vod/send_to_device.json`
	* 方法：POST
	* 参数：
		* media_ids -- 故事儿歌的ID
	* 说明：多个音频时，用半角逗号分隔
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			}

1. 添加到播放列表 `/weixin/jsapi/playlist/add.json`
	* 方法：POST
	* 参数：
		* media_id -- 故事儿歌的ID
	* 返回：
		
			{
				"code":200,
				"message":"OK"
			} 
1. 从播放列表中删除 `/weixin/jsapi/playlist/remove.json`
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
1. 讲故事首页 `/weixin/jsapi/story/index.json`
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
							"name":"童话故事",
							"icon":"图标URL"
						},
						{
							"id":6776,
							"name":"寓言故事",
							"icon":"图标URL"
						}
					],
					"recommends":[
						{
							"id":16778,
							"name":"小兔子",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16776,
							"name":"小兔子不乖",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"category_name":"寓言故事",
							"icon":"图标URL",
						}
					]
				}
			}
			
1. 某个分类下所有的故事列表 `/weixin/jsapi/story/list.json`
	* 方法：GET
	* 参数：category_id -- 分类ID
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16778,
							"name":"小兔子",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16776,
							"name":"小兔子不乖",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"category_name":"寓言故事",
							"icon":"图标URL",
						}
				]
			}  1. 讲故事-搜索提示 `/weixin/jsapi/story/search_suggest.json`

	* 方法：POST
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
1. 讲故事-搜索 `/weixin/jsapi/story/search.json`

	* 方法：POST
	* 参数：keyword -- 已输入关键词
	* 返回：
		
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16778,
							"name":"小兔子",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16776,
							"name":"小兔子不乖",
							"category_name":"童话故事",
							"icon":"图标URL",
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"category_name":"寓言故事",
							"icon":"图标URL",
						}
				]
			}

	
1. 故事文本 `/weixin/jsapi/story/{story_id}.json`
	* 方法：GET
	* 参数：
		* story_id -- 故事文本的ID，放在URL中，比如ID为1234，则请求`story/1234.json`
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":{
					"id":1234,
					"content":"从前有座山，山里有个老和尚，老和尚对小和尚说。。。"
				}
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
1. 推荐的语音包列表 `/weixin/jsapi/audio_pack/recommends.json`
	* 方法：GET
	* 参数：无
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":[
					{
						"id":16779,
						"name":"钢琴系列",
						"cover":"封面图标URL",
					},
					{
						"id":16719,
						"name":"睡前故事",
						"cover":"封面图标URL",
					},
					{
						"id":1279,
						"name":"大灰狼系列",
						"cover":"封面图标URL",
					},
					{
						"id":1339,
						"name":"光头强和熊二",
						"cover":"封面图标URL",
					}
				]
			}

1. 语音包详情 `/weixin/jsapi/audio_pack/{语音包ID}.json`
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

1. 语音包播放情况 `/weixin/jsapi/audio_pack/play_stat.json`
	* 方法：GET
	* 参数：
		* `voice_pack_id` -- 后台将在URL尾部拼接上此参数
	* 返回结果说明：
		* `played` - 已播放多少秒
		* `total` - 共多少秒
		
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
							"played":30,
							"total":100,
							"is_in_playlist":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"played":30,
							"total":100,
							"is_in_playlist":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"played":30,
							"total":100,
							"is_in_playlist":true
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"audio":"音频的URL，一般都mp3",
							"category_name":"儿歌",
							"played":30,
							"total":100,
							"is_in_playlist":true
						}
				]
			}
					
1. 	我的播放列表 `/weixin/jsapi/playlist/list.json`
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

1. 我的故事列表 `/weixin/jsapi/story_voice/list.json`
	* 方法：GET
	* 参数：无
	* 返回：
			
			{
				"code":200,
				"message":"OK",
				"data":[
						{
							"id":16778,
							"name":"小兔子",
							"duration":"00:59",
							"voice":"故事录音URL"
						},
						{
							"id":16776,
							"name":"小兔子不乖",
							"duration":"00:59",
							"voice":"故事录音URL"
						},
						{
							"id":16779,
							"name":"小兔子乖乖",
							"duration":"00:59",
							"voice":"故事录音URL"
						}
				]
			}

1. 从我的故事中删除 `/weixin/jsapi/story_voice/delete.json`
	* 方法：POST
	* 参数
		* story_voice_id -- 故事录音的ID
	* 返回：
			
			{
				"code":200,
				"message":"OK"
			}	 

### 六。设置
1. 更新设备 `/weixin/jsapi/settings/update.json`
	* 方法：POST
	* 参数：
		* (可选参数)baby_nick -- 宝宝昵称
		* (可选参数)baby_birthday -- 宝宝生日
		* (可选参数)device_volume -- 音量大小，整数，取值范围1-3代表低中高
		* (可选参数)device_tone -- 提示音，整数，范围待定

	* 说明：按需要填充参数，可以同时改一个或多个
	* 返回：
			
				{
					"code":200,
					"message":"OK"
				}
			
	
 