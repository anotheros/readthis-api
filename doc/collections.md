# 收藏夹

收藏夹是用户建立的分支文章列表.

## 获取的关注者

### HTTP 请求

```
GET /v2/collections/:id/follower
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 收藏夹的 id
count     |            | 可选, 这是一个属性请求, 存在该参数时, 将忽略除 id 外的所有参数, 返回结果改为目标收藏夹的关注者总数

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

---

## 根据名称搜索收藏夹

### HTTP 请求

```
GET /v2/collections
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
keyword   | string     | 搜索收藏夹的关键字
cursor    | string{32} | 起始收藏夹的 id
direction | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number     | 可选, 限制返回的结果数量, 默认为 20

### 请求体

无

### 响应体

返回数组

```
[collections]
```

## 获取收藏夹信息

### HTTP 请求

```
GET  /v2/collections/:id
HEAD /v2/collections/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 收藏夹的 id

### 请求体

无

### 响应体

```
{
  id: string{32} // 收藏夹的 id
  name: string // 收藏夹的名称
  description: string // 收藏夹的描述文字
  create_at: number // 创建收藏夹的时间, Unix 时间戳
  update_at: number // 更新收藏夹的时间, Unix 时间戳
  user_id: string{32} // 创建收藏夹的用户的 id
  articles_count: number // 收藏夹内包含的文章数量
  followers_count: number // 该收藏夹的关注者数量
  is_default: boolean // 是否为默认收藏夹
}
```

---

## 创建收藏夹

### HTTP 请求

```
POST /v2/collections
```

### URL 参数

无

### 请求体

```
{
  name: string // 收藏夹的名称
  description: string // 收藏夹的描述文字
}
```

### 响应体

```
{
  id: string{32} // 收藏夹的 id
  name: string // 收藏夹的名称
  description: string // 收藏夹的描述文字
  create_at: number // 创建收藏夹的时间, Unix 时间戳
  update_at: number // 更新收藏夹的时间, Unix 时间戳
  user_id: string{32} // 创建收藏夹的用户的 id
  is_default: boolean // 是否为默认收藏夹
}
```

---

## 更新收藏夹信息

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
  name: string // 收藏夹的名称
  description: string // 收藏夹的描述文字
}
```

### 响应体

```
{
  id: string{32} // 收藏夹的 id
  name: string // 收藏夹的名称
  description: string // 收藏夹的描述文字
  create_at: number // 创建收藏夹的时间, Unix 时间戳
  update_at: number // 更新收藏夹的时间, Unix 时间戳
  user_id: string{32} // 创建收藏夹的用户的 id
  is_default: boolean // 是否为默认收藏夹
}
```

---

## 向收藏夹内添加文章

### HTTP 请求

```
POST /v2/collections/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 收藏夹的 id

### 请求体

```
{
  article_id: string{32} // 需要添加到收藏夹的文章的 id
}
```

### 响应体

无, 服务器应返回 204.

---

## 检测收藏夹内是否存在特定的分支文章

### HTTP 请求

```
HEAD /v2/collections/:collection_id/articles/:article_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | -----------
collection_id | string{32} | 收藏夹的 id
article_id    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---

## 删除收藏夹内的文章

### HTTP 请求

```
DELETE /v2/collections/:collection_id/articles/:article_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | -----------
collection_id | string{32} | 收藏夹的 id
article_id    | string{32} | 文章的 id

### 请求体

无

### 响应体

无

---

## 获取收藏夹内的分支文章序列

### HTTP 请求

```
GET /v2/collections/:id/articles
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 收藏夹的 id
cursor    | string     | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
direction | string     | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number     | 可选, 限制返回的结果数量, 默认为 20
count     |            | 可选, 这是一个属性请求, 存在该参数时, 将忽略除 id 外的所有参数, 返回结果改为目标收藏夹的文章总数

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

## 删除收藏夹

```
DELETE /v2/collections/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 收藏夹的 id

### 请求体

无

### 响应体

无
