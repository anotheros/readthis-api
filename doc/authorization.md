# 授权

授权管理.

**授权**
* [创建授权](#创建授权)
* [注销授权](#注销授权)

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

### 响应体

```
{
  user_id: string
  token: string
}
```

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
