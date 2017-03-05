# 用户

用户是网站的基本成员.

**用户**
* [创建用户](#创建用户)
* [获取用户](#获取用户)
* [更新用户](#更新用户)
* [修改用户密码](#修改用户密码)

**关注者**
* [获取用户关注者](#获取用户关注者)
* [获取用户的关注者列表](#获取用户的关注者列表)

**关注中的用户**
* [添加关注中的用户](#添加关注中的用户)
* [获取关注中的用户](#获取关注中的用户)
* [获取关注中的用户列表](#获取关注中的用户列表)

**收藏夹**
* [关注收藏夹](#关注收藏夹)
* [获取用户创建的收藏夹](#获取用户创建的收藏夹)
* [获取用户关注的收藏夹](#获取用户关注的收藏夹)
* [获取用户关注的收藏夹列表](#获取用户关注的收藏夹列表)
* [取消关注收藏夹](#取消关注收藏夹)

**标签**
* [关注标签](#关注标签)
* [获取关注的标签](#获取关注的标签)
* [获取关注的标签列表](#获取关注的标签列表)
* [取消关注标签](#取消关注标签)

## 创建用户

### HTTP 请求

```
POST /v2/users
```

### URL 参数

无

### 请求体

```
{
  email: string // Email 地址
  password: string // 密码
}
```

### 响应体

```
{
  id: string // 用户的id
  nickname: string // 昵称, 默认为 id, 可修改一次
  password: string // 密码
  email: string // Email 地址
  url_token: string // 个性域名, 默认为 id, 可修改一次
  create_at: number // 注册时间, Unix 时间戳
  is_admin: boolean // 是否是管理员
}
```

---

## 获取用户

### HTTP 请求

```
GET /v2/users/:id
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

无

### 响应体

```
{
  id: string // 用户的id
  nickname: string // 昵称, 默认为 id, 可修改一次
  url_token: string // 个性域名, 默认为 id, 可修改一次
  create_at: number // 注册时间, Unix 时间戳
  is_admin: boolean // 是否是管理员
  following_count: number // 正在关注数量
  follower_count: number // 关注者数量
  collections_count: number // 收藏夹数量
  following_collections_count: number // 关注的收藏夹数量
  following_tags_count: number // 关注的标签数量
}
```

---

## 更新用户

### HTTP 请求

```
PUT   /v2/users/:id
PATCH /v2/users/:id
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  nickname: string // 昵称, 默认为 id, 可修改一次
  url_token: string // 个性域名, 默认为 id, 可修改一次
}
```

### 响应体

```
{
  id: string // 用户的id
  nickname: string // 昵称, 默认为 id, 可修改一次
  password: string // 密码
  email: string // Email 地址
  url_token: string // 个性域名, 默认为 id, 可修改一次
  create_at: number // 注册时间, Unix 时间戳
  is_admin: boolean // 是否是管理员
}
```

---

## 修改用户密码

### HTTP 请求

```
PUT   /v2/users/:id/password
PATCH /v2/users/:id/password
```

### 请求体

```
{
  old_passowrd: string // 旧密码
  new_password: string // 新密码
}
```

### 响应体

无

---

## 获取用户关注者

### HTTP 请求

```
GET  /v2/users/:user_id/followers/:follower_user_id
HEAD /v2/users/:user_id/followers/:follower_user_id
```

### URL 参数

参数名            | 值类型      | 描述
---------------- | ---------- | -------------------------------------------------------
user_id          | string{32} | 用户的 id
follower_user_id | string     | 关注者的用户id

### 请求体

无

### 响应体

如果存在, 302 跳转至 `/users/:follower_user_id`

---

## 获取用户的关注者列表

### HTTP 请求

```
GET /v2/users/:id/followers
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id
count     |            | 可选, 属性请求

### 请求体

无

### 响应体

通常情况下返回:

```
[users]
```

当属性请求 count 存在时, 返回

```
number
```

---

## 添加关注中的用户

### HTTP 请求

```
POST /v2/users/:id/following
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  user_id: string // 添加的用户 id
}
```

### 响应体

无

---

## 获取关注中的用户

### HTTP 请求

```
GET  /v2/users/:user_id/following/:following_user_id
HEAD /v2/users/:user_id/following/:following_user_id
```

### URL 参数

参数名             | 值类型      | 描述
----------------- | ---------- | -------------------------------------------------------
user_id           | string{32} | 用户的 id
following_user_id |            | 需要查询的正在关注者 id

### 请求体

无

### 响应体

如果存在, 302 跳转至 `/users/:user_id`

---

## 获取关注中的用户列表

### HTTP 请求

```
GET /v2/users/:id/following
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id
count     |            | 可选, 属性请求

### 请求体

无

### 响应体

通常情况下返回:

```
[users]
```

当属性请求 count 存在时, 返回

```
number
```

---

## 关注收藏夹

### HTTP 请求

```
POST /v2/users/:id/following_collections
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  collection_id: string // 收藏夹的 id
}
```

### 响应体

无

---

## 获取用户创建的收藏夹

### HTTP 请求

```
GET /v2/users/:id/collections
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id
count     |            | 可选, 属性请求

### 请求体

无

### 响应体

通常情况下返回:

```
[collections]
```

当属性请求 count 存在时, 返回

```
number
```

---

## 获取用户关注的收藏夹

### HTTP 请求

```
GET  /v2/users/:user_id/following_collections/:collection_id
HEAD /v2/users/:user_id/following_collections/:collection_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | ---------------------------------------------------
user_id       | string{32} | 用户的 id
collection_id | string     | 收藏夹的 id

### 请求体

无

### 响应体

如果该用户关注了此收藏夹, 302 跳转到 `/v2/collections/:collection_id`

---

## 获取用户关注的收藏夹列表

### HTTP 请求

```
GET /v2/users/:id/following_collections
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id
count     |            | 可选, 属性请求

### 请求体

无

### 响应体

通常情况下返回:

```
[collections]
```

当属性请求 count 存在时, 返回

```
number
```

---

## 取消关注收藏夹

### HTTP 请求

```
DELETE /v2/users/:user_id/following_collections/:collection_id
```

### URL 参数

参数名         | 值类型      | 描述
------------- | ---------- | ---------------------------------------------------
user_id       | string{32} | 用户的 id
collection_id | string     | 收藏夹的 id

### 请求体

无

### 响应体

无

---

## 关注标签

### HTTP 请求

```
POST /v2/users/:id/following_tags
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id

### 请求体

```
{
  tag_name: string // 标签名
}
```

### 响应体

无

---

## 获取关注的标签

### HTTP 请求

```
GET  /v2/users/:user_id/following_tags/:tag_name
HEAD /v2/users/:user_id/following_tags/:tag_name
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
user_id   | string{32} | 用户的 id
tag_name  | string     | 标签名

### 请求体

无

### 响应体

如果存在, 跳转到 `/tags/:tag_name`

---

## 获取关注的标签列表

### HTTP 请求

```
GET /v2/users/:id/following_tags
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
id        | string{32} | 用户的 id
count     |            | 可选, 属性请求

### 请求体

无

### 响应体

通常情况下返回:

```
[tags]
```

当属性请求 count 存在时, 返回

```
number
```

---

## 取消关注标签

### HTTP 请求

```
GET  /v2/users/:user_id/following_tags/:tag_name
HEAD /v2/users/:user_id/following_tags/:tag_name
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
user_id   | string{32} | 用户的 id
tag_name  | string     | 标签名

### 请求体

无

### 响应体

无
