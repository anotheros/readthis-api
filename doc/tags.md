# 标签

**标签**
* [根据标签名获取标签](#根据标签名获取标签)

**其他**
* [根据标签名获取标签的关注者](#根据标签名获取标签的关注者)

## 根据标签名获取标签

### HTTP 请求

```
GET  /v2/tags/:tagName
HEAD /v2/tags/:tagName
```

### URL 参数

参数名     | 值类型      | 描述
--------- | ---------- | -------------------------------------------------------
tagName  | string     | 标签名, 需要 URL encode

### 请求体

无

### 响应体

```
{
  id：string
  name: string // 标签名
  fansCount: number // 关注标签的用户数量
}
```

---

## 根据标签名获取标签的关注者

### HTTP 请求

```
GET  /v2/tags/:tagName/fans
HEAD /v2/tags/:tagName/fans
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


>  使用tagId 查询时，地址换为/v2/tagId/:tagId  其他不变