## 属性列表


### 1-20
#### 1. DataContext

>  kview引擎的dataContext，kooboo的html渲染引擎。您可以将值显式设置到datacontext中，或者只将值声明为JS全局变量，它将可以从kview引擎访问。

#### 2. Response

> 用于将数据设置为HTTP resposne流的HTTP响应对象

#### 3. Request

> 访问http请求数据、查询字符串、表单或标头。Cookie可从k.Cookie获取。
> var值=k.request.queryname；
> var值=k.request.queryString.queryname；
> var值=k.request.form.queryname；

#### 4. Net
#### 5. InlineEditor
#### 6. Module
#### 7. ClientJS

> 将对象发送到浏览器JavaScript

#### 8. Community

> 与公众共享项目

#### 9. Session

> 用于小型交互式信息的临时存储器。会话不持续
> k.session.set（“key”，obj）；
> var back=k.session.get（“key”）；
> k.session.newkey=“值”；

#### 10. Dom

> 文档对象模型

#### 11. WebSocket

> WebSocket服务

#### 12. sms

> 发送短信通知

#### 13. ViewData

> 共享当前上下文存储

#### 14. Info

> 访问当前请求信息

#### 15. User
#### 16. Account
#### 17. Logger
#### 18. Organization
#### 19. Version

> 将版本nr附加到图像url以进行缓存。仅当系统设置为映像版本缓存时有效

#### 20. Template

### 21-40
#### 21. Cache
#### 22. SiteDb
#### 23. Site

> 具有版本控制的Kooboo网站数据库

#### 24. Url
#### 25. File

> 提供对站点文件夹下的文本或二进制文件的读写访问

#### 26. Cookie

> 获取或设置cookie值

#### 27. config
#### 28. Settings
#### 29. event
#### 30. diagnosis
#### 31. DB
#### 32. Task
#### 33. KeyValue

> 数据库键值存储

#### 34. Database
#### 35. Sqlite
#### 36. Mysql
#### 37. SqlServer
#### 38. Sql

> 动态选择的数据库
> 例子：
> 站点设置默认数据库=>mysql
> k.sql==k.mysql

#### 39. Mongo
#### 40. Api

### 41-60
#### 41. OpenApi
#### 42. Market
#### 43. Content
#### 44. Extension
#### 45. ex
#### 46. String
#### 47. Text
#### 48. Date

> Date对象,有format方法

#### 49. Utils
#### 50. mail
#### 51. map
#### 52. Compression
#### 53. Xml
#### 54. Security

> 单向和双向加密

#### 55. WebUtility
#### 56. Office

> office操作
> 例如:excel

## 

## 服务器执行的script

```html
<script engine="kscript">
    // 服务器执行的node，可以访问到k对象
    let list = k.content.list.all()

    // console.log()  console is defined 无此对象
</script>
```


- k.import( ) 引入文件
- k.sqllit 访问sqllit数据库
  - 

- k.response 设置返回体的信息
  - statusCode(code)  设置返回体的状态码
  - json() 参数为符合json格式的对象，会转为json格式 
- k.mail 创建邮件对象？
  - createMessage 类似form对象，可以设置邮件的属性
    - from 
    - to
    - subject
    - htmlBody
    - addAttachment
    - ......
  - smtp.send( )  发送邮件