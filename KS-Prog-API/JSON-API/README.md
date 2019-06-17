# JSON API

## What is JSON-API

## [Specification](https://jsonapi.org/format/)
* [Document Structure](Specification/Document-Structure.md)
* [Fetching Data](Specification/Fetching-Data.md)
* [Creating, Updating and Deleting Resources](CURD-Resources.md)
* Query Parameters
```md
查询参数必须遵守成员命名的规则，同时必须包含至少一个非a-z字符(U+0061 to U+007A)。
推荐使用 U+002D HYPHEN-MINUS, “-“, U+005F LOW LINE, “_”, 或者大写字母(如: camelCasing)。

如果服务器获取到不遵从以上命名规则的查询参数，并且不知道如何处理，那么服务器必须返回 400 Bad Request。
```
* [Errors](Specification/Errors.md)

## [Implementations](https://jsonapi.org/implementations/#server-libraries-net)
### Client libraries
### Server libraries

## [Design](https://jsonapi.org/recommendations/)

## Reference
* [用 JSON 构建 API 的标准指南](https://github.com/justjavac/json-api-zh_CN)