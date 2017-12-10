“Connection”头字段允许发送者表示对当前连接所期望的控制选项。为了避免迷惑下游接收者，代理或者网关**必须**在转发消息前移除或者取代替换任何接收到的连接选项。

当一个除了Connection的头字段被用来提供对当前连接的控制信息，发送者**必须**在Connection头字段中列出对应的字段名。代理或网关必须在转发消息之前解析接收到的Connection头字段，并且对于该字段中的每个连接选项，从消息中删除具有与连接选项相同名称的任何头字段，然后删除 Connection头域本身（或者用中介自己的转发消息的连接选项替换它）。

因此，Connection头字段提供了一种声明方式，用于区分仅用于直接收件人的头字段（“逐跳”）和那些打算送给链上所有收件人的字段（“端到端” “），使消息能够自我描述，并允许部署未来特定于连接的扩展，而不用担心老的中介会盲目地转发这些扩展。

Connection头字段的值有下列语法：

> ```
>      Connection        = 1#connection-option
>      connection-option = token
> ```

连接选项是不区分大小写的。

一个发送者不能发送一个连接选项，该连接选项对应于一个用于所有有效负载接收者的头域。例如，Cache-Control永远都不会被视为一个合适的连接选项（RFC7234的5.2节）。

连接选项并不总是对应于消息中的一个头字段的出现，因为如果没有与连接选项关联的参数，则可能不需要连接特定的头字段。相反，一个连接特定的头字段接受时没有对应的连接选项通常意味着字段已经被一个中介不当的转发并且应该被接收者忽略。

当定义新的连接选项时，规范的作者应该调查已有的头字段名并确保新的连接选项没有与已经部署的头字段使用相同的名称。定义一个新的连接选项基本上保留了用于携带与连接选项相关的附加信息的潜在字段名称，因为发送者将该字段名称用于其他任何事情是不明智的。

“close”连接选项被定义为发送者用于表明连接将在响应完成后被关闭。例如`Connection: close`在请求或响应中都表明发送者将要在当前请求/响应完成（6.6节）后关闭连接。

不支持保持连接的客户端**必须**在每个请求消息中发送“close”连接选项。

不支持保持连接的服务器**必须**在每个不是1xx（信息）状态码的响应消息中发送“close”连接选项。