“If-Modified-Since”头字段使GET或HEAD请求方法以所选择的表示的修改日期为条件，比在字段值中提供的日期更新。如果数据没有改变，则避免传送选定的表示数据。

> ```
>      If-Modified-Since = HTTP-date
> ```

字段的一个例子：

```
    If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT
```

如果请求包含一个If-None-Match头字段，接收者**必须**忽略If-Modified-Since；在If-None-Match中的条件被视为比If-Modified-Since中的条件更准确的替代，并且他们两个结合只是为了与没有实现If-None-Match的老旧中介的互操作。

如果被接受的字段不是要给有效的HTTP-date，或者如果请求方法不是GET或HEAD，接收者**必须**忽略If-Modified-Since头字段。

接收者**必须**根据源服务器的时钟来解释If-Modified-Since字段值的时间戳。

If-Modified-Since一般被用于两个目的：1. 允许高效的更新一个被缓存的表示，这个表示没有实体标签；2. 限制网页遍历最近被改变过的资源的范围

当用于缓存更新时，缓存一般将会使用被缓存消息的Last-Modified字段的值来生成If-Modified-Since的值。这个行为在的时钟同步很差或服务器已经选择只尊重确切的时间戳匹配的时候是最具互操作性的（由于Last-Modified日期出现问题，当源服务器的时钟被更正或从归档备份中恢复表示）。然而，缓存偶尔基于其他数据生成了字段值，如基于被缓存消息或消息被接收到时的本地时钟时间的Date头字段，特别是当缓存消息没有包含Last-Modified字段时。

“If-Unmodified-Since”头字段使得请求方法以所选表示的最后修改日期早于或等于字段值中提供的日期为条件。这个字段在用户代理没有表示的实体标签的情况下完成了与If-Match相同的目的。

> ```
>      If-Unmodified-Since = HTTP-date
> ```

字段的一个例子：

> ```
>      If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT
> ```

如果亲求包含If-Match头字段，接收者**必须**忽略If-Unmodified-Since；If-Match中的条件被视为比If-Unmodified-Since中的条件更准确的替代，并且二者的结合只是为了可能没有实现If-Match的老旧中介的互操作性。

如果接收者接收到的字段值不是有效的HTTP-date，它**必须**忽略If-Unmodified-Since。

接收者**必须**按源服务器的时钟来解释If-Unmodified-Since字段值的时间戳。

If-Unmodified-Since最长被用于状态改变方法（如POST，PUT，DELETE）以阻止当多个用户代理并行的操作一个没有提供表示的实体标签的资源时意外的复写（即，阻止“更新丢失”问题）。如果被选择表示不匹配任何已经在先前的请求中缓存（或部分缓存）的表示，它也可以用于安全方法以中断请求。

接收到If-Unmodified-Since头字段的源服务器在执行方法前**必须**评估条件（第5节）。源服务器**不得**在被选表示的最后修改日志被字段值提供的日期更接近当前的时候执行被请求的方法；作为替代源服务器**必须**响应412状态码或者如果源服务器已经确定状态改变正被请求并且最终状态已经反映到目标资源的当前状态时响应2xx状态码（即，用户代理请求的改变已经成功，但是用户代理没有意识到，因为先前的响应消息丢失了或者其他用户代理进行了兼容的改变）。在后一种情况中，源服务器**不得**在响应中发送校验器头字段，除非它可以确认请求是由相同用户代理发出的前一个改变的重复。

If-Unmodified-Since头字段会被缓存和中介忽略，因为它不适用于缓存响应。