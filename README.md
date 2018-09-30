# XyKey-OpenFormat
与 XyKey 兼容的开放原文格式

XyKey 对用户数据的原文导出功能做了增强，使用了 JSON 格式对关键的属性做了包装，方便其它 APP 进行导入处理。

## 这个开放格式只把最重要和通用的属性提取
- 项目名称（必须有值的核心属性）-name
- 账号-account
- 密码1（用作最主要的密码）-password
- 密码2（考虑很多支付类信息需要额外的支付密码而设立的密码）-password2
- 链接（用作快速跳转或记录产品网页）-url
- 备注-note
- 用户自定义的条目-ertra

兼容目前绝大多数密码管理 app 的数据设计。

这个开放格式是 xykey 为了降低用户对数据迁移的难度而设计的，因为任何开发者都没法保证自己的产品能永远保持更新维护，我个人也不认为 xykey 优秀到能取代其它同类 app ，xykey 也有很多设计上不如其它 app 的地方。
所以不妨开放这样一个格式，在这些独立产品之间能简单地互通一些常规数据，不仅能为自己引流更多愿意尝试的用户，用户使用的心理负担也更低，最终还是为了让大家的 app 都能做的更好，让更多人培养起保护管理自己账号密码的习惯，也算是为历史做了贡献。

所以任何有兴趣的、想为自己导入 xykey 用户的、或者同样希望为用户降低负担的开发者，都可以选择支持导入这个格式的数据。不强求支持导出这个格式。

## 格式说明
此格式下所有属性都不能为空或缺漏，即使是没有数据的字段，也需要装载。

### 最外层
```
{
    "version": "用来判断数据格式的版本，方便做版本兼容处理，Number类型，目前为 1 ",
    "key": "用来存储key对象的数组，Array类型"
}
```

### key对象
```
{
    "name": "条目名称，长度必须大于 0，string类型",
    "account": "账号，string类型",
    "password": "密码，string类型",
    "password2": "密码2，string类型",
    "url": "链接，string类型",
    "note": "备注，string类型",
    "extra": "额外自定义字段数组，Array类型"
}
```
### extra对象
```
{
    "name": "名称，String类型",
    "content": "内容，String类型"
}
```
## 完整示例：
```
{
    "version": 1,
    "key": [
        {
            "name": "test1",
            "account": "test@test.com",
            "password": "123456",
            "password2": "",
            "url": "http://www.google.com",
            "note": "",
            "extra": []
        },
        {
            "key": [
                {
                    "name": "test2",
                    "account": "",
                    "password": "",
                    "password2": "9317",
                    "url": "",
                    "note": "www.github.com",
                    "extra": [
                        {
                            "name": "custom",
                            "content": "field"
                        }
                    ]
                }
            ]
        }
    ]
}
```
