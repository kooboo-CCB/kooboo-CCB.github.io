# 属性列表

## 前端常用

### 1. DataContext
> kview 引擎的 dataContext(数据上下文)。您可以将值显式设置到 datacontext 中，或者只将值声明为 JS 全局变量，它将可以从 kview 引擎访问。
``` javascript
// 组件1
  <script engine="kscript">
    k.dataContext.set("name","CCB")
    k.dataContext.set("info",{
        age:18,
        type:'any'
    })
</script>
// 组件2
<script engine="kscript">
    let name = k.dataContext.get("name")
    let info = k.dataContext.get("info")
</script>
// 获取之后可以在khtml中使用
<div k-content="info.age"></div>
```

### 2. Response

> 用于将数据设置为 HTTP resposne 流的 HTTP 响应对象
k.Response对象有如下属性
1. binary
2. execute
3. json
4. redirect
5. renderView
6. setHeader
7. statusCode
8. unanthorized
9. write 

 !> 由于缺少文档,以下是`chargpt`对9个方法`可能`的作用说明

> - binary：将响应的内容设置为二进制数据，可以用于下载文件或显示图像等需要以二进制格式传输的内容。
> - execute：执行响应的内容，通常用于执行动态生成的 JavaScript 代码或者其他类型的动态内容。
> - json：将响应的内容设置为 JSON 格式的数据，通常用于 API 响应或其他需要返回结构化数据的场景。
> - redirect：将响应重定向到另一个 URL，通常用于实现页面跳转或者路由功能。
> - renderView：渲染一个 HTML 视图，并将其作为响应返回给客户端，通常用于显示页面内容。
> - setHeader：设置响应的 HTTP 头信息，例如设置响应类型、缓存策略、跨域策略等。
> - statusCode：设置响应的 HTTP 状态码，通常用于表示请求的状态和结果，例如 200 表示成功、404 表示未找到等。
> - unanthorized：设置响应的 HTTP 状态码为 401（未授权），通常用于表示用户需要进行身份验证或者没有访问权限。
> - write：向响应中写入文本内容，通常用于输出 HTML、文本、XML 等格式的内容。

### 3. Request

> 访问 http 请求数据、查询字符串、表单或标头。
> var 值=k.request.queryname；
> var 值=k.request.queryString.queryname；
> var 值=k.request.form.queryname；

**返回示例**

```javascript
{
    "queryString": {},
    "form": {},
    "files": [],
    "body": null,
    "postData": null,
    "method": "GET",
    "clientIp": "118.166.10.26",
    "headers": {
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
        "Host": "dev_2.ninjible-dev-sg.sitepapa.com",
        "UserAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36",
        ":method": "GET",
        "AcceptEncoding": "gzip, deflate, br",
        "AcceptLanguage": "zh-CN,zh;q=0.9",
        "CacheControl": "max-age=0",
        "Cookie": "_site_culture=nl,_gid=GA1.2.17487441.1683628492,_ga=GA1.1.1385787511.1683623736,_site_id_=598a2176-dd5c-383d-70fe-bba727acc0d0,_ga_FC5DZ0P2MF=GS1.1.1683701176.5.1.1683703323.0.0.0,_site_version_=871",
        "Referer": "https://ninjible-dev-sg.sitepapa.com/",
        "UpgradeInsecureRequests": "1",
        "secchua": "\"Chromium\";v=\"112\", \"Google Chrome\";v=\"112\", \"Not:A-Brand\";v=\"99\"",
        "secchuamobile": "?0",
        "secchuaplatform": "\"Windows\"",
        "secfetchsite": "same-site",
        "secfetchmode": "navigate",
        "secfetchuser": "?1",
        "secfetchdest": "document"
    },
    "url": "/test"
}
```

### 4. ClientJS

> 将对象发送到浏览器 JavaScript , 可以向客户端发送信息
Ninjible项目中,在Report-page页面,在服务端请求解析结果并渲染页面,减少客户端白屏时间。
在解析完后，将信息通过 `k.clientJS.setVariable` 方法传递信息给客户端发送邮件使用。
``` javascript
  k.clientJS.setVariable('lang', JSON.stringify(lang))
  k.clientJS.setVariable('pageState', JSON.stringify(pageState))
  k.clientJS.setVariable('requestdata', requestdata)
```
!> 传递给客户端的变量会挂载在全局对象`window`上

### 5. Session

> 用于小型交互式信息的临时存储器。会话不持续
> k.session.set（“key”，obj）；
> var back=k.session.get（“key”）；
> k.session.newkey=“值”；

#### 7. Info

> 当前请求信息 返回示例如下
>
> 可以获取常用信息有：Culture，BaseUrl

```Javascript
{
    "Culture": "nl",
    "Name": "dev_2",
    "Setting": {},
    "User": {
        "UserName": null,
        "FirstName": null,
        "LastName": null,
        "Language": null
    },
    "BaseUrl": "https://dev_2.ninjible-dev-sg.sitepapa.com/",
    "Version": 673,
    "Domains": [
        "dev_2.ninjible-dev-sg.sitepapa.com"
    ],
    "Host": "dev_2.ninjible-dev-sg.sitepapa.com"
}
```

#### 8. Cookie

> 获取或设置 cookie 值 , 返回值示例如下

``` json
k.cookie
{
    "Keys": [
        "_ga",
        "_ga_2GB21SEBRP",
        "_site_id_",
        "_site_culture",
        "_ga_FC5DZ0P2MF",
        "_site_version_"
    ],
    "Values": [
        "GA1.1.1370139942.1682245682",
        "GS1.1.1682245592.11.1.1682245706.0.0.0",
        "598a2176-dd5c-383d-70fe-bba727acc0d0",
        "nl",
        "GS1.1.1683597548.6.1.1683598186.0.0.0",
        "677"
    ]
}
```

!> k.cookie._site_culture 可以直接获取变量



## 后端常用

### 1.File

> 提供对站点文件夹下的文本或二进制文件的读写访问

### 2. Database

### 3. Sqlite

### 4. Mysql

### 5. SqlServer

### 6. Sql

> 动态选择的数据库
> 例子：
> 站点设置默认数据库=>mysql
> k.sql==k.mysql





# 未解释 或 不常用

- #### Net

- #### ViewData

- #### Dom

- #### WebSocket

- #### sms

- #### KeyValue

- #### User

- #### Account

- #### Module

- #### Community

- #### Logger

- #### Organization

- #### Version

- #### Template

- #### SiteDb

- #### Site

- #### Url

- #### config

- #### Settings

- #### event

- #### diagnosis

- #### DB

- #### Cache

- #### OpenApi

- #### Market

- #### Content

- #### Extension

- #### ex

- #### String

- #### Text

- #### Date

- #### Utils

- #### mail

- #### map

- #### Compression

- #### Xml

- #### Security

- #### WebUtility

- #### Office

- #### Mongo



## 案例

### 服务器执行的 script

```html
<script engine="kscript">
  // 服务器执行的node，可以访问到k对象
  let list = k.content.list.all();

  // console.log()  console is defined 无此对象
</script>
```

- k.import( ) 引入文件
- k.sqllit 访问 sqllit 数据库

  -

- k.response 设置返回体的信息
  - statusCode(code) 设置返回体的状态码
  - json() 参数为符合 json 格式的对象，会转为 json 格式
- k.mail 创建邮件对象？
  - createMessage 类似 form 对象，可以设置邮件的属性
    - from
    - to
    - subject
    - htmlBody
    - addAttachment
    - ......
  - smtp.send( ) 发送邮件
