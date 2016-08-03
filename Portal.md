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
<br>

### 利用云巴 Portal 发布消息
客户端集成 YunBa SDK 后，打开 Portal 上应用详情页面，可以向客户端 `subscribe` 的 [频道](https://github.com/yunba/kb/blob/master/%E9%A2%91%E9%81%93%E5%92%8C%E5%88%AB%E5%90%8D.md#%E9%A2%91%E9%81%93topic)（Topic）发布消息，客户端即可收到消息，如图所示:
<br><br>
![tutorials_push_notification_iOS_publish.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_tutorials/tutorials_push_notification_iOS_publish.png)
<br><br>
在客户端（以 Android 客户端为例）订阅频道：
<br><br>
![android_emu_appmsg.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_quickstart/android_emu_appmsg.png)
<br><br>
客户端收到 Portal 发布的消息：
<br><br>
![android_emu_pushmsg.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_quickstart/android_emu_pushmsg.png)
<br><br>
**Publish2 发布消息**<br>
- 点击 **Publish2** 可测试扩展参数的消息的发送，如下图。<br>
- 点击 **更多选项** 可设置 [离线消息](https://github.com/yunba/kb/blob/master/%E4%BA%91%E5%B7%B4%E7%9A%84%E7%A6%BB%E7%BA%BF%E6%B6%88%E6%81%AF.md)保留时间（Time To Live）、[QoS](https://github.com/yunba/kb/blob/master/QoS.md) 值 和 [Message ID](https://github.com/yunba/kb/blob/master/MessageID.md)（如果不填则由系统自动生成）
<br>
- 可设置 **APN JSON** 发送 APNs 消息，发送 APNs 消息的方法具体可参考 [如何通过云巴实现 APNs 推送](https://github.com/yunba/kb/blob/master/%E5%A6%82%E4%BD%95%E9%80%9A%E8%BF%87%E4%BA%91%E5%B7%B4%E5%AE%9E%E7%8E%B0%20APNs%20%E6%8E%A8%E9%80%81.md) 和 [APNs 参数设置](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/TheNotificationPayload.html#//apple_ref/doc/uid/TP40008194-CH107-SW1)。
<br><br>
![publish2.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_kb/Portal_publish2.png)
<br><br>
**查看 Portal 上发布的历史消息**<br>
点击 **历史消息** 可查看在 Portal 上发布的历史消息。
<br>

### 云巴 Portal 的发布上报统计
![report.jpeg](https://raw.githubusercontent.com/yunba/docs/master/image/publish_statistic.png)
<br>
如图所示，可查看该应用（[AppKey](https://github.com/yunba/kb/blob/master/AppKey.md)） 下的消息发布和送达情况。<br>蓝色波形为一定时间（10 秒、分钟、小时、日）内的消息发布数量；蓝色波形为一定时间内的消息送达数量。（Portal 也属于一个用户）<br>

### 云巴 Portal 的在线用户统计
![online.jpeg](https://raw.githubusercontent.com/yunba/docs/master/image/online_statistic.png)
<br>
- 一段时间内的在线用户数：该时间段内持续在线（connected）的用户数量。如：“在线用户数/小时” 的单位表示该小时内持续在线，未断开与云巴的长连接的用户数量。
<br>
- 一段时间内的活跃用户数：该时间段内进行过上线操作的用户数量（不一定持续在线）。如：“活跃用户数/小时” 的单位表示该小时内进行过上线操作，即连接过云巴服务的用户数量。
<br><br>
**注**：如果订阅了该 Topic 但未设置用户 [别名](https://github.com/yunba/kb/blob/master/%E9%A2%91%E9%81%93%E5%92%8C%E5%88%AB%E5%90%8D.md#%E5%88%AB%E5%90%8Dalias)（Alias），则在 “在线用户”和“频道用户列表” 都不进行显示。
<br><br>
**频道用户列表**<br>
点击 **频道用户列表**，可查看应用（[AppKey](https://github.com/yunba/kb/blob/master/AppKey.md)） 下某个 [频道](https://github.com/yunba/kb/blob/master/%E9%A2%91%E9%81%93%E5%92%8C%E5%88%AB%E5%90%8D.md#%E9%A2%91%E9%81%93topic) 的收听用户别名列表。<br>

