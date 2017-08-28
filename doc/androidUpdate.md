Android 更新配置

##lite版本

### HTTP 请求

```
GET  /androidUpdate/lite/{:id}.json
```

### URL 参数

参数名 | 值类型      | 描述
----- | ---------- | -----------
id    | string{32} | 用户的 id


##大版本

### HTTP 请求

```
GET  /androidUpdate/update.json
```

### 相应体

```
{
codeVersion: int //版本号
md5:string //当前apk包的md5值
force: boolean // true 为强制更新
msg:sting //更新提示语
}
```