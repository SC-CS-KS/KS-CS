# Fetching Data
```md
数据包括资源和关联，可以通过向后端发送GET请求获取数据。
响应可以通过以下描述的可选特征进一步提取。
```
## Fetching Resources
```md
服务器必须支持通过URL获取资源，URL可以通过以下形式提供：
top-level链接对象中的self链接.
resource-level链接对象中的self链接.
relationship-level链接对象中的related链接.
```
```http
以下请求获取一个文献集合：
GET /articles HTTP/1.1
Accept: application/vnd.api+json

以下请求获取一篇文献：
GET /articles/1 HTTP/1.1
Accept: application/vnd.api+json

以下请求获取一篇文献的作者:
GET /articles/1/author HTTP/1.1
Accept: application/vnd.api+json
```
### Responses

## Fetching Relationships
### Responses
```md
服务器必须支持通过关联URL获取关联数据，关联URL可以通过关联的links对象中的self链接提供。
```
```http
1. 以下请求获取文献的评论数据:
GET /articles/1/relationships/comments HTTP/1.1
Accept: application/vnd.api+json

2. 以下请求获取文献的作者数据:
GET /articles/1/relationships/author HTTP/1.1
Accept: application/vnd.api+json
```
## Inclusion of Related Resources (内联资源)
```md
后端可以默认回复与主数据相关的资源。
后端也可以支持include请求参数以保证客户端可以指定需要回复的相关资源。

如果后端不支持include参数，必须以400 Bad Request状态码回复任何包含此参数的请求。
如果后端支持include参数并且客户端使用了此参数，服务器不能在复合文档的included部分包含任何未请求的资源对象。

include参数的值必须是一个由逗号分隔符(U+002C COMMA, “,”) 分割的关联路径列表。
关联路径是由点号分隔符(U+002E FULL-STOP, “.”) 分割的关联名称。

如果服务器不能识别关联路径或不能通过路径支持内联资源，必须以400 Bad Request状态码回复。
```
* 可以同时请求评论和文献:
```http
GET /articles/1?include=comments HTTP/1.1
Accept: application/vnd.api+json
```
* 可以通过如下形式为每个关联名称定义逗号分割路径，以请求与其他资源相关的资源：
```http
GET /articles/1?include=comments.author HTTP/1.1
Accept: application/vnd.api+json
```
* 可以通过逗号分割列表请求多个相关资源:
```http
GET /articles/1?include=author,comments.author HTTP/1.1
Accept: application/vnd.api+json
```
* 可以向关联后端请求相关资源:
```http
GET /articles/1/relationships/comments?include=comments.author HTTP/1.1
Accept: application/vnd.api+json
```
```md
在这种情况下，主数据应该是代表此文献的评论连接的资源标识符对象集合，所有评论和评论作者将会作为相关数据返回。
```
## Sparse Fieldsets (稀疏字段组)
```md
客户端可能通过fields[TYPE]参数,请求后端返回只包含特定字段的响应。
fields参数的值必须用逗号分隔开,用来表示需要返回字段的名称。

如果客户端请求了一组给定类型的字段,那么后端不能包括资源对象内此类型的附加字段。
```
```http
GET /articles?include=author&fields[articles]=title,body&fields[people]=name HTTP/1.1
Accept: application/vnd.api+json
```
## Sorting
```md
服务器可以选择性支持，根据一个或多个条件(排序字段)对资源集合排序。
后端可能支持带有sort查询参数的请求,来排序主要数据。
sort的值必须代表排序字段。
```
```http
GET /people?sort=age HTTP/1.1
Accept: application/vnd.api+json
```
```md
后端可能支持带有多个排序字段的请求,允许用逗号分隔排序字段。
排序字段应该被按照特定顺序执行。
```
```http
GET /people?sort=age,name HTTP/1.1
Accept: application/vnd.api+json
```
```md
每个排序字段必须按升序排列。除非它带有-前缀,这种情况下将按降序排列。
```
```http
GET /articles?sort=-created,title HTTP/1.1
Accept: application/vnd.api+json
```
```md
以上的例子应首先返回最新的条目。在同一天创建的条目讲按照标题的字母升序排列。
```
```md
如果服务器不支持查询参数sort指定的排序,必须返回400 Bad Request。
如果服务器支持排序,并且客户端通过查询参数sort进行排序,
服务器必须返回根据指定条件排序的, 上层data数组的元素。
```
## Pagination
```md
服务器可以选择性限制响应返回的资源数量,为所有可获取资源的子集("page")。
服务器可以提供传送分页后数据集的连接("pagination links")。
pagination links必须出现在集合相关的连接对象中。需要在上层links对象中提供pagination links。
```
* 下面的键必须被用于pagination links ：
```md
first: the first page of data
last: the last page of data
prev: the previous page of data
next: the next page of data
```
```md
如需表示特定的连接不可用，这些键必须被省略,或者值为null。
分页的排序，必须与JSON API的排序规则一致。
查询参数page是分页的保留字，服务器和客户端应该用这个参数进行分页。
```
## Filtering
```md
查询参数filter是过滤的保留字，服务器和客户端应该用这个参数进行过滤。
```