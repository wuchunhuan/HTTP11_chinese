TRACE方法请求一个远端的，应用层的，环回的请求消息。请求的最终接收者**应该**反映消息被接收到，除了下面描述的一些字段，以一个带有Content-Type为“message/http”（RFC7230，8.3.1节）的200（成功）响应的消息体回到客户端。最终的接收者时源服务器或第一个在请求中接收到Max-Forwards值为0的服务器（5.1.2节）。

客户端**不得**子啊TRACE请求中生成包含可能被响应泄露的敏感数据的头字段。例如，用户代理在TRACE请求中发送存储的用户证书（RFC7235）或cookies（RFC6265）是愚蠢的。请求的最终接收者在生成响应体的时候**应该**排除任何可能包含敏感数据的请求头字段。

TRACE允许客户端查看在请求链的另一端被接收到的内容并且使用这个数据来测试或信息诊断。Via头字段（RFC7230，5.7.1节）需要特别关注，因为它作为请求链的跟踪。使用Max-Forwards头字段允许客户端限制请求链的长度，这对于测试代理在一个无穷循环中转发消息是游泳的。

客户端**不得**在TRACE请求中发送消息主体。

TRACE方法的响应不可被缓存。