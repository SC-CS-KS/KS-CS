# [Document Structure](https://jsonapi.org/format/#document-structure)

## [Top Level](http://jsonapi.org.cn/format/)
```md
JSON 对象必须位于每个JSON API文档的根级。
```
* 文档必须包含以下至少一种top-level键：
```md
data: 文档的”primary data”
errors: 错误对象列表
meta: 包含非标准元信息的元对象

data键和errors键不能再一个文档中同时存在。
```
* 文档可能包含以下任何top-level键：
```md
jsonapi: 描述服务器实现的对象
links: 与primary data相关的链接对象
include: 与primary data或其他资源相关的资源对象("included resources")列表

如果文档不包含top-level data键，included键也不应该出现。
```
* 文档的top-level 链接对象可能包含以下键：
```md
self: 生成当前响应文档的链接
related: 当primary data代表资源关系时，表示相关资源链接
Primary data 的分页链接

文档中的“primary data”代表一个请求所要求的资源或资源集合。
```
* Primary data 必须是以下列举的一种
```md
如果请求要求单一资源，应该是一个单一资源对象，或一个单一资源标识符，或null
如果请求要求资源集合，应该是一个资源对象列表，或一个空列表([])
```
## Resource Objects (资源对象)
```md
JSON API 文档中的"Resuorce objects"代表资源。
```
* 一个资源对象必须至少包含以下top-level键：
```md
id
type

例外：当资源对象来自客户端并且代表一个将要在服务器创建的新资源时，id键不是必须的。
```
* 资源对象可能包含以下top-level键：
```md
'attribute': 属性对象代表资源的某些数据
relationshiops: 关联对象描述该资源与其他JSON API资源之间的关系
links: 链接资源包含与资源相关的链接
meta: 元数据资源包含与资源对象相关的非标准元信息，这些信息不能被作为属性或关联对象表示
```
* 一篇文献(即一个"文献"类型的资源)在文档中这样表示:
```json
{
  "type": "articles",
  "id": "1",
  "attributes": {
    "title": "Rails is Omakase"
  },
  "relationships": {
    "author": {
      "links": {
        "self": "/articles/1/relationships/author",
        "related": "/articles/1/author"
      },
      "data": { "type": "people", "id": "9" }
    }
  }
}
```
### Identification （标识符）
```md
每个资源对象包含一个id键和一个type键。
id键和type键的值必须是字符串类型。

对于每一个既定API，每个资源对象的type和id对必须定义一个单独且唯一的资源。
(由一个或多个但行为表现为一个服务器的服务器控制的URI集合构成一个API。)

type键用于描述共享相同属性和关联的资源对象。
type键的值必须与遵循键名称相同的约束条件。
```
### fields (字段)
```md
资源对象的属性和关联被统称为"fields"。

一个资源对象的所有字段必须与type和id在同一命名空间中。
即一个资源不能拥有名字相同的属性与关联，也不能拥有被命名为type或id的属性和关联。
```
### attribute (属性)
```md
attribute键的值必须是一个对象(一个"attributes object")。
属性对象的键("attributes")代表与资源对象中定义的与其有关的信息。

属性可以包含任何合法JSON值。

JSON对象和列表涉及的复杂数据结构可以作为属性的值。
但是一个组成或被包含于属性中的对象不能包含relationships或links键，
因为这些键为此规范未来的用途所预留。

虽然一些has-one关系的外键(例如author_id)被在内部与其他将要在资源对象中表达的信息一起储存，
但是这些键不能作为属性出现。
```
### relationships（关联）
```md
relationships键的值必须是一个对象("relationships object")。

关联对象("relationships")的键表示在资源对象中定义的与其相关的其他资源对象。
关联可以是单对象关联或多对象关联。
```
* 一个"relationship object"必须包含以下至少一种键：
```md
links: 一个链接对象至少包含以下一种键：
    self: 指向关联本身的链接("relationship link")。此链接允许客户端直接修改关联。
    例如，通过一个articale的关联URL移除一个author将会解除一个人与article的关系而不需要删除这个people资源本身。
    获取成功后，这个链接将返回一个相关资源之间的连接，将其作为primary data。(见 获取关联).
related: 相关资源链接.
data: 资源连接.
meta: 包含关于此关联的非标准元信息的元对象.

一个代表多对象关联的关联对象可能在links键下也包含分页链接
```
### Related Resource Links
```md
"related resource link"提供 关联中链接的资源对象的权限。
当获取成功后，相关资源对象将作为响应的primary data返回。

例如，通过一个GET请求检索时，一篇article的comments关联可以指定一个返回评论集合资源对象的链接。

当一个相关资源链接出现时，它必须指向一个合法URL， 即使关联当前不予任何目标资源相关。
此外，一个相关资源链接不能因为它的关联内容更改而更改。
```
### Resource Linkage
```md
复合文档中的资源连接允许客户端将所有包含的资源对象链接在一起，而不需要通过链接GET任何URL。
```
* 资源连接必须通过以下一种形式表述：
```md
空的单对象关联用null表示.
空的多对象关联用一个空列表([])表示.
非空单对象关联用一个资源标识符对象表示.
非空多对象关联用一个资源标识符对象列表表示
```
* 例如，以下文献与author相关：
```json
{
  "type": "articles",
  "id": "1",
  "attributes": {
    "title": "Rails is Omakase"
  },
  "links": {
    "self": "http://example.com/articles/1"
  }
}
```
### Resource Links
```md
资源对象中的可选的links键包含与资源相关的链接。
当链接对象存在时，它可能包含指向定义了资源对象所表示的资源的self链接。
```
```json
{
  "type": "articles",
  "id": "1",
  "attributes": {
    "title": "Rails is Omakase"
  },
  "links": {
    "self": "http://example.com/articles/1"
  }
}
```
```md
服务器收到一个特定URL的GET请求后，必须回复将此资源作为promary data的响应。
```
## Resource Identifier Objects (资源标识符对象)
```md
“resource identifier object”是一个定义单独资源的对象。
“resource identifier object”必须包含type和id键。
“resource identifier object”也可能包含meta键，它的值是包含非标准元信息的meta对象。
```
## Compound Documents (复合文档)
```md
为了减少HTTP请求的数量，服务器可能允许包含相关资源与所请求的主要资源的响应。
这种响应被称作"compound documents"。

在复合文档中，所有包含的资源必须以一个top-level中的included键中的资源对象列表表示。

复合文档要求 “full linkage”，这意味着所有包含其中的资源必须至少被一个在同一文档中的资源标识符对象定义。
这些资源标识符对象可以是primary data或与主要或相关资源包含在一起的资源连接。

全连接要求唯一的例外是当包含连接数据的关联字段被通过稀疏字段集合排除时。

对于每个typy和id对，一个复合文档不能包含超过一个资源对象。
```
## Meta Information (元信息)
```md
在指定位置，meta键可用于包含非标准元信息。每个meta键的值必须是一个对象("meta object")。
任何键都可以包含在meta对象中。
```
```json
{
  "meta": {
    "copyright": "Copyright 2015 Example Corp.",
    "authors": [
      "Yehuda Katz",
      "Steve Klabnik",
      "Dan Gebhardt",
      "Tyler Kellen"
    ]
  },
  "data": {
    // ...
  }
}
```
## Links (链接)
```md
在指定位置，links键可用于表示链接。每个links键的值必须是一个对象("links object")。
每个链接对象的键是一个"link"。
```
* 一个链接必须是以下形其中之一：
```md
1. 一个包含链接的URL的字符串.
2. 一个可以包含以下键的对象("link object"):
  href: 一个包含此链接URL的字符串
  meta: 包含与此链接相关非标准元信息的元对象
```
* 以下self链接是一个简单的URL:
```json
"links": {
  "self": "http://example.com/posts"
}
```
* 以下related链接包含一个URL和与资源集合相关的元信息：
```json
"links": {
  "related": {
    "href": "http://example.com/articles/1/comments",
    "meta": {
      "count": 10
    }
  }
}
```
## JSON:API Object (JSON API 对象)
```md
一个JSON API文档可能在top level jsonapi键下包含与其实现相关的信息。
如果它出现，jsonapi键的值必须是一个对象("jsonapi object")。
jsonapi对象可能包含version键，其值是一个表明被支持的最高JSON API版本的字符串。
此对象也可能包含一个meta键，其值是一个包含非标准元信息的meta对象。
```
```json
{
  "jsonapi": {
    "version": "1.0"
  }
}
```

## 
* [Member Names](https://jsonapi.org/format/#document-member-names)