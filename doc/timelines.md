# 时间线

时间线是以时间进行降序排列的分支文章(articles)列表.

**时间线**
* [获取分支文章列表](#获取分支文章列表)

## 获取分支文章列表

### HTTP 请求

```
GET  /v2/timelines
HEAD /v2/timelines
```

### URL 参数

参数名     | 值类型          | 描述
--------- | -------------- | ------------------------------------------------------
tag       | string         | 可选, 需要查询的标签名, 需要 URL encode
cursor    | string         | 可选, 作为起始点的 article 的 id, 如果此项为空, 后端将默认以最新的 article 作为起始点
direction | string         | 可选, 有关时间的查询方向, 可选值为 newer 或 older, 默认为 older
limit     | number         | 可选, 限制返回的结果数量, 默认为 20

### 请求体

无

### 响应体

返回值为数组.

```
[articles]
```
