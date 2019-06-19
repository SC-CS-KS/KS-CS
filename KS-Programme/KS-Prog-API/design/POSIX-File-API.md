# POSIX File API
## 设计原则
```md
1. 提供清晰的思维模型 provides a good mental model
    一个API如何被使用，以及API本身如何被维护，是依赖于维护者和使用者能够对该API有清晰的、一致的认识。
2. 简单 “Make things as simple as possible, but no simpler.” 
3. 容许多个实现 allows multiple implementations
    一般来说，在讨论API设计时常常被提到的原则是解耦性原则或者说松耦合原则。
    然而相比于松耦合原则，这个原则更加有可操作性：如果一个API自身可以有多个__完全不同的实现__，
    一般来说这个API已经有了足够好的抽象，和自身的某一个具体实现无关，
    那么一般也不会出现和外部系统耦合过紧的问题。因此这个原则更本质一些。
```

## 最佳实践
### 想想优秀的API例子：POSIX File API
```md
整个最佳实践可以总结为一句话：“想想File API是怎么设计的。”
1. File API已经有几十年历史（从1988年算起将近40年），尽管期间硬件软件系统的发展经历了好几代，
    这套API核心保持了稳定。这是极其了不起的。
2. API提供了非常清晰的概念模型，每个人都能够很快理解这套API背后的基础概念：
    什么是文件，以及相关联的操作（open, close, read, write），清晰明了
3. 支持很多的不同文件系统实现，这些系统实现甚至于属于类型非常不同的设备，
    例如磁盘、块设备、管道（pipe）、共享内存、网络、终端terminal等等。
    所有不同的设备不同的文件系统实现都可以采用了同样的接口，
    使得上层系统不必关注底层实现的不同，这是这套API强大的生命力的表现。
```
### Document well 写详细的文档
### Carefully define the "resource" of your API 仔细的定义“资源”
```md
Resource资源本身是对一套API操作核心对象的一个抽象Abstraction。
例如对于文件的API，可以看出，文件File这个Resource（资源）的抽象，是“可以由一个字符串唯一标识的数据记录”。
这个定义去除了文件是如何标识的（这个问题留给了各个文件系统的具体实现），
也去除了关于如何存储的组织结构（again，留给了存储系统）细节。
```
### Choose the right level of abstraction 选择合适的抽象层
```md
是在定义对象时需要选择合适的Level of abstraction（抽象的层级）

以File API为例。在设计这样的API时，选择抽象的层级的可能的选项有多个，例如：
文本、图像混合对象
“数据块” 抽象
”文件“抽象

这些不同的层级的抽象方式，可能描述的是同一个东西，但是在概念上是不同层面的选择。
当设计一个API用于与数据访问的客户端交互时，“文件File“是更合适的抽象，
而设计一个API用于文件系统内部或者设备驱动时，数据块或者数据块设备可能是合适的抽象，
当设计一个文档编辑工具时，可能会用到“文本图像混合对象”这样的文件抽象层级。

又例如，数据库相关的API定义，底层的抽象可能针对的是数据的存储结构，
中间是数据库逻辑层需要定义数据交互的各种对象和协议，
而在展示（View layer）的时候需要的抽象又有不同
```
### Prefer using different model for different layers 不同层建议采用不同的数据模型
```md
强调强调的是不同层之间模型不同。

在服务化的架构下，数据对象在处理的过程中往往经历多层。
在这里我们的建议是不同的Layer采用不同的数据结构。
John Ousterhout 书里面则更直接强调：Different layer, different abstraction。

例如网络系统的7层模型，每一层有自己的协议和抽象，是个典型的例子。
而前面的文件API，则是一个Logic layer的模型，而不同的文件存储实现（文件系统实现），
则采用各自独立的模型（如快设备、内存文件系统、磁盘文件系统等各自有自己的存储实现API）。

当API设计倾向于不同的层采用一样的模型的时候，
可能意味着这个Service本身的职责没有定义清楚，是否功能应该下沉？

不同的层采用同样的数据结构带来的问题还在于API的演进和维护过程。
一个系统演进过程中可能需要替换掉后端的存储，可能因为性能优化的关系需要分离缓存等需求，
这时会发现将两个层的数据绑定一起（甚至有时候直接把前端的json存储在后端），会带来不必要的耦合而阻碍演进。
```
### Naming and identification of the resource 命名与标识
```md
API定义了一个资源对象，下面一般需要的是提供命名/标识(Naming and identification)。
在naming/ID方面，一般有两个选择（不是指系统内部的ID，而是会暴露给用户的）：
用free-form string作为ID（string nameAsId)
用结构化数据表达naming/ID

采用Free-form string的方式定义的命名，为系统的具体实现留下了最大的自由度。
带来的问题是命名的内在结构（如路径）本身并非API强制定义的一部分，转为变成实现细节。
如果命名本身存在结构，客户端需要有提取结构信息的逻辑。这是一个需要做的平衡。

例如文件API采用了free-form string作为文件名的标识方式，而文件的URL则是文件系统具体实现规定。
这样，就容许Windows操作系统采用"D:\Documents\File.jpg"而Linux采用"/etc/init.d/file.conf"这样的结构了。
而如果文件命名的数据结构定义为
{
   disk: string,
   path: string
}
这样结构化的方式，透出了"disk"和"path"两个部分的结构化数据，
那么这样的结构可能适应于Windows的文件组织方式，而不适应于其他文件系统，也就是说泄漏了实现细节。

如果资源Resource对象的抽象模型自然包含结构化的标识信息，则采用结构化方式会简化客户端与之交互的逻辑，强化概念模型。
这时牺牲掉标识的灵活度，换取其他方面的优势。例如，银行的转账账号设计，可以表达为
{
   account: number
   routing: number
}
这样一个结构化标识，由账号和银行间标识两部分组成，这样的设计含有一定的业务逻辑在内，
但是这部分业务逻辑是__被描述的系统内在逻辑而非实现细节__，
并且这样的设计可能有助于具体实现的简化以及避免一些非结构化的字符串标识带来的安全性问题等。
因此在这里结构化的标识可能更适合。

另一个相关的问题是，__何时应该提供一个数字unique ID?__ 这是一个经常遇到的问题。
有几个问题与之相关需要考虑：
是否已经有结构化或者字符串的标识可以唯一、稳定标识对象？如果已经有了，那么就不一定需要numerical ID；
64位整数范围够用吗？
数字ID可能不是那么用户友好，对于用户来讲数字的ID会有帮助吗？
如果这些问题都有答案而且不是什么阻碍，那么使用数字ID是可以的，__否则要慎用数字ID__。
```
### Conceptually what are the meaningful operations on this resource? 对于该对象来说，什么操作概念上是合理的？
```md
在确定下来了资源/对象以后，我们还需要定义哪些操作需要支持。这时，考虑的重点是“__概念上合理(Conceptually reasonable)__”。
换句话说，operation + resource 连在一起听起来自然而然合理
（如果Resource本身命名也比较准确的话。当然这个“如果命名准确”是个big if，非常不容易做到）。
操作并不总是CRUD（create, read, update, delete）。

例如，一个API的操作对象是额度（Quota)，那么下面的操作听上去就比较自然：
Update quota（更新额度），transfer quota（原子化的转移额度）
但是如果试图Create Quota，听上去就不那么自然，因额度这样一个概念似乎表达了一个数量，概念上不需要创建。
额外需要思考一下，这个对象是否真的需要创建？我们真正需要做的是什么？
```
### For update operations, prefer idempotency whenever feasible 更新操作，尽量保持幂等性
```md
Idempotency幂等性，指的是一种操作具备的性质，具有这种性质的操作可以被多次实施并且不会影响到初次实施的结果
“the property of certain operations in mathematics and computer science whereby they 
can be applied multiple times without changing the result beyond the initial application.”

很明显Idempotency在系统设计中会带来很多便利性，例如客户端可以更安全的重试，从而让复杂的流程实现更为简单。
但是Idempotency实现并不总是很容易。

1. Create类型的idempotency
    创建的Idempotency，多次调用容易出现重复创建，为实现幂等性，
    常见的做法是使用一个__client-side generated de-deduplication token（客户端生成的唯一ID）__，
    在反复重试时使用同一个Unique ID，便于服务端识别重复。
2. Update类型的Idempotency
    更新值(update）类型的API，应该避免采用"Delta"语义，以便于实现幂等性。
    对于更新类的操作，我们再简化为两类实现方式
    Incremental（数量增减），如IncrementBy(3)这样的语义
    SetNewTotal（设置新的总量）

    IncrementBy 这样的语义重试的时候难以避免出错，而SetNewTotal（3）（总量设置为x）语义则比较容易具备幂等性。
    当然在这个例子里面，也需要看到，IncrementBy也有有点，即多个客户请求同时增加的时候，比较容易并行处理，
    而SetTotal可能导致并行的更新相互覆盖（或者相互阻塞）。
    可以认为更新增量和设置新的总量这两种语义是不同的优缺点，需要根据场景来解决。
    如果必须优先考虑并发更新的情景，可以使用更新增量的语义，并辅助以Deduplication token解决幂等性。

3. Delete类型idempotency
    Delete的幂等性问题，往往在于一个对象被删除后，再次试图删除可能会由于数据无法被发现导致出错。
    这个行为一般来说也没什么问题，虽然严格意义上不幂等，但是也无副作用。
    如果需要实现Idempotency，系统也采用了Archive->Purge生命周期的方式分步删除，或者持久化Purge log的方式，都能支持幂等删除的实现。
```
### Compatibility 兼容
```md
API的变更需要兼容，兼容，兼容！重要的事情说三遍。
这里的兼容指的是向后兼容，而兼容的定义是不会Break客户端的使用，
也即__老的客户端能否正常访问服务端的新版本（如果是同一个大版本下）不会有错误的行为__。
这一点对于远程的API（HTTP/RPC）尤其重要。

常见的__不兼容__变化包括（但不限于）:
删除一个方法、字段或者enum的数值
方法、字段改名
方法名称字段不改，但是语义和行为的变化，也是不兼容的。这类比较容易被忽视。
```
### Batch mutations 批量更新
```md
批量更新如何设计是另一个常见的API设计决策。这里我们常见有两种模式：
客户端批量更新，或者服务端实现批量更新。

API的设计者可能会希望实现一个服务端的批量更新能力，但是我们建议要尽量避免这样做。
__除非对于客户来说提供原子化+事务性的批量很有意义（all-or-nothing）__，
否则实现服务端的批量更新有诸多的弊端，而客户端批量更新则有优势：
服务端批量更新带来了API语义和实现上的复杂度。例如当部分更新成功时的语义、状态表达等
即使我们希望支持批量事物，也要考虑到是否不同的后端实现都能支持事务性
批量更新往往给服务端性能带来很大挑战，也容易被客户端滥用接口
在客户端实现批量，可以更好的将负载由不同的服务端来承担（见图）
客户端批量可以更灵活的由客户端决定失败重试策略
```
### Be aware of the risks in full replace 警惕全体替换更新模式的风险
```md
所谓Full replacement更新，是指在Mutation API中，用一个全新的Object/Resource去替换老的Object/Resource的模式。
API写出来大概是这样的: UpdateFoo(Foo newFoo);
这是非常常见的Mutation设计模式。但是这样的模式有一些潜在的风险作为API设计者必须了解。

使用Full replacement的时候，更新对象Foo在服务端可能已经有了新的成员，而客户端尚未更新并不知道该新成员。
服务端增加一个新的成员一般来说是兼容的变更，但是，如果该成员之前被另一个知道这个成员的client设置了值，
而这时一个不知道这个成员的client来做full-replace，该成员可能就会被覆盖。

更安全的更新方式是采用Update mask，也即在API设计中引入明确的参数指明哪些成员应该被更新。
UpdateFoo {
  Foo newFoo; 
  boolen update_field1; // update mask
  boolen update_field2; // update mask
}
或者update mask可以用repeated "a.b.c.d“这样方式来表达。

不过由于这样的API方式维护和代码实现都复杂一些，采用这样模式的API并不多。
所以，本节的标题是“be aware of the risk“，而不是要求一定要用update mask。
```
### Don't create your own error codes or error mechanism 不要试图创建自己的错误码和返回错误机制
```md
API的设计者有时很想创建自己的Error code，或者是表达返回错误的不同机制，
因为每个API都有很多的细节的信息，设计者想表达出来并返回给用户，想着“用户可能会用到”。
但是事实上，这么做经常只会使API变得更复杂更难用。

Error-handling是用户使用API非常重要的部分。为了让用户更容易的使用API，
最佳的实践应该是用标准、统一的Error Code，而不是每个API自己去创立一套。
例如HTTP有规范的error code，Google Could API设计时都采用统一的Error code等【2】。
```
* 为什么不建议自己创建Error code机制？
```md
1. Error-handling是客户端的事，而对于客户端来说，是很难关注到那么多错误的细节的，一般来说最多分两三种情况处理。
    往往客户端最关心的是"这个error是否应该重试(retryable)"还是应该继续向上层返回错误，而不是试图区分不同的error细节。
    这时多样的错误代码机制只会让处理变得复杂
2. 有人觉得提供更多的自定义的error code有助于传递信息，但是这些信息除非有系统分别处理才有意义。
    如果只是传递信息的话，error message里面的字段可以达到同样的效果。
```
## Reference
* 1. [阿里研究员谷朴：API 设计最佳实践的思考](https://yq.aliyun.com/articles/683044)
* 2. [API Design patterns for Google Cloud](https://cloud.google.com/apis/design/design_patterns)
* [API design best practices](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design?spm=a2c4e.11153940.blogcont683044.11.391b7163skKKNU)
