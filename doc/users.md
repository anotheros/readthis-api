# 用户

用户是基本成员.

## 根据用户 id 获取用户详细信息

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

## 注册用户

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

## 更新用户资料

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

## 根据用户 id 获取用户关注者

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

## 根据用户 id 获取用户的关注者列表

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

## 添加正在关注者

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

## 根据用户 id 获取用户正在关注的用户列表

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

## 根据用户 id 获取用户正在关注的用户

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

## 根据用户 id 获取其收藏夹

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

## 取消收藏夹关注

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

## 从用户处获取其关注的收藏夹

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

## 添加关注的收藏夹

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

## 根据用户 id 获取其关注的收藏夹

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

## 删除关注的标签

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

---

## 从用户处获取其关注的标签

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

## 根据用户 id 获取关注的标签

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

## 添加关注的收藏夹

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
