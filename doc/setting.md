设置页面

该api是给 设置页面使用。0是Android，1是 ios

### HTTP 请求

```
GET  /v2/setting/{0|1}/setting.json
```
### 响应体

```
[
	{
	  title: string // 例如活动
	  url: string // 
	},
	{
	  title: string // 标题 例如精品推荐
	  url: string // 点击后的地址
	}
]
```





![](https://github.com/zhangshanhai/readthis-web/blob/master/10%E4%B8%87%E5%8A%A0/%E8%A7%86%E8%A7%89%E7%A8%BF/iPhone%2067%20%E2%80%93%E8%AE%BE%E7%BD%AE.png?raw=true)



