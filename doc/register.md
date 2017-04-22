# 注册

该接口用于用户的注册和修改密码，逻辑一样。

**注册**
* [检查用户名](#检查用户名)
* [发送邀请码](#发送邀请码)
* [注册](#注册)


---

## 检查用户名

### HTTP 请求

```
HEAD /v2/user/:userName
```

### URL 参数

| 参数名      | 值类型        | 描述     |
| -------- | ---------- | ------ |
| userName | string{32} | 数字字母组合 |

### 请求体

```

```
### 响应头

| 状态码  | 描述   |
| ---- | ---- |
| 200  | 可用   |
| 409  | 不可用  |

### 响应体

```

```

---


## 发送邀请码

### HTTP 请求

```
POST /v2/email
```

### URL 参数



### 请求体

```
{
email: string //email地址
}
```
### 响应头

| 状态码  | 描述   |
| ---- | ---- |
| 200  | ok   |


### 响应体

```

```

---



## 注册

### HTTP 请求

```
POST /v2/user
```

### URL 参数

无


### 请求体

```
{
    code:string //激活码
    userName:string //用户名
    email:string // 收到邀请码的邮箱
    password:string //明文密码
}
```
### 响应头

| 状态码  | 描述   |
| ---- | ---- |
| 200  | ok   |

```
Token: xxxx
```


### 响应体

注册成功后 自动登录成功。

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
