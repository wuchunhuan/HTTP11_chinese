由于HTTP主要使用文本，字符分隔字段，解析器通常对于基于发送很长的流数据的攻击很弱势，尤其是实现期望一个未定义长度的协议元素。

为了促进互操作性，针对请求行（3.1.1节）和头字段（3.2节）的最小尺寸限制提出了具体建议。这些都是最低限度的建议，即使是资源有限的实施也是可以支持的。 预计大多数实现将选择更高的限制。

服务器可以拒绝一个请求目标过长(RFC7231的6.5.12节)或请求负载体过大（RFC7231的6.5.11节）的消息。与容量限制相关的额外状态码已经被HTTP扩展RFC6585定义。

收件人应该仔细限制他们处理其他协议元素的程度，包括（但不限于）请求方法，响应状态短语，头字段名称，数字值和主体块。未能限制这样的处理可能造成缓存溢出，算数溢出，或者增加拒绝服务攻击的漏洞。