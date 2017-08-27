该需求简单暴利。

功能如同 [小程序版本](https://github.com/zhangshanhai/collection-xcx)。
非常像 今日头条小程序。只是做成app 只读版本，用户只能读和分享。不能收藏。


让不同开发的运营，直接能生成自己的app。

如果运营需要定制需求，直接找对应的客户端开发。进行收费定制。

做完后应该很像 [湾区日报](https://wanqu.co/about/)。



使用api 
1.userId 可以在配置文件配置。方便程序员生成app，admob 广告标识符配置（7使用）。

2.通过[获取用户创建的微刊](https://github.com/zhangshanhai/readthis-api/blob/master/doc/users.md#%E8%8E%B7%E5%8F%96%E7%94%A8%E6%88%B7%E5%88%9B%E5%BB%BA%E7%9A%84%E5%BE%AE%E5%88%8A) api，拉去头部HorizontalScrollView 内容。

3.1通过[获取微刊内的文章列表](https://github.com/zhangshanhai/readthis-api/blob/master/doc/collections.md#%E8%8E%B7%E5%8F%96%E5%BE%AE%E5%88%8A%E5%86%85%E7%9A%84%E6%96%87%E7%AB%A0%E5%88%97%E8%A1%A8) api,拉取文章列表。

3.2 按tagId过滤 微刊内文章。3.1api 含tagId即可。

4.文章字段，snapshot:boolean // 是否支持快照，支持快照时表示服务器中有body 缓存。如果不支持，客户端需要在 app内置webviwe中打开jumpUrl 地址。

5.[根据文章id、微刊id，获取文章](https://github.com/zhangshanhai/readthis-api/blob/master/doc/collections.md#%E8%8E%B7%E5%8F%96%E5%BE%AE%E5%88%8A%E5%86%85%E7%9A%84%E6%96%87%E7%AB%A0) 含body字段，body用md 渲染。

6.在5页面，正文结尾 查看原文地址。如4功能。

7.在5页面 添加admob 广告。 在3列表页面 加入 admob 广告。

8.分享功能，分享谋篇文章（调用系统），分享某 微刊最近10篇文章（直接到剪切板）

9.离线收藏功能，sqlite 。用户删除app 即丢失这些数据。

10.其他周边，清理缓存，字体大小，夜间主题 。可做可不做。







查看小程序例子。

![](https://github.com/zhangshanhai/collection-xcx/raw/master/gh_7f4a7039e66b_344.jpg)
