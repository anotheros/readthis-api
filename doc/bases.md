# 文章

文章是相同原文地址的文章(articles)的统一来源, 文章由页面的 URL MD5 值保证唯一性, 只能通过后台创建, 不可经外部修改.

**文章**
* [用URL的MD5值获取文章](#用URL的MD5值获取文章)

**分支文章**
* [用URL的MD5值获取文章的分支文章](#用URL的MD5值获取文章的分支文章)

## 用URL的MD5值获取文章

### HTTP 请求

```
GET  /v2/bases/:urlMd5
HEAD /v2/bases/:urlMd5
```

### URL 参数

参数名   | 值类型  | 描述
------- | ------ | -------------------
urlMd5 | string | 文章的 url 的 md5 值

### 请求体

无

### 响应体

```
{
  id: string{32} // 文章的 id
  title: string // 文章的标题
  body: string // 文章的正文内容
  summary: string // 文章的摘要
  externalUrl: string // 文章的原文绝对地址(外部地址)
  jumpUrl: string // 文章的跳转绝对地址
  iconUrl: string // 文章的图标绝对地址
  titleImageUrl: string[] // 文章题图的绝对地址数组, 可能为空
  createTime: number // 文章的创建时间, Unix时间戳
  updateTime: number // 文章的更新时间, Unix时间戳
  tags: tag[] // 基底的标签名数组, 此项为后端统计引用自文章分支文章的高频标签所生成, 更新频率为一天一次
}
```

---

