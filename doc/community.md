# 社群

社群是用户一起分享文章的地方。

**社群**

* [创建社群](#创建社群)
* [获取社群](#获取社群)
* [更新社群、图片简介](#更新社群)
* [更新社群、设置私密、只读](#更新社群设置)
* [删除社群](#删除社群)
* [获取社群列表](#获取社群列表)


**社群内文章**

* [向社群内添加文章](#向社群内添加文章)
* [获取社群内的文章列表](#获取社群内的文章列表)
* [获取社群内的文章](#获取社群内的文章)
* [删除社群内的文章](#删除社群内的文章)
* [修改社群内文章、通过审核、置顶](#修改社群内文章)

**社群与用户**

* [加入社群](#加入社群)
* [退出社群](#退出社群)
* [查询社群内成员](#查询社群内成员)
* [查询某个社群内成员](#查询某个社群内成员)
* [修改社群内成员、禁言、](#修改社群内成员)

---

## 创建社群

### HTTP 请求

```
POST /v2/community
```

### URL 参数

无

### 请求体

```
{
  name: string // 社群的名称
  description: string // 社群的描述文字
  userId: string{32} // 可选,创建微刊的用户的 id
  visible:boolean //可选, 是否公开;默认 是
  contentVisible:boolean //可选 内容是否公开;默认 是
  mute:boolean //可选 是否只有管理员可发帖;默认 否
  logo:string//可选 
  img:string//可选 
  domain:string//可选
}
```

### 响应头
201 或者其他

### 响应体

```
{
  id: string{32} // 社群的 id
  name: string // 社群的名称
  description: string // 社群的描述文字
  userId: string{32} // 可选,创建社群的用户的 id
  visible:boolean //可选, 是否公开;默认 是
  contentVisible:boolean //可选 内容是否公开;默认 是
  mute:boolean //可选 是否只有管理员可发帖;默认 否
  logo:string//可选 
  img:string//可选 
  domain:string//可选
  createTime: number // 创建社群的时间, Unix 时间戳
  updateTime: number // 更新社群的时间, Unix 时间戳
  userId: string{32} // 创建社群的用户的 id
  membersCount:long //成员个数
  }
```

---



## 获取社群

### HTTP 请求

```
GET /v2/community/:id
```

### URL 参数

参数名            | 值类型      | 描述
---------------- | ---------- | -----------
id               | string{32} | 社区的 id


### 请求体

```

```

### 响应头
200 或者其他

### 响应体

```
community
```

---

## 更新社群

### HTTP 请求

```
PUT /v2/community/:id
```

### URL 参数

参数名            | 值类型      | 描述
---------------- | ---------- | -----------
id               | string{32} | 社区的 id

### 请求体

```
{
  id:long
  description: string // 社群的描述文字
  logo:string//可选 
  img:string//可选 
  domain:string//可选
}
```

### 响应头

200 或者其他

### 响应体

```
community
```

---

## 更新社群设置

### HTTP 请求

```
PATCH /v2/community/:id
```

### URL 参数

参数名            | 值类型      | 描述
---------------- | ---------- | -----------
id               | string{32} | 社区的 id

### 请求体

```
{
 
  id:long,
  visible:boolean,//可选, 是否被搜索，发现;默认 否
  memberReview:boolean//可选, 用户是否先审核后加入;默认 否
  visible:boolean //可选, 是否公开;默认 是
  contentVisible:boolean //可选 内容是否公开;默认 是
  mute:boolean //可选 是否只有管理员可发帖;默认 否
}
```

### 响应头

200 或者其他

### 响应体

```
community 
```

---
## 获取社群列表

### HTTP 请求

```
GET /v2/community
```

### URL 参数

参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
id        | string{32} | 社区的 id
cursor    | string     | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
limit     | number     | 可选, 限制返回的结果数量, 默认为 20
name      |string      |可选 精确查找
keywords  |string      |可选，模糊查找


### 请求体

```

```

### 响应头

200 或者其他

### 响应体

```
[community]
```

---

## 社群内文章

## 向社群内添加文章

### HTTP 请求

```
POST /v2/community/:communityId/summary
```

### URL 参数

参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
id        | string{32} | 社区的 id


### 请求体

```
{
  summaryId:string{32} // 文章的 id
  titleImageUrl:string{32} // 文章的头图地址

  imageUrls:List<Img>//多图模式，多图片
  remark: string//多图模式，简介

}
```

```
img

{
  md5String:string//图片的md5
  url:string//图片的url
}
```

### 响应头

200 或者其他

### 响应体

```
{
  id: string{32} // 社群的 id
  summaryId:string{32} // 文章的 id
  summary: Summary //内容
  titleImageUrl:string{32} // 文章的头图地址

  imageUrls:List<Img>//多图模式，多图片
  remark: string//多图模式，简介
  
  createTime: number // 创建社群的时间, Unix 时间戳
  updateTime: number // 更新社群的时间, Unix 时间戳
  userId: string{32} // 创建社群的用户的 id
}

  
```

```
summary
{
  id: string // 文章的 id
  title: string // 文章标题
  body: string // 文章的正文内容
  summary: string // 文章摘要
  url: string // 文章的原文绝对地址(外部地址，用于显示)
  jumpUrl: string // 文章的跳转绝对地址
  iconUrl: string // 文章的图标绝对地址
  titleImageUrl: string[] // 题图的绝对地址数组, 可能为空
  createTime: number // 文章创建时间, Unix时间戳
  updateTime: number // 文章更新时间, Unix时间戳
  snapshot:boolean // 是否支持快照，支持快照时表示服务器中有body 缓存。如果不支持，客户端需要在 app内置webviwe中打开jumpUrl 地址。
}
  
```

---

## 获取社群内的文章列表

### HTTP 请求

```
GET /v2/community/:communityId/summary
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
id        | string{32} | 微刊的 id
cursor    | string     | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
limit     | number     | 可选, 限制返回的结果数量, 默认为 20


### 请求体

```

```

### 响应头

200 或者其他

### 响应体

```
[communitySummary]
```

---
## 获取社群内的文章

### HTTP 请求

```
GET /v2/community/:communityId/summary/{id}
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
id|long |文章的id

### 请求体

```

```

### 响应头

200 或者其他

### 响应体

```
communitySummary
```

---

## 删除社群内的文章

### HTTP 请求

```
DELETE /v2/community/:communityId/summary/{id}
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
id|long |文章的id

### 请求体

```

```

### 响应头

204 或者其他

### 响应体

```
  
```

---
## 修改社群内文章

### HTTP 请求

```
PATCH /v2/community/:communityId/summary/{id}
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
id|long |文章的id

### 请求体

```
{
  status:int // 1 审核通过，-1 拒绝审核 可选
  pinned:boolean // true 置顶，false 取消置顶 可选
}

```

### 响应头

200 或者其他

### 响应体

```
communitySummary 
```

---
## 社群成员

## 加入社群

### HTTP 请求

```
POST /v2/community/:communityId/user
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id


### 请求体

```
{
  userId:String // 当前用户id
}

```

### 响应头

201 或者其他

### 响应体

```
CommunityMemberVo
{
  id:long// memberId
  communityId;
  userId:String{32}//用户id
  userName:string//
  admin:boolean  //是否是管理员
  owner:boolean//是否是群主
  black:boolean//是否拉黑
  mute:boolean//是否静音
  status:int;//0 未审核；-1 已经踢出去；1 审核通过；-9999 拉黑
  createTime;
  updateTime;
}
  
```

---

## 退出社群

### HTTP 请求

```
DELETE /v2/community/:communityId/user/:memberId
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
memberId|long| memberId

### 请求体

```

```

### 响应头

204 或者其他

### 响应体

```

```

---

## 查询社群内成员

### HTTP 请求

```
GET /v2/community/:communityId/user
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
cursor    | string     | 可选, 作为起始点的 memberId 的 id, 如果此项为空, 后端将默认以最新的 memberId 作为起始点
limit     | number     | 可选, 限制返回的结果数量, 默认为 20


### 请求体

```

```

### 响应头

200 或者其他

### 响应体

```
[CommunityMemberVo]
```

---
## 查询某个社群内成员

### HTTP 请求

```
GET /v2/community/:communityId/user/:memberId
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
memberId    | long     | memberId



### 请求体

```

```

### 响应头

200 或者其他

### 响应体

```
CommunityMemberVo
```

---
## 修改社群内成员

### HTTP 请求

```
PATCH /v2/community/:communityId/user/:memberId
```

### URL 参数


参数名     | 值类型     | 描述
--------- | ---------- | ------------------------------------
communityId| long | 社区的 id
memberId    | long     | memberId



### 请求体

```
{
  admin:boolean  //是否是管理员
  black:boolean//是否拉黑
  mute:boolean//是否静音
  status:int;//-1 已经踢出去；1 审核通过；-9999 拉黑
}

```

### 响应头

200 或者其他

### 响应体

```
CommunityMemberVo
```

---

