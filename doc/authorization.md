# 授权

授权管理.

**授权**

* [创建授权](#创建授权)
* [注销授权](#注销授权)
* [判断token是否过期](#判断token是否过期)

## 创建授权

### HTTP 请求

```
POST /v2/authorization
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
### 响应头
```
Token: xxxxxx//认证token
```

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

## 判断token是否过期

```
head /v2/authorization/:token
```

### URL 参数

参数名 | 值类型  | 描述
----- | ------ | -------
token | string | token

### 请求体

无
### 响应头

204
401

### 响应体

无
---

## 注销授权

```
DELETE /v2/authorization/:token
```

### URL 参数

参数名 | 值类型  | 描述
----- | ------ | -------
token | string | token

### 请求体

无

### 响应体

无
