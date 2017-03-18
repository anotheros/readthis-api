# 微刊

微刊是用户建立的用于收集文章的容器.

**微刊**
* [创建微刊](#创建微刊)√
* [发布期刊](#发布期刊)√
* [获取微刊](#获取微刊)√
* [更新微刊](#更新微刊)√
* [删除微刊](#删除微刊)√
* [根据名称搜索微刊](#根据名称搜索微刊)

**微刊内的文章**
* [向微刊内添加文章](#向微刊内添加文章)√
* [修改微刊内文章](#修改微刊内文章)√
* [获取微刊内的文章列表](#获取微刊内的文章列表)√
* [检测微刊内是否存在特定的文章](#检测微刊内是否存在特定的文章)√
* [删除微刊内的文章](#删除微刊内的文章)√
* [查询期刊内文章](#查询期刊内文章)√

**其他**
* [获取微刊的关注者列表](#获取微刊的关注者列表)√

---

## 创建微刊

### HTTP 请求

```
POST /v2/collections
```

### URL 参数

无

### 请求体

```
{
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  userId: string{32} // 可选,创建微刊的用户的 id
  visible:boolean //可选, 是否公开;默认 是
}
```

### 响应体

```
{
  id: string{32} // 微刊的 id
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  createTime: number // 创建微刊的时间, Unix 时间戳
  updateTime: number // 更新微刊的时间, Unix 时间戳
  userId: string{32} // 创建微刊的用户的 id
  isDefault: boolean // 是否为默认微刊
  visible:boolean // 是否公开
  stages:number //总期刊数量，当前期刊
}
```

---


## 发布期刊

### HTTP 请求

```
POST /v2/collections/:collectionsId/stages/:stages
```

### URL 参数


参数名           | 值类型     | 描述
---------------- | ---------- | -----------
collectionsId    | string{32} | 微刊的 id
stages           |int         | 第几期刊。

### 请求体

无

### 响应头
204 或者其他

### 响应体

```

```

---

## 获取微刊

### HTTP 请求

```
GET  /v2/collections/:id
HEAD /v2/collections/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 微刊的 id

### 请求体

无

### 响应体

```
{
  id: string{32} // 微刊的 id
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  createAt: number // 创建微刊的时间, Unix 时间戳
  updateAt: number // 更新微刊的时间, Unix 时间戳
  userId: string{32} // 创建微刊的用户的 id
  articlesCount: number // 微刊内包含的文章数量
  fansCount: number // 该微刊的关注者数量
  isDefault: boolean // 是否为默认微刊
  visible:boolean // 是否公开
  stages:number //总期刊数量，当前期刊
}
```

---

## 更新微刊

### HTTP 请求

```
PUT   /v2/collections/:id
PATCH /v2/collections/:id
```

### URL 参数

无

### 请求体

```
{
  id: string{32} // 必填,微刊的 id
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  userId: string{32} // 创建微刊的用户的 id
  isDefault: boolean // 是否为默认微刊
  visible:boolean // 是否公开
}
```

### 响应体

```

```

---

## 删除微刊

```
DELETE /v2/collections/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 微刊的 id

### 请求体

无

### 响应体

无

---

## 根据名称搜索微刊

### HTTP 请求

```
GET /v2/collections
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | ----------------------------
keyword   | string     | 搜索微刊的关键字
cursor    | string{32} | 起始微刊的 id
order     | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number     | 可选, 限制返回的结果数量, 默认为 20

### 请求体

无

### 响应体

返回数组

```
[collections]
```

---

## 向微刊内添加文章

### HTTP 请求

```
POST /v2/collections/:collectionId/articles
```

### URL 参数

参数名         | 值类型     | 描述
-------------- | ---------- | -----------
collectionId   | string{32} | 微刊的 id

### 请求体

```
{
  articleId: string{32} //可选,需要添加到微刊的文章的 id
  title: string // 可选,文章标题
  url: string //可选, 文章的原文绝对地址(外部地址)
  tags: string[] //可选, 标签名数组, 可能为空
  remark: string //可选, 文章的备注
}
(articleId,url 其一必填，都写以id为主) 
```

### 响应体

无, 服务器应返回 204.

---

## 修改微刊内文章

### HTTP 请求

```
PUT /v2/collections/:collectionId/articles/:articleId
PATCH /v2/collections/:collectionId/articles/:articleId
```

### URL 参数

参数名           | 值类型     | 描述
--------------- | ---------- | -----------
collectionId    | string{32} | 微刊的 id
articleId       |string{32}  |文章的 id

### 请求体

```
{
  articleId: string{32} // 文章的 id
  title: string // 文章标题
  tags: string[] // 标签名数组, 可能为空
  remark: string // 文章的备注
}
```

### 响应体

无, 服务器应返回 204.
---

## 获取微刊内的文章列表

### HTTP 请求

```
GET /v2/collections/:id/articles
head /v2/collections/:id/articles
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | ------------------------------------
id        | string{32} | 微刊的 id
cursor    | string     | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
order     | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number     | 可选, 限制返回的结果数量, 默认为 20


### 请求体

无

### 响应头

```
count:100
```

### 响应体


```
[articles]
```


---

## 获取微刊内的文章

### HTTP 请求

```
GET /v2/collections/:collectionId/articles/:articleId
```

### URL 参数

参数名       | 值类型     | 描述
------------ | ---------- | -----------
collectionId | string{32} | 微刊的 id
articleId    | string{32} | 文章的 id

### 请求体

无

### 响应体

```
[articles]
```

---

## 检测微刊内是否存在特定的文章

### HTTP 请求

```
HEAD /v2/collections/:collectionId/articles/:articleId
```

### URL 参数

参数名       | 值类型     | 描述
------------ | ---------- | -----------
collectionId | string{32} | 微刊的 id
articleId    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---

## 删除微刊内的文章

### HTTP 请求

```
DELETE /v2/collections/:collectionId/articles/:articleId
```

### URL 参数

参数名       | 值类型     | 描述
------------ | ---------- | -----------
collectionId | string{32} | 微刊的 id
articleId    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---


## 查询期刊内文章

### HTTP 请求

```
GET /v2/collections/:collectionsId/stages/:stages
```

### URL 参数


参数名           | 值类型     | 描述
---------------- | ---------- | -----------
collectionsId    | string{32} | 微刊的 id
stages           |int         | 第几期刊。

### 请求体

无

### 响应头


### 响应体

```
[articles]
```

---
## 获取微刊的关注者列表

### HTTP 请求

```
GET /v2/collections/:id/fans
HEAD /v2/collections/:id/fans
```

### URL 参数

参数名    | 值类型     | 描述
--------- | ---------- | ------------------------------
id        | string{32} | 微刊的 id


### 请求体

无

### 响应头

```
count:100
```

### 响应体

通常情况下返回值为数组:

```
[users]
```

