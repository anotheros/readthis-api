# 分支文章

分支文章是主要的操作对象, 分支文章基于基底文章(base_articles)衍生而来, 具备可编辑性.

## 获取分支文章详细信息

### HTTP 请求

```
GET  /v2/articles/:id
HEAD /v2/articles/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 分支文章的 id

### 请求体

无

### 响应体

```
{
  id: string // 文章的 id
  title: string // 文章标题
  body: string // 文章的正文内容
  summary: string // 文章摘要
  external_url: string // 文章的原文绝对地址(外部地址)
  jump_url: string // 文章的跳转绝对地址
  icon_url: string // 文章的图标绝对地址
  title_image_url: string[] // 题图的绝对地址数组, 可能为空
  create_at: number // 文章创建时间, Unix时间戳
  update_at: number // 文章更新时间, Unix时间戳
  tags: string[] // 标签名数组, 可能为空
  remark: string // 分支文章的备注
  base_id: string{32} // 对应基底文章的 id
  user_id: string // 对应创建该分支文章的用户的 id
}
```

---

## 创建新的(分支)文章

若 URL 未被记录在库, 则会自动建立相应的基底文章.

### HTTP 请求

```
POST /v2/articles
```

### URL 参数

无

### 请求体

```
{
  title: string // 文章标题
  external_url: string // 文章的原文绝对地址(外部地址)
  tags: string[] // 标签名数组, 可能为空
  remark: string // 分支文章的备注
  collection_id: string // 用户的收藏夹 id, 文章将被添加到这个收藏夹, 此值为null时, 服务器会将文章添加到该用户的默认收藏夹
}
```

### 响应体

```
{
  id: string // 文章的 id
  title: string // 文章标题
  body: string // 文章的正文内容
  summary: string // 文章摘要
  external_url: string // 文章的原文绝对地址(外部地址)
  jump_url: string // 文章的跳转绝对地址
  icon_url: string // 文章的图标绝对地址
  title_image_url: string[] // 题图的绝对地址数组, 可能为空
  create_at: number // 文章创建时间, Unix时间戳
  update_at: number // 文章更新时间, Unix时间戳
  tags: string[] // 标签名数组, 可能为空
  remark: string // 分支文章的备注
  base_id: string{32} // 对应基底文章的 id
  user_id: string // 对应创建该分支文章的用户的 id
}
```

---

## 修改分支文章

### HTTP 请求

```
PUT   /v2/articles/:id
PATCH /v2/articles/:id
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 分支文章的 id

### 请求体

对于 PUT 请求, 需要包含完整的数据结构, 对于 PATCH 请求, 只需要部分.

```
{
  title: string // 文章标题
  tags: string[] // 标签名数组, 可能为空
  remark: string // 分支文章的备注
}
```

### 响应体

```
{
  id: string // 文章的 id
  title: string // 文章标题
  body: string // 文章的正文内容
  summary: string // 文章摘要
  external_url: string // 文章的原文绝对地址(外部地址)
  jump_url: string // 文章的跳转绝对地址
  icon_url: string // 文章的图标绝对地址
  title_image_url: string[] // 题图的绝对地址数组, 可能为空
  create_at: number // 文章创建时间, Unix时间戳
  update_at: number // 文章更新时间, Unix时间戳
  tags: string[] // 标签名数组, 可能为空
  remark: string // 分支文章的备注
  base_id: string{32} // 对应基底文章的 id
  user_id: string // 对应创建该分支文章的用户的 id
}
```
