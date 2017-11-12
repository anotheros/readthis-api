# Readthis API 文档

 [Readthis](http://100000p.com) 
 [android 端移步此处](https://github.com/zhangshanhai/100000p-android) 
 [ios 端移步到此处](https://github.com/zhangshanhai/100000p-ios)

[墨刀 交互原型](https://pro.modao.cc/app/LBLKgOOullAvgb5V9e8N1hGmWZ4DHHd)

[api文档地址](https://github.com/zhangshanhai/readthis-api)

[功能点](https://github.com/zhangshanhai/readthis-web/blob/master/README.md)

[手绘图](https://github.com/zhangshanhai/readthis-web/blob/master/img/index.md)

# [ui设计图](https://github.com/zhangshanhai/readthis-web/tree/master/10%E4%B8%87%E5%8A%A0)

[产品方向目标](https://github.com/zhangshanhai/readthis-api/blob/master/pm.md)


[lite版本需求说明](https://github.com/zhangshanhai/readthis-api/blob/master/lite.md)

api 根目录 api.100000p.com

注意 该api 支持 http2 。 http2 比http1.1 更强悍。

## API 文档

# 👉👉👉[修改记录日志必看](https://github.com/zhangshanhai/readthis-api/blob/master/changeLog.md)👈👈👈

[注册](https://github.com/zhangshanhai/readthis-api/blob/master/doc/register.md)√

[授权](https://github.com/zhangshanhai/readthis-api/blob/master/doc/authorization.md)√


[时间线](https://github.com/zhangshanhai/readthis-api/blob/master/doc/timelines.md)√

[文章](https://github.com/zhangshanhai/readthis-api/blob/master/doc/articles.md)√


[根据url查文章](https://github.com/zhangshanhai/readthis-api/blob/master/doc/bases.md)√


[用户](https://github.com/zhangshanhai/readthis-api/blob/master/doc/users.md)√


[个性域名](https://github.com/zhangshanhai/readthis-api/blob/master/doc/url-tokens.md)


[微刊](https://github.com/zhangshanhai/readthis-api/blob/master/doc/collections.md)√

[社群](https://github.com/zhangshanhai/readthis-api/blob/master/doc/community.md)√

[标签](https://github.com/zhangshanhai/readthis-api/blob/master/doc/tags.md)√


[远程页面](https://github.com/zhangshanhai/readthis-api/blob/master/doc/remote-pages.md)√

[Android 更新api](https://github.com/zhangshanhai/readthis-api/blob/master/doc/androidUpdate.md)√

[设置页面 api](https://github.com/zhangshanhai/readthis-api/blob/master/doc/setting.md)√

## 设计规范

Readthis 的 API 遵循[现代 RESTful API 设计规范](https://github.com/BlackGlory/modern-restful-api-design-specification).


## api约定

1. 请求list列表时 都需要带上参数，size。
返回时，头部都会返回 count: 个数。

2. 如果查询只要id，则 在原来地址请求的对象下 加 _id 即可。**文档中没有体现**

> 例如 /v2/collections/:collectionId/articles_id  表示查某一微刊下的所有文章的id。

3. 当返回文章数组时候，不包括文章内容body字段。当返回单个文章时，返回body字段。

## 问题汇总。

1.分页问题。

使用游标。取列表最后一个的id，作为下一个请求的cursor参数。

第一次请求 20 条，显示10条，另外10条缓存起来，然后 加载更多的时候，从缓存中取出10条；然后从服务器请求10条 放缓存里。如果返回没有数据，则认为到达底部。这样好处是 体验上感觉很快。

2.登录问题

需要登录才能访问的api，如果没有登录，则返回 401 状态码。

登录需要在header里 写入 Token 。
Linux curl 示意，

```
curl -H "Token: xxxxx" http://xxxxx
```

所有api最好都带上 Token，除了注册登录。

3.返回415 怎么办。 http 头 需要加上

```
Content-type: application/json;charset=UTF-8
```
 
4.错误信息 从返回的 header 里的 code 里取得 错误码，含义如下。

| code         | 中文   | 英文 | 
| ------------ | ----- | ---- |
| 1001         |校验码不能为空 | code is not empty| 
| 1002         |email不能为空 | email is not empty| 
| 1003         |注册失败 | regist is fail| 
| 1004         |token 失效或者不正确| token is illegal| 
| 1005         |密码不正确或者用户不存在|Email does not exist or password is incorrect| 
| 1006         |用户名不可用|username does exist| 
| 2001         |收藏夹名字不能为空|collections name can not be null| 
| 2002         |没有这个收藏夹|this collections does not exist| 
| 2003         |没有这个文章|this article does not exist| 
| 2004         |这个文章已经存在|this article does exist| 
| 2005         |url地址在黑名单中|this article in the blacklist| 
| 2006         |没有在这个收藏夹中找到该文章|this article not in this collections| 
| 2007         |没有在这个标签|tag does not exist| 
| 2008         |收藏夹名字已经存在|collections name does  exist| 
| 2009         |收藏夹id不能为空|collectionsid can not be null| 
| 3001         |未找到该用户|this user does not exist| 
| 4001         |社群名字不能为空|community name can not be null| 
| 4006         |没有在这个社群中找到该文章|this article not in this community | 
| 4008         |社群名字已经存在|community name does  exist| 
| 4009         |社群id不能为空| community can not be null|
| 9001         |参数校验不合法|Illegal parameter calibration |
| 9401         |没有登录|not login|
| 9403         |没有权限|not auth|
| 9404         |未找到|not fond|
| 9507         |服务器存储失败|Insufficient Storage|
| 9999         |其他系统错误|system error| 



## 讨论

[![](http://pub.idqqimg.com/wpa/images/group.png "用户交流群")](http://shang.qq.com/wpa/qunwpa?idkey=bc60b852e963704404153f225800257ab64dc5727cab6e777166f7d76046ba7a)

群号:238068472
