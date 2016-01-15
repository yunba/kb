## Portal

Portal，即 “门户”。云巴的 Portal 是用户应用的管理入口，后端连接着云巴的实时消息系统。

用户在云巴官网注册并登录后，可以通过点击页面右上方的用户名进入 Portal 页面。 
通过云巴的 Portal 页面，可以创建和管理应用、发布消息、查看统计信息，还可以查看通过 Portal 发布过的消息的历史记录。

常有客户疑惑，为什么只有一个设备在线时，Portal 的在线用户统计数量却是 2 ？原因很简单，Portal 也同时是一个 [JavaScript](https://github.com/yunba/yunba-javascript-sdk) 客户端，可以向指定应用（[AppKey](https://github.com/yunba/kb/blob/master/AppKey.md)）的指定 Topic 发布消息，因此会算在统计内。
