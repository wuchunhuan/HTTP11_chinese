已存HTTP客户端和用户代理一般无限期的保留认证信息。HTTP不为源服务器提供将客户端导向丢弃这些缓存凭证的的机制，因为协议无法感知用户代理是如何获取或管理这些凭证的。对过期或撤销凭证的机制可以作为认证方案定义的一部分被指明。

凭证缓存影响应用程序安全模式的情况包括但不限于：

- 空闲一段时间的客户端，服务器可能希望客户端重新提示用户输入凭据。
- 包含会话终止指示（例如页面上的“注销”或“提交”按钮）的应用程序，应用程序的服务器端在此之后“知道”客户端没有更多理由保留凭证。

缓存凭证的用户代理被鼓励提供一个易于访问的机制来丢弃用户控制下的缓存证书。