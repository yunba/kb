## 云巴 iOS 消息推送

如下图所示，客户端集成了云巴的 iOS SDK，
服务端通过云巴的 SDK 向 iOS 设备发消息。
<br>
一方面，云巴的服务器会负责向苹果的服务器发送 APNs 的消息；
另一方面，当应用在前台运行时，云巴会通过与 App 建立的长连接，直接推送内部消息。

![iOS_push_msg.png](https://raw.githubusercontent.com/yunba/docs/master/image/for_kb/iOS_push_msg.png)


* 集成 APNs

云巴 SDK 集成了 APNs，开发者无需开发与 APNs 对接的模块，也不必自己负责 Device Token 的更新，一切交给云巴。

* 确保消息的送达

众所周知，APNs 并不保证消息的送达。
而云巴 SDK 支持 [离线消息](https://github.com/yunba/kb/blob/master/云巴的离线消息.md) 的功能，可保证消息送达客户端。
<br>
在推送消息时，如果客户端当前不在线，消息将暂存在云巴服务器上（多达 50 条，长达 15 天）。
当客户端上线并成功连接到云巴的服务器后，服务器会把离线消息推送给该客户端。客户端成功接收后，服务器才会删除保存的离线消息。
<br>
