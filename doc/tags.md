# 标签

**标签**

* [根据标签名获取标签](#根据标签名获取标签)
* [根据id获取标签](#根据id获取标签)
* [查询所有标签](#查询所有标签)

**其他**

* [根据标签名获取标签的关注者](#根据标签名获取标签的关注者)
* [根据标签id获取标签的关注者](#根据标签id获取标签的关注者)

## 根据id获取标签

### HTTP 请求

```
GET  /v2/tags/:tagId
HEAD /v2/tags/:tagId
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
tagId  | string     | tagId

### 请求体

无

### 响应体

```
{
  id：string
  tagName: string // 标签名
  fansCount: number // 关注标签的用户数量
  following:boolean //是否关注状态，不 幂等
  special: number //关注 权重 ，不幂等
  summaryCount: number // 关联文章数量，不幂等，为0 未使用
}
```

---
## 查询所有标签

### HTTP 请求

```
GET  /v2/tags
HEAD /v2/tags
```

### URL 参数

参数名     | 值类型          | 描述
--------- | -------------- | ------------------------------------------------------
wd        |string          | 可选, 搜索关键词
cursor    | string         | 可选, 作为起始点的 tag 的 id, 如果此项为空, 后端将默认以最新的 tag 作为起始点
limit     | number         | 可选, 限制返回的结果数量, 默认为 20

### 请求体

无

### 响应体

```
[tag]
```

---


## 根据标签id获取标签的关注者

### HTTP 请求

```
GET  /v2/tags/:tagId/fans
HEAD /v2/tags/: tagId/fans
```

### URL 参数

参数名   | 值类型    | 描述
-------- | --------- | ----------------------------
tagId  | string    | tagId

### 请求体

无

### 响应头

count:100

### 响应体

返回值为数组:

```
[users]
```


## 根据标签名获取标签

### HTTP 请求

```
GET  /v2/tagName/:tagName
HEAD /v2/tagName/:tagName
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
tagName  | string     | 标签名, 需要 URL encode

### 请求体

无

### 响应体

```
{tag}
```

---

## 根据标签名获取标签的关注者

### HTTP 请求

```
GET  /v2/tagName/:tagName/fans
HEAD /v2/tagName/:tagName/fans
```

### URL 参数

参数名   | 值类型    | 描述
-------- | --------- | ----------------------------
tagName  | string    | 标签名, 需要 URL encode


### 请求体

无

### 响应头

count:100

### 响应体

返回值为数组:

```
[users]
```
