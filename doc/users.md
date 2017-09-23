# 用户

用户是网站的基本成员.
**用户**
* [获取用户](#获取用户)

**粉丝**
* [获取用户粉丝](#获取用户粉丝)
* [删除用户粉丝](#删除用户粉丝)
* [获取用户的粉丝列表](#获取用户的粉丝列表)

**偶像**
* [添加偶像](#添加偶像)
* [获取偶像](#获取偶像)
* [删除偶像](#删除偶像)
* [获取偶像列表](#获取偶像列表)

**微刊**
* [关注微刊](#关注微刊)
* [获取用户创建的微刊](#获取用户创建的微刊)
* [获取用户关注的微刊](#获取用户关注的微刊)
* [获取用户关注的微刊列表](#获取用户关注的微刊列表)
* [取消关注微刊](#取消关注微刊)

**标签**
* [关注标签](#关注标签)
* [获取关注的标签](#获取关注的标签)
* [获取关注的标签列表](#获取关注的标签列表)
* [取消关注标签](#取消关注标签)



## 获取用户

### HTTP 请求

```
GET /v2/users/:id
```

### URL 参数

参数名    | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

无

### 响应体

```
{
  id: string // 用户的id
  nickname: string // 昵称, 默认为 id, 可修改一次
  urlToken: string // 个性域名, 默认为 id, 可修改一次
  defaultCollectionsId:string  默认收藏夹id
  createTime: number // 注册时间, Unix 时间戳
  idolCount: number // 正在关注数量
  fansCount: number // 粉丝数量
  collectionsCount: number // 微刊数量
  followCollectionsCount: number // 关注的微刊数量
  followTagsCount: number // 关注的标签数量
}
```

---


## 获取用户粉丝

### HTTP 请求

```
GET  /v2/users/:userId/fans/:fansId
HEAD /v2/users/:userId/fans/:fansId
```

### URL 参数

参数名     | 值类型     | 描述
---------- | ---------- | -------------------------------------------------------
userId     | string{32} | 用户的 id
fansId     | string     | 粉丝的用户id

### 请求体

无

### 响应体

如果存在, 302 跳转至 `/users/:fansId`

---

## 删除用户粉丝

### HTTP 请求

```
DELETE  /v2/users/:userId/fans/:fansId
```

### URL 参数

参数名     | 值类型     | 描述
---------- | ---------- | -------------------------------------------------------
userId     | string{32} | 用户的 id
fansId     | string     | 粉丝的用户id

### 请求体

无

### 响应体



---

## 获取用户的粉丝列表

### HTTP 请求

```
GET /v2/users/:id/fans
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id


### 请求体

无

### 响应头

```
count:100
```
### 响应体

通常情况下返回:

```
[users]
```


---

## 添加偶像

### HTTP 请求

```
POST /v2/users/:id/idol
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | --------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
id:string， // 偶像id
visible：boolean// 是否可见
}
```

### 响应体

无

---

## 获取偶像

### HTTP 请求

```
GET  /v2/users/:userId/idol/:idolUserId
HEAD /v2/users/:userId/idol/:idolUserId
```

### URL 参数

参数       | 值类型     | 描述
---------- | ---------- | ----------------------
userId     | string{32} | 用户的 id
idolUserId |            | 需要查询的正在粉丝 id

### 请求体

无

### 响应体

如果存在, 302 跳转至 `/users/:userId`

---

## 删除偶像

### HTTP 请求

```
DELETE /v2/users/:userId/idol/:idolUserId

```

### URL 参数

参数       | 值类型     | 描述
---------- | ---------- | ----------------------
userId     | string{32} | 用户的 id
idolUserId |            | 需要查询的正在粉丝 id

### 请求体

无

### 响应体



---

## 获取偶像列表

### HTTP 请求

```
GET /v2/users/:id/idol
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id


### 请求体

无

### 响应头

```
count:100
```

### 响应体

通常情况下返回:

```
[users]
```

## 关注微刊

### HTTP 请求

```
POST /v2/users/:id/followingCollections
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  id: string // 微刊的 id
  visible: boolen// 是否可见，非悄悄关注
  special:int // 特别关注。置顶。权重
}
```

### 响应体

无

---

## 获取用户创建的微刊

### HTTP 请求

```
GET /v2/users/:id/collections
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | ---------------------------
id        | string{32} | 用户的 id


### 请求体

无

### 响应头

```
count:100
```

### 响应体

通常情况下返回:

```
[collections]
```



---

## 获取用户关注的微刊

### HTTP 请求

```
GET  /v2/users/:userId/followingCollections/:collectionId
HEAD /v2/users/:userId/followingCollections/:collectionId
```

### URL 参数

参数名       | 值类型     | 描述
------------ | ---------- |---------------------
userId       | string{32} | 用户的 id
collectionId | string     | 微刊的 id



### 请求体

无

### 响应体

如果该用户关注了此微刊, 302 跳转到 `/v2/collections/:collectionId`

---

## 获取用户关注的微刊列表

### HTTP 请求

```
GET /v2/users/:id/followingCollections
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- |------------------------------
id        | string{32} | 用户的 id
special   |boolean	   | 是否只要特殊关注，true 返回特殊关注；false返回 全部，按 特殊关注权重倒叙。默认false

### 请求体

无

### 响应头

```
count:100
```
### 响应体

通常情况下返回:

```
[collections]
```



---

## 取消关注微刊

### HTTP 请求

```
DELETE /v2/users/:userId/followingCollections/:collectionId
```

### URL 参数

参数名       | 值类型     | 描述
------------ | ---------- | ----------------------
userId       | string{32} | 用户的 id
collectionId | string     | 微刊的 id

### 请求体

无

### 响应体

无

---

## 关注标签

### HTTP 请求

```
POST /v2/users/:id/tags
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  id: string // tag的 id
  visible: boolen// 是否可见，非悄悄关注
  special:int // 特别关注。置顶。权重。权重高，查询我关注的标签时，该标签就越靠前。为0 则 不是特别关注。
}
```

### 响应体

无


### HTTP 请求

```
POST /v2/users/:id/tagName
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  tagName: string // 标签名字
  visible: boolen// 是否可见，非悄悄关注
  special:int // 特别关注。置顶。权重
}
```

### 响应体

无

---

## 获取关注的标签

### HTTP 请求

```
GET  /v2/users/:userId/tags/:tagId
HEAD /v2/users/:userId/tags/:tagId
```

### URL 参数

参数名   | 值类型     | 描述
-------- | ---------- | -----------------------------
userId   | string{32} | 用户的 id
tagId  | string     | 标签id

### 请求体

无

### 响应体

如果存在, 跳转到 `/tags/:tagId`

### HTTP 请求

```
GET  /v2/users/:userId/tagName/:tagName
HEAD /v2/users/:userId/tagName/:tagName
```

### URL 参数

参数名   | 值类型     | 描述
-------- | ---------- | -----------------------------
userId   | string{32} | 用户的 id
tagName  | string     | 标签名

### 请求体

无

### 响应体

如果存在, 跳转到 `/tags/:tagName`


---

## 获取关注的标签列表

### HTTP 请求

```
GET /v2/users/:id/tags
GET /v2/users/:id/tags_id
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | -------------------------------
id        | string{32} | 用户的 id
special   |boolean	   | 是否只要特殊关注，true 返回特殊关注；false返回 全部，按 特殊关注权重倒叙。默认false

### 请求体

无

### 响应头

```
count:100
```

### 响应体

通常情况下返回:

```
[tags]
```


```
[ids]
```

---

## 取消关注标签

### HTTP 请求

```
DELETE  /v2/users/:userId/tags/:tagId

```

### URL 参数

参数名   | 值类型     | 描述
-------- | ---------- | -----------------------------
userId   | string{32} | 用户的 id
tagId  | string{32}     | 标签id

### 请求体

无

### 响应体

无

---

### HTTP 请求

```
GET  /v2/users/:userId/tagName/:tagName
HEAD /v2/users/:userId/tagName/:tagName
```

### URL 参数

参数名   | 值类型     | 描述
-------- | ---------- | -----------------------------
userId   | string{32} | 用户的 id
tagName  | string     | 标签名

### 请求体

无

### 响应体

无
