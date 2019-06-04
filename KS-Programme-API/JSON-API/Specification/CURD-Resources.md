# Resource CURD
```md
服务器可能支持给定类型资源的创建，服务器也可能允许已存在资源的更新和删除。
服务器允许单次请求，更新多个资源，如下所述。多个资源更新必须完全成功或者失败，不允许部分更新成功。
任何包含内容的请求，必须包含Content-Type:application/vnd.api+json请求头。
```
## Creating Resources
```md
向表示待创建资源所属资源集的URL，发出POST请求，创建一个或多个资源。
请求必须包含单一资源对象作为主数据。
资源对象必须包含至少一个type成员。
```
* 新photo可以通过如下请求创建：
```json
POST /photos HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": {
    "type": "photos",
    "attributes": {
      "title": "Ember Hamster",
      "src": "http://example.com/images/productivity.png"
    },
    "relationships": {
      "photographer": {
        "data": { "type": "people", "id": "9" }
      }
    }
  }
}
```
```md
如果资源对象在relationships提供了关系,它的值必须是一个有data成员的关系对象。
这个键的值代表新资源将要有的连接。
```
### Client-Generated IDs
```md
服务器可能接受创建资源的请求中有客户端生成的ID。
ID必须被id键指定,它的值必须是通用唯一识别码。 
客户端应该使用 RGC4122 RGC4122中描述的合适的UUID。
```
```json
POST /photos HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": {
    "type": "photos",
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "attributes": {
      "title": "Ember Hamster",
      "src": "http://example.com/images/productivity.png"
    }
  }
}
```
```md
服务器必须对不支持的带有客户端生成ID的创建请求返回 403 Forbidden。
```
### Responses
* 201 Created
```md
如果POST请求不包括客户端生成的ID,并且请求的资源成功被创建,服务器必须返回201 Created状态码。
响应应该包含Location头，用以标示请求创建所有资源的位置。
响应必须含有一个文档，用以存储所创建的主要资源。

如果响应返回的资源对象在links成员里包含self键，
并且响应数据头提供了Location, 那么self的值必须匹配Location的值。
```
```json
HTTP/1.1 201 Created
Location: http://example.com/photos/550e8400-e29b-41d4-a716-446655440000
Content-Type: application/vnd.api+json

{
  "data": {
    "type": "photos",
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "attributes": {
      "title": "Ember Hamster",
      "src": "http://example.com/images/productivity.png"
    },
    "links": {
      "self": "http://example.com/photos/550e8400-e29b-41d4-a716-446655440000"
    }
  }
}
```
* 204 No Content
```md
如果POST请求包括客户端生成的ID，并且请求的资源成功被创建,那么服务器必须返回201 Created 状态码和响应文档(如上所述)
或者只返回204 No Content状态码，没有响应文档。
```
* 403 Forbidden
```md
服务器可能向不支持的创建资源的请求返回403 Forbidden的响应。
```
* 404 Not Found
```md
如果创建请求引用的相关资源不存在,服务器必须返回404 Not Found的响应。
```
* 409 Conflict
```md
如果创建请求中,客户端生成的ID已经存在,服务器必须返回409 Conflict的响应。
如果创建请求中,资源对象的type不在后端支持的类型里,服务器必须返回409 Conflict的响应。
服务器应该在响应中包括错误详情和足够的信息以识别冲突原因。
```
* Other Responses
```md
服务器响应可能没有状态码。
服务器可能响应包括错误详情的错误响应。
服务器与客户端必须依照HTTP的语义准备和解译响应。
```
## Updating Resources
```md
向表示资源的URL发出PATCH请求，即可进行资源更新。

资源的URL可以从资源对象的self的值获得。
或者,当GET请求返回了一个资源对象作为主资源, 同样的请求URL可被用来更新资源。

PATCH请求必须包括一个资源对象作为主资源。资源对象必须包含type和id成员。
```
```json
PATCH /articles/1 HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": {
    "type": "articles",
    "id": "1",
    "attributes": {
      "title": "To TDD or Not"
    }
  }
}
```
### Updating a Resource’s Attributes
* 下面的PATCH请求被解译为只更新title和text两个属性:
```json
PATCH /articles/1 HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": {
    "type": "articles",
    "id": "1",
    "attributes": {
      "title": "To TDD or Not",
      "text": "TLDR; It's complicated... but check your test coverage regardless."
    }
  }
}
```
### Updating a Resource’s Relationships
* 下面的PATCH请求将会更新author关联:
```json
PATCH /articles/1 HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": {
    "type": "articles",
    "id": "1",
    "relationships": {
      "author": {
        "data": { "type": "people", "id": "1" }
      }
    }
  }
}
```
### Responses
```md
202 Accepted 
如果服务器接受更新,但在服务器响应时更新并未完成,那么服务器必须返回202 Accepted状态码。

204 No Content
如果更新成功，且服务器没有更新任何未提供的属性，那么服务器必须或者返回204 No Content状态码和响应文档,
或者只返回204 No Content状态码,没有响应文档。

200 OK
如果服务器接受更新，但是在请求指定内容之外做了资源修改，
必须响应200 OK以及更新的资源实例，像是向此URL发出GET请求。

如果更新成功,客户端当前属性保持更新,并且服务器只响应最上层元数据,那么服务器必须返回200 OK状态码。
这种情况下,服务器不能包括更新后的资源。

其它响应
服务器使用其它HTTP错误状态码反映错误。 客户端必须依据HTTP规范处理这些错误信息。 
如下所述，错误细节可能会一并返回。
```
## Updating Relationships
### Updating To-One Relationships (更新 To-One 关联 )
```md
PATCH请求必须包括上层名为data的成员,包括:
相关新资源的资源表示对象
或者
null，用来删除关联。
```
* 下面的请求更新author关联:
```json
PATCH /articles/1/relationships/author HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": { "type": "people", "id": "12" }
}
```
* 下面的请求会清除author关联:
```json
PATCH /articles/1/relationships/author HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": null
}
```
```md
如果关联被成功更新,服务器必须返回一个成功的响应。
```
### Updating To-Many Relationships (更新 To-Many 关联)
```json
PATCH /articles/1/relationships/tags HTTP/1.1
Content-Type: application/vnd.api+json
Accept: application/vnd.api+json

{
  "data": [
    { "type": "tags", "id": "2" },
    { "type": "tags", "id": "3" }
  ]
}
```
### Responses
```md
202 Accepted
如果服务器接受关联更新请求,但在服务器响应时更新并未完成,那么服务器必须返回202 Accepted状态码。

204 No Content
如果更新成功，并且请求中的资源与结果相符，那么服务器必须或者返回204 No Content状态码。

200 OK
如果服务器接受更新,但用在请求指定以外的方式更改了目标关联,那么b必须返回200 OK响应。 
响应文档必须包括被更新关联的代表。
如果更新成功,客户端当前数据保持更新,并且服务器只响应最上层元数据,那么服务器必须返回200 OK状态码。
这种情况下,服务器不能包括更新后的资源。

403 OK
服务器必须向不支持的更新关联请求发出403 Forbidden响应。

其它响应
服务器可能使用其它HTTP错误状态码反映错误。
服务器可能响应包括错误详情的错误响应。
服务器与客户端必须依照HTTP的语义准备和解译响应。
```
## Deleting Resources
```md
向资源URL发出DELETE请求即可删除单个资源。
```
```http
DELETE /photos/1 HTTP/1.1
Accept: application/vnd.api+json
```
### Responses
```md
1. 202 Accepted
  如果删除资源的请求被接受处理,但在服务器响应时处理并未完成,那么服务器必须返回202 Accepted状态码。

2. 204 No Content
如果删除请求成功，服务器必须返回204 No Content 状态码,并且没有返回内容

3. 200 OK
  如果删除请求成功,服务器必须返回200 OK状态码,并且返回上层的元数据。

4. 404 NOT FOUND
  如果因为资源不存在,删除请求失败,那么服务器应该返回404 Not Found状态码。

5. 其它响应
  服务器可能使用其它HTTP错误状态码反映错误。
  服务器可能响应包括错误详情的错误响应。
  服务器与客户端必须依照HTTP的语义准备和解译响应。
```
