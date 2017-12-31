被动协商（又称为，客户端驱动协商），最好的响应表示的选择是由客户端初始响应（而不管状态码）之后执行的，这个响应从源服务器接受，包含一个资源可选表示的列表。如果初始响应表示不满足用户代理，则可以对基于包含在列表中的元数据选择的一个或多个替代资源执行GET请求，以获得该响应的不同表示形式。替代的选择可能被用户代理自动的执行或者被用户从一个生成的（可能是超文本）菜单中选择手动执行。

注意上面个提到的响应的表示，通常不是资源的表示。如果提供这些备选方案的响应具有作为目标资源的表示的语义（例如，对GET请求的200（OK）响应），或者具有如下语义，则备选表示仅被认为是目标资源的表示 提供到目标资源的替代表示的链接（例如，对GET请求的300（多个选择）响应）。

服务器可以选择不发送初始表示，而不是替代列表，并且由此指示由用户代理进行的被动协商是优选的。例如，在300（多种选择）和406（不可接受）状态码的响应中列出的替代包含了可用表示的信息，所以用户或者用户代理可以通过做一个选择来做出回应。

当响应会随着常用维度（如类型，语言或编码）而变化时，当源服务器不能通过检查请求确定用户代理的能力，以及通常当公共缓缓被用于分担服务器负载和减少网络使用的时候，被动协商是有利的。

被动协商的缺点是向用户代理发送替代列表，如果在报头部分中传输，会降低用户感知的延迟，并且需要第二个请求来获得替代表示。此外，本协议没有定义自动选择的机制，但是它也没有阻止这种机制被作为一个扩展开发。