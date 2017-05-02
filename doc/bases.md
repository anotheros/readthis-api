


## 用URL获取文章

### HTTP 请求

```
GET  /v2/proxy
HEAD /v2/proxy
```

### URL 参数

参数名   | 值类型  | 描述
------- | ------ | -------------------
url | string | 文章的 url ，需要urlencode

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
### 举例

```
https://api.100000p.com/v2/proxy?url=https%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMjM5NzE2MzAwMA%3D%3D%26mid%3D204800240%26idx%3D1%26sn%3Dc91bfbf4a8b435beec34596c4805d12b
```
---

