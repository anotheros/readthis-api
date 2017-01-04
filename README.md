# readthis 接口协议说明



---

## 目录


* [注册](#reg)
* [摘要](#summary)
   * [查询摘要](#selectSummary)
   * [修改摘要](#updateSummary)
* [用户](#user)
* [收藏夹](#collections)
    * [关注收藏夹](#collectionsfollow)
* [喜欢](#like)
* [已读](#readed)
* [稍后阅读](#readLader)
* [推荐给某人某篇文章](#recommendSomeone)
* [评论](#comment)
* [可能喜欢](#maybelike)
   * [上推](#upPushbelike)
   * [下拉](#pullDownbelike)
* [一系列 查询如下](#selectOther)
* [短地址](#shoturl)
* [通知](#notice)
* [好友关系](#friends)
* [查询某一用户](#users)
* [标签](#tag)
* [打分](#score)
* [冒烟测试](#test)



---

<div id="reg"></div>
##注册  
###检测用户名是否存在 

地址|方法|参数|返回值
---|---|---|---
{domain}/2/checkUserName/{userName}|post||存在{"message":"true"}
||||不存在{"message":"false"}





###检测email是否可用

地址|方法|参数|返回值
---|---|---|---
{domain}/2/checkEmail/|post|admin@admin.com|{"message":"true"}
||||{"message":"false"}


###发送注册验证邮件

地址|方法|参数|返回值
---|---|---|---
{domain}/2/sendRegEmail/|post|admin@admin.com|{"message":"true"}
||||{"message":"false"}

###注册

地址|方法|参数|返回值
---|---|---|---
{domain}/2/regist/sadfnmvlmasjfajflsmlsdjil|post|{"userName":"name","email":"admin@admin.com",//该email不会被后台使用，会使用验证时的邮箱"password":"adsfaasdf"}|:404 {"message":"code不能为空"}
||||200 {"message":"code已经过期"}
||||406 {"message":"json格式不正确"}
||||200 {"message":"ok"}



### 登录

地址|方法|参数|返回值
---|---|---|---
{domain}/2/dologin|post|{"email":"admin@admin.com","password":"admin"}| '''登录成功，会在http头里返回Token 值。其他需要登录的操作，需要带着http头去请求。'''


---

<div id="summary"></div>
## 摘要

<div id="selectSummary"></div>
###**查询摘要**

###查询全站 摘要和标签

地址|方法|参数|返回值
---|---|---|---
http://readthis.sinaapp.com/2/global/summary/{from}/{to}/{timestamp}|get|timestamp 为分页参数，避免时间性刷新过快，导致重复数据出现在列表里|





###根据原文urlmd5 查询摘要###

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/url/{urlmd5}|get|urlmd5|

###查询不带标签的摘要 ###
地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/summary|get|summaryid|



###根据文章id查相关摘要和标签 ###

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}|get||

###增加url，标题，摘要，标签###

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary|POST|<code>{"summary":{"url":"http://zhangziyou.sinaapp.com","title":"子游博客","abstracts":"这是一个摘要","media":"超媒体链接，比如图片"},"tag":[{"tagName":"uuid"},{"tagName":"标签1"}]}</code>||

###**修改标摘要**

<div id="updateSummay"></div>
###修改标题，摘要

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/summary|PUT|<code>{"summaryId":"uuid""link":"http:zhangziyou.sinaapp.com",//此次，link在后台会被无视"title":"子游博客",//js可以异步的取到"abstracts":"这是一个摘要","media":"超媒体链接，比如图片"}</code>|成功返回200，{message:true}
|||| 409 {massage:"正在被其他用户修改"}	
|||| 423  {massage:"，已经被锁定"}




###修改摘要和标签

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}|PUT|<code>{"summary":{"url":"http://zhangziyou.sinaapp.com","title":"子游博客","abstracts":"这是一个摘要","media":"超媒体链接，比如图片"},[{"tagName":"uuid"},{"tagName":"标签1"}]}</code>|成功返回200，{massage:true}
||||Status: 409 ,{massage:"正在被其他用户修改"}
||||Status: 423, {massage:"，已经被锁定"}








###只修改标签

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/tag|PUT|<code>[{"tagName":"uuid"},{"tagName":"标签1"}]</code>|成功返回200，{"massage":"true"}
||||Status: 423,{"massage":，"已经被锁定"}


---
###检查链接是否存在

地址|方法|参数|返回值
---|---|---|---
{domain} /2/checkLink/md5(www.baidu.com)|get|www.baidu.com 的md5|{"message":"true"}


---
###请求修改摘要api
修改提交摘要的时候，需要向服务器申请修改。理由，不能同时多人编辑。

地址|方法|参数|返回值
---|---|---|---
{domain} /2/summary/{summaryId}/edit|POST||200,{"message":"true"}
|||| 409,{"massage":"正在被其他用户修改"}
||||423,{massage:"已经被锁定"}




---
###根据id 只查询文章的   此处为 原网站镜像，当然格式化后的

地址|方法|参数|返回值
---|---|---|---
/{domain}/2/article/{summaryid}/|get|summaryid|


---
<div id="user"></div>
##用户

###检测 user 的uri是否存在
 说明，在本站的个性域名。只能改一次且不能如别人重复

地址|方法|参数|返回值
---|---|---|---
{domain}/2/useruri|GET||存在：{"message":"true"}
||||不存在：{"message":"false"}




###检测 uri是否存在

地址|方法|参数|返回值
---|---|---|---
{domain}/2/useruri/{uri}|POST|{uri}|存在：{"message":"uri已经存在"}
||||不存在：{"message":"uri不存在"}

###修改user 的uri

地址|方法|参数|返回值
---|---|---|---
{domain}/2/useruri|PUT|{“uri”:”zhang”}|200,成功：{"message":"修改成功"}
||||403,失败：{"message":"禁止修改"}


---
##收藏夹
<div id="collections"></div>
###创建收藏夹

地址|方法|参数|返回值
---|---|---|---
{domain}/2/collections|POST|todo|201,成功：{"message":"true"}
||||200,失败：{"message":"false"}


###查询收藏夹

地址|方法|参数|返回值
---|---|---|---
{domain}/2/collections/{collectionsId}|get||todo

###删除收藏夹

地址|方法|参数|返回值
---|---|---|---
{domain}/2/collections/{collectionsId}|DELETE||成功：{"message":"true"}
||||200,失败：{"message":"false"}

###修改收藏夹

地址|方法|参数|返回值
---|---|---|---
/collections/{collectionsId}|put||200,406，201


---
<div id="collectionsfollow"></div>
##关注收藏夹


地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/collections/{collectionsId}/{visible} |POST|visible是否公开关注|201,成功：{"message":"true"}
||||200,失败：{"message":"false"}

##取消关注收藏夹


地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/collections/{collectionsId} |delete||201,成功：{"message":"true"}
||||200,失败：{"message":"false"}


##是否关注收藏夹

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/collections/{collectionsId} |get||{"message":"true"}
||||{"message":"false"}

##是否关注收藏夹

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/collections/{collectionsId} |get||{"message":"true"}
||||{"message":"false"}

##查询关注的人


地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/collections/{collectionsId}/fans |get||todo


###收藏到某收藏夹


地址|方法|参数|返回值
---|---|---|---
{domain}/2/collection/{collectionsId}/{summaryid}|post||201,200


###取消收藏

地址|方法|参数|返回值
---|---|---|---
{domain}/2/collection/{collectionsId}/{summaryid}|DELETE|204 成功
||||200,失败：{"message":"false"}

###判断某文章是否在收藏列表

地址|方法|参数|返回值
---|---|---|---
{domain}/2/collection/{collectionsId}/{summaryid}|GET||不在：{"message":"false"}
||||存在：{"message":"true"}


---
<div id="like"></div>
##喜欢 说明：点赞或者叫+1
###喜欢

地址|方法|参数|返回值
---|---|---|---
{domain}/2/liked/{summaryId}|POST|{summaryId}|成功：{"message":"true"}
||||失败：{"message":"false"}

###判断是否已经喜欢###
地址|方法|参数|返回值
---|---|---|---
{domain}/2/liked/{summaryId}|GET||成功：{"message":"true"}
||||失败：{"message":"false"}

###取消喜欢###
地址|方法|参数|返回值
---|---|---|---
{domain}/2/liked/{summaryId}|DELETE||成功：{"message":"true"}
||||失败：{"message":"false"}

<div id="dislike"></div>
###不喜欢某文章###
说明：因为系统可能推荐给你不喜欢的东西，所以从节目删除。存数据库，以后不在推荐，而且这是推荐系统的一个指标

地址|方法|参数|返回值
---|---|---|---
{domain}/2/dislike/{summaryId}|POST||成功：{"message":"true"}
||||失败：{"message":"false"}


###判断是否是不喜欢###
地址|方法|参数|返回值
---|---|---|---
{domain}/2/dislike/{summaryId}|GET||成功：{"message":"true"},失败：{"message":"false"}



###取消不喜欢###
地址|方法|参数|返回值
---|---|---|---
{domain}/2/dislike/{summaryId}|DELETE||成功：{"message":"true"}
||||失败：{"message":"false"}


---
<div id="readed"></div>
##已读##
###标记为已读###
 说明：在原网站已经读过了。所以标记一下。同样是 一个推荐的指标  注意，用户通过本站调整到原网站时，这个表也会插入数据
 
地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/haveread/{summaryId}|POST||成功：{"message":"true"}
||||失败：{"message":"false"}

###判断是否是已读###

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/haveread/{summaryId}|GET||不是：{"message":"false"}
||||是：{"message":"true"}

###标记为未读###

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/haveread/{summaryId}|DELETE||204 成功：{"message":"true"}
||||失败：{"message":"false"}


---

##阅读操作
<div id="readLader"></div>
###稍后阅读##

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/later/{summaryId}|POST||成功：{"message":"true"}
||||失败：{"message":"false"}

###判断是否是稍后阅读

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/later/{summaryId}|GET||不是：{"message":"false"}
||||是：{"message":"true"}

###取消稍后阅读

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/later/{summaryId}|DELETE||成功：{"message":"true"}
||||失败：{"message":"false"}


---
##推荐给某人某篇文章

<div id="recommendSomeone"></div>

地址|方法|参数|返回值
---|---|---|--- 
{domain} /2/recommend/{summaryid}/{userid}|POST||成功：{"message":"true"}
||||失败：{"message":"false"}
||||403{"massage":"userid不存在或者不是好友"}"



---
##评论
###评论+1

<div id="comment"></div>

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/plus/Comment/{Commentid}|POST||成功：{"message":"true"}
||||失败：{"message":"false"}


---
###添加一条评论
 注意：articleId 和summaryId 是一个东西 如果不一致，后台会返回错误信息

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/comments/{summaryid}|POST|{"articleId":"文章摘要的uuid","users":[{"id":"asd"},{"id":"asd2"}],"comment":"评论内容"} json说明，users 是 被at的人的集合|成功：201
||||错误：200


---
###回复一条评论

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/recomments/{commentsId}|post|{"parentId":"uuid","user":{"id":"asd"},"articleId":"文章摘要的uuid","users":[{"id":"asd"},{"id":"asd2"}],"comment":"评论内容"} 注意，这里的commentsId 和 parentId 一致|返回201


---
###根据评论id查相关子评论

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/childrenComments/{commentid}/{from}/{to}|get||



---
<div id="maybelike"></div>
##查询可能喜欢的

get
### 可能喜欢的摘要


地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/maybelike/summary/{10}|get||返回最新10条或者n条 只返回摘要

###摘要和标签 

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/maybelike/summaryAndTag/{10}|get||返回最新10条或者n条 摘要和标签


###上推
<div id="upPushbelike"></div>

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/upPushbelike/summaryAndTag/{pageTime}|get||上推查询可能喜欢的10条摘要和标签  不足时 补充历史浏览（pageTime 是一个long时间戳，该接口返回 比这个时间戳小的，最近的10条，可用于上推加载）

###下拉
<div id="pullDownbelike"></div>

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/pullDownbelike/summaryAndTag/{pageTime}|get||下拉查询可能喜欢的10条摘要和标签  不足时 补充历史浏览（pageTime 是一个long时间戳，该接口返回 比这个时间戳大的，最近的10条，可用于下拉刷新和首次加载）

## 一系列 查询如下
<div id="selectOther"></div>

liked  | dislike | collection | commented | browse | haveread 

###返回摘要

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/summary/{1}/{10}|get|{operate} 为liked，dislike，collection，commented , browse , haveread |返回1到10条 摘要

###返回摘要和标签

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/summaryandtag/{from}/{to}|get|同上|

###只返回id

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/ids/{from}/{to}|get|同上|正确结果 200 返回值略
||||404 {"message":"没有数据"}
||||406 {"message":"参数不正确"}
||||500 {"message":" ****"}




### 根据标签id 或者标签名字查询
tagid/tagname

<div id="tagname"></div>

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/summary/{tag}/{1}/{10}|get|{operate} 为tagid，tag 其中之一 ；tag 为tagid或者tagname支持汉字。|返回1到10条 摘要

###返回摘要和标签

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/summaryandtag/{tag}/{from}/{to}|get|{operate} 为tagid，tag 其中之一 ；tag 为tagid或者tagname支持汉字。|返回1到10条 摘要和标签

###只返回id

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/{operate}/ids/{tag}/{from}/{to}|get|{operate} 为tagid，tag 其中之一 ；tag 为tagid或者tagname支持汉字。|正确结果返回1到10条id ，200 返回值略
||||404 {"message":"没有数据"}
||||406 {"message":"参数不正确"}
||||500 {"message":" ****"}


---
<div id="shoturl"></div>
##短地址

###根据短地址换原地址
即 点击链接调整到源地址


地址|方法|参数|返回值
---|---|---|---
{domain}/2/j/{uri}|get||:302 Location http://google.com
||||404
||||500

###查看某文章的阅读次数 
 
地址|方法|参数|返回值
---|---|---|---
{domain}/2/readtimes/{summaryid}|get||200
||||404
||||500
 

 


###根据id查询 uri（本站跳转前地址），url（跳转后地址，用于显示）


地址|方法|参数|返回值
---|---|---|---
{domain}/2/uri/{summaryid}|get||200{summaryid:”uudi”,url:”zhangziyou.sinaapp.com”;uri:”http://127.0.0.1/ziyoureader/j/1234qwe”}
 


### 根据url（原网站地址的md5）查询 id（数据库主键），uri（本站跳转前短地址），url（跳转后地址，用于显示）


地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/id/{url}|get||{summaryid:”uudi”,url:”zhangziyou.sinaapp.com”;uri:”http://127.0.0.1/ziyoureader/j/1234qwe”}
 

---

<div id="notice"></div>
##通知的

###at 我的评论

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/atme/comments/{form}/{to}|get||404
||||406
||||500
||||200

###得到未读at信息数量  unread 为未读，read 为全部

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/atme/sum/{read}|get||200
||||500
||||406

###得到私信数量  unread 为未读，read 为全部

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/message/sum/{read}|get||

### 查询私信

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/message/{form:[\\d]+}/{to}|get||


---
<div id="friends"></div>
##好友关系
###发送消息给某人

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/message/user/{touserid}|post|“消息主体”|






###查询关注我的人  没有from to 则查全部

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/fans/{from}/{to}|get||:200
||||404
||||406
||||500





###查询关注我的人的总数

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/sum/fans|get||返回数据 有多少粉丝 返回相应个数


### 判断是否是我的粉丝


地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/fans/{userid}|get||{message:"true"}
||||{message:"false"}
 
###删除某粉丝

地址|方法|参数|返回值
---|---|---|--- 
{domain}/2/fans/{userid}|delete||204 {message:"true"}
||||{message:"false"}
 


###查询我关注的人

地址|方法|参数|返回值
---|---|---|---
{domain}/2/follow/{from}/{to}|get||

###查询关注我的人的总数

地址|方法|参数|返回值
---|---|---|---
{domain}/2/sum/follow|get||

###判断是否关注此人

地址|方法|参数|返回值
---|---|---|---
{domain}/2/follow/{userid}|get||

###取消关注某人

地址|方法|参数|返回值
---|---|---|---
{domain}/2/follow/{userid}|delete||



跟fan区别不大

###关注某人


地址|方法|参数|返回值
---|---|---|---
{domain}/2/follow/{userid}|post||204 
||||200 {"message":"失败"}




---
<div id="users"></div>
##某一用户
##查询某一用户属性

地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/info/{from}/{to}|get||
##某一用户关注的标签


地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/tag/{from}/{to}|get||

##某一用户关注的创建收藏夹



地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/creatcollections/{from}/{to}|get||

##某一用户关注的创建收藏夹



地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/collections/{from}/{to}|get||
##某一用户关注的人

地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/follow/{from}/{to}|get||
##某一用户关注的粉丝

地址|方法|参数|返回值
---|---|---|---
{domain}/2/users/{userid}/fans/{from}/{to}|get||
---
<div id="tag"></div>
##标签
###查询某一标签的详细信息

地址|方法|参数|返回值
---|---|---|---
{domain}/2/tag/{tagid}|get|||

###通过名字查询某一标签的详细信息
 tagName 的N大写
 
 地址|方法|参数|返回值
---|---|---|---
{domain}/2/tagName/{tagName}|get||


###查询所有标签

地址|方法|参数|返回值
---|---|---|---
{domain}/2/tag/{from}/{to}|get||404
||||406
||||500
||||200


###返回标签总数

地址|方法|参数|返回值
---|---|---|---
{domain}/2/sum/tag|get||


###查询我关注的所有标签

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/tag/{from}/{to}|get||



###返回我关注的标签总数

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/sum/tag|get||

###关注某一标签

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/tag/{tagid}|post||201 {message:"成功"}
||||200 {message:"失败"}

###取消关注某一标签

delete

地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/tag/{tagid}|delete||200 {message:"成功"}

###判断是否关注某一标签


地址|方法|参数|返回值
---|---|---|---
{domain}/2/user/tag/{tagid}|get||200 


---
<div id="score"></div>
##打分

###给文章评分 包含修改(如果曾经评分过，则是修改评分)


地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/score/{score}|post||{"message":"true"}
||||{"message":"false"}


###查询我的评分

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/score/|get||


###查询平均分

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/score/avg/|get||4



###查询评分总人数

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/score/sum|get||10

###查询分布 不支持

地址|方法|参数|返回值
---|---|---|---
{domain}/2/summary/{summaryid}/score/distribution|get||500
||||404
||||200


---
<div id="test"></div>
##冒烟测试 api

地址|方法|参数|返回值
---|---|---|---
{domain}/2/help/test|||200{"冒烟测试"："true"}
|||数据库挂了 返回 500 



返回其他状态码 5xx不是程序返回的，证明程序也挂了。

