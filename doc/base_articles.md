# 基底文章

基底文章是相同原文地址的文章(articles)的统一来源, 基底文章由页面的 URL MD5 值保证唯一性, 只能通过后台创建, 不可经外部修改.

## 从 URL 的 MD5 值查询基底文章的详细信息

### HTTP 请求

```
GET  /2/base_articles/:url_md5
HEAD /2/base_articles/:url_md5
```

### URL 参数

参数名  |值    |描述
-------|------|-------------------
url_md5|string|文章的 url 的 md5 值

### 请求体

无

### 响应体

```
{
  id: string{32} // 基底文章的 id
  title: string // 基底文章的标题
  body: string // 基底文章的正文内容
  summary: string // 基底文章的摘要
  external_url: string // 基底文章的原文绝对地址(外部地址)
  jump_url: string // 基底文章的跳转绝对地址
  icon_url: string // 基底文章的图标绝对地址
  title_image_url: string[] // 基底文章题图的绝对地址数组, 可能为空
  create_at: number // 基底文章的创建时间, Unix时间戳
  update_at: number // 基底文章的更新时间, Unix时间戳
  tags: string[] // 基底的标签名数组, 此项为后端统计引用自基底文章分支文章的高频标签所生成, 更新频率为一天一次
}
```

## 从 URL 的 MD5 值查询基底文章的分支文章

### HTTP 请求

```
GET  /2/base_articles/:url_md5/forks
HEAD /2/base_articles/:url_md5/forks
```

### URL 参数

参数名  |值     |描述
-------|-------|--------------------------------------------
url_md5|string |文章的 url 的 md5 值
details|boolean|可选, 设置为 true 时, 将一并返回分支文章的内容数据

### 请求体

无

### 响应体

details值为false或未设置时, 返回值为分支文章的 id 数组.

```
[string]
```

details值为true时, 返回值为分支文章的详细内容数组, 详细格式参考`GET /2/articles`.

```
[articles]
```
