#RESTFUL API风格规范
&emsp;具象状态传输（英文：Representational State Transfer，简称REST）是Roy Thomas Fielding博士于2000年在他的博士论文["Architectural Styles and the Design of Network-based Software Architectures"](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) 中提出来的一种万维网软件架构风格。（[wiki百科](https://zh.wikipedia.org/wiki/REST)）
+++
######统一接口（Uniform Interface）
GET:从服务器取出一项或多项资源（select）
POST：新建一项或多项资源（create）
PUT：更新服务器的资源（update）Client提供完整的更新后的数据
PATCH：更新服务器的资源（update）Clinet只提供需要更新的数据
DELETE：删除服务器资源（delete）
+++
状态码
200 GET/PUT/PATCH ok 获取成功 返回对应的数据
201 POST/PUT/PATCH created 创建或更新成功 返回创建的数据
204 DETELE no content  删除成功 不返回数据
400 POST/PUT/PATCH invalid request Client提供了不正确的数据
401 unauthorized 未授权。
403 forbidden 鉴权成功，但是该用户没有权限。
404 not found 请求了不存在的内容
500 internal server error 服务器内部错误
1XX 底层HTTP功能，一般不用
2XX 成功就发给Client
3XX 重定向
4XX 客户端请求错误，请求不存在的资源或没权限
5XX 服务端错误
+++
1，Url区分大小写
2，url以/结尾，不以/结尾会从定向到/结尾
3，用-不用_分割url单词
+++
1，API要包含版本信息，可以将版本信息放到url中
比如：/api/v20160910/names/
2，使用名词，不用动词来语义化API
比如：不好：/api/v20160910/getNames/
好：/api/v20160910/Names/
3，不要把url参数写到api里，不好	/api/v20160910/Names？openid=“asdsadasdasads”
4，可以用url参数对资源进行过滤。
######无状态 Statelessness 
对每个资源的请求，都不依赖其他资源，也不依赖其他请求
每个资源都有至少一个uri能对其定位,这个定位与其他资源无关，不会因为其他资源的变化而变化
######可缓存 Cacheable 
响应内容可以在通信链的某处被缓存，以提升性能。
######客户-服务器 Client-Server
通信表现为request-response的形式，只能由Client单方面发起。
######分层系统 Layered System
通过限制组件的行为，每个组件只能“看到”与其交互的紧邻层，将架构分解为若干等级的层
######按需代码（可选） Code on Demand (optional)
支持通过下载并执行一些代码，对Client的功能进行扩展
