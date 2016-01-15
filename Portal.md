## Portal

### 功能
Portal，即 “门户”。云巴的 Portal 是用户应用的管理入口，后端连接着云巴的实时消息系统。

用户在云巴官网注册并登录后，可以通过点击页面右上方的用户名进入 Portal 页面。 
通过云巴的 Portal 页面，可以创建和管理应用、发布消息、查看统计信息，还可以查看通过 Portal 发布过的消息的历史记录。

常有客户疑惑，为什么只有一个设备在线时，Portal 的在线用户统计数量却是 2 ？原因很简单，Portal 也同时是一个 [JavaScript](https://github.com/yunba/yunba-javascript-sdk) 客户端，可以向指定应用（[AppKey](https://github.com/yunba/kb/blob/master/AppKey.md)）的指定 Topic 发布消息，因此会算在统计内。

### 如何在云巴 Portal 上创建新应用

- 打开[云巴官方网站](http://yunba.io)，注册并登录。
- 登录后，会进入 Yunba Portal 界面，点击右上角 “我的应用” --> “创建新应用”。
- 逐一填写应用信息。其中，“应用名称” 和 “应用包名” 是必填项。对于 Android 应用来说，“应用包名” 一项需要填写 “Android” 应用包名。见下图。
- 对于 iOS 应用，在 “iOS 开发/生产证书” 处上传 iOS 开发/生产证书（*.p12）。如果证书导出时有设置密码，需要在 “开发/生产证书密码” 项填上证书的密码。
- 创建完成后，查看 “应用信息” 页面，可以看到应用的 AppKey、Secret Key 等。**请妥善保管好您的 AppKey、Secret Key 等应用信息，不要在群聊等公众场合下泄露。**

![tutorials_push_notification_iOS_create_new_app.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_tutorials/tutorials_push_notification_iOS_create_new_app.png)
