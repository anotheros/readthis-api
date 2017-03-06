# 微刊

微刊是用户建立的用于收集文章的容器.

**微刊**
* [创建微刊](#创建微刊)
* [获取微刊](#获取微刊)
* [更新微刊](#更新微刊)
* [删除微刊](#删除微刊)
* [根据名称搜索微刊](#根据名称搜索微刊)

**微刊内的文章**
* [向微刊内添加文章](#向微刊内添加文章)
* [修改微刊内文章](#修改微刊内文章)
* [获取微刊内的文章列表](#获取微刊内的文章列表)
* [检测微刊内是否存在特定的文章](#检测微刊内是否存在特定的文章)
* [删除微刊内的文章](#删除微刊内的文章)

**其他**
* [获取微刊的关注者列表](#获取微刊的关注者列表)

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
}
```

### 响应体

```
{
  id: string{32} // 微刊的 id
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  create_at: number // 创建微刊的时间, Unix 时间戳
  update_at: number // 更新微刊的时间, Unix 时间戳
  user_id: string{32} // 创建微刊的用户的 id
  is_default: boolean // 是否为默认微刊
}
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
  create_at: number // 创建微刊的时间, Unix 时间戳
  update_at: number // 更新微刊的时间, Unix 时间戳
  user_id: string{32} // 创建微刊的用户的 id
  articles_count: number // 微刊内包含的文章数量
  followers_count: number // 该微刊的关注者数量
  is_default: boolean // 是否为默认微刊
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
  name: string // 微刊的名称
  description: string // 微刊的描述文字
}
```

### 响应体

```
{
  id: string{32} // 微刊的 id
  name: string // 微刊的名称
  description: string // 微刊的描述文字
  create_at: number // 创建微刊的时间, Unix 时间戳
  update_at: number // 更新微刊的时间, Unix 时间戳
  user_id: string{32} // 创建微刊的用户的 id
  is_default: boolean // 是否为默认微刊
}
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

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
keyword   | string     | 搜索微刊的关键字
cursor    | string{32} | 起始微刊的 id
direction | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
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
POST /v2/collections/:collection_id/articles
```

### URL 参数

参数名     | 值类型      | 描述
---------- | ---------- | -----------
id         | string{32} | 微刊的 id

### 请求体

```
{
  article_id: string{32} // 需要添加到微刊的文章的 id
  title: string // 可选,文章标题
  external_url: string //可选, 文章的原文绝对地址(外部地址)
  tags: string[] //可选, 标签名数组, 可能为空
  remark: string //可选, 文章的备注
}
```

### 响应体

无, 服务器应返回 204.

---

## 修改微刊内文章

### HTTP 请求

```
PUT /v2/collections/:collection_id/articles
PATCH /v2/collections/:collection_id/articles
```

### URL 参数

参数名     | 值类型      | 描述
---------- | ---------- | -----------
id         | string{32} | 微刊的 id

### 请求体

```
{
  article_id: string{32} // 需要添加到微刊的文章的 id
  title: string // 文章标题
  external_url: string // 文章的原文绝对地址(外部地址)
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
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 微刊的 id
cursor    | string     | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
direction | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number     | 可选, 限制返回的结果数量, 默认为 20
count     |            | 可选, 这是一个属性请求, 存在该参数时, 将忽略除 id 外的所有参数, 返回结果改为目标微刊的文章总数

### 请求体

无

### 响应体

通常情况下返回值为数组:

```
[articles]
```

当存在 count 属性请求时返回值为:

```
{
  count: number
}
```

---

## 获取微刊内的文章

### HTTP 请求

```
GET /v2/collections/:collection_id/articles/:article_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | -----------
collection_id | string{32} | 微刊的 id
article_id    | string{32} | 文章的 id

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
HEAD /v2/collections/:collection_id/articles/:article_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | -----------
collection_id | string{32} | 微刊的 id
article_id    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---

## 删除微刊内的文章

### HTTP 请求

```
DELETE /v2/collections/:collection_id/articles/:article_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | -----------
collection_id | string{32} | 微刊的 id
article_id    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---

## 获取微刊的关注者列表

### HTTP 请求

```
GET /v2/collections/:id/follower
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 微刊的 id
count     |            | 可选, 这是一个属性请求, 存在该参数时, 将忽略除 id 外的所有参数, 返回结果改为目标微刊的关注者总数

### 请求体

无

### 响应体

通常情况下返回值为数组:

```
[users]
```

当存在 count 属性请求时返回值为:

```
{
  count: number
}
```
