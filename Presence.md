## 实时在线（Presence）

### 1. Presence 的由来

作为一个基于 MQTT 协议的 Pub/Sub 实时系统，云巴的服务器上连接着千千万万不同平台的客户端。

对于使用云巴服务的开发者们来说，一个至关重要的运营数据就是：应用的某个用户当前是在线还是离线，有谁加入或离开了某个频道。

在 MQTT 协议中，并没有引入相关的功能。于是，我们利用 MQTT 现有的一些特性，设计了 Presence 功能。

### 2. 什么是 Presence

实时在线（Presence）是云巴提供的实时获取某个频道下所有用户（别名）的上、下线通知以及订阅、取消订阅该频道的通知。

**从这个定义可以看出，监听某个频道下的 Presence 消息的前提就是：每个用户都必须有自己的标识符。**

在云巴系统内部，会为每一个连接云巴的客户端生成一个唯一的标识符，即 UID。由于这个 UID 是一串无意义的字符串，不便于对外公开和使用，因而，我们设计了“别名”的概念来取代内部的 UID。

用户可以通过为客户端设置不同的“别名”来唯一标识客户端。云巴系统会将客户端的“别名”与其 UID 进行绑定。（有关别名的详细介绍，请参考[《频道与别名》](https://github.com/yunba/kb/blob/master/%E9%A2%91%E9%81%93%E5%92%8C%E5%88%AB%E5%90%8D.md#%E5%88%AB%E5%90%8Dalias)一文。）

换句话说，**使用 Presence，只能监听已经设置了 别名 的客户端，未设置 别名 的客户端不会被监听。**

### 3. Presence 的原理

Presence 的实质是，对 [频道](https://github.com/yunba/kb/blob/master/频道和别名.md#频道topic) 下所有用户 [别名](https://github.com/yunba/kb/blob/master/频道和别名.md#别名alias) 的状态的订阅。成功订阅后，Topic 下的任何用户别名的状态一旦发生变化，都会向 Topic + '/p' 频道发送消息。

例如，某用户（客户端）通过调用 `subscribe_presence("news")` 来监控 news 频道下的 Presence 消息。
调用成功后，云巴系统会自动为该客户端订阅一个名为 news/p 的频道，并将 news 频道的所有的 Presence 消息发给 news/p，让用户可以实时掌控该频道所有的 Presence 消息。

**注**：在调用 Presence API 时，系统自动为用户订阅的 Topic + '/p' 是一个特殊的频道，不会出现在用户实际的订阅列表中。

订阅了某个频道的 Presence 后，可以监听到的通知包括：
* Online：该频道下所有别名的上线通知
* Offline：该频道下所有别名的下线通知
* Join：某个用户（别名）订阅了该频道，即该频道下新增了一个用户（别名）
* Leave：某个用户（别名）取消订阅了该频道，即该频道下一个现有用户（别名）离开了


### 2. 相关 API
下面以 [JavaScript SDK](https://github.com/yunba/yunba-javascript-sdk) 为例，介绍一下与频道相关的 API。

* [`subscribe_presence`](http://yunba.io/docs2/Javascript_SDK/#subscribe_presence) 用来监听某个频道下所有用户的别名状态的变化。
* [`unsubscribe_presence`](http://yunba.io/docs2/Javascript_SDK/#unsubscribe_presence) 用来取消对某频道下用户别名状态变化的监听。

### 3. 举例
以云巴 [JavaScript SDK Demo](https://github.com/yunba/docs/blob/master/quickstart/demo/Demo_JavaScript.md) 为例。假设频道 news 下有一个名为 defy 的用户，下线后又立刻上线；后有一个名为 cat 的用户订阅了 news 频道，之后又立刻取消订阅。如果通过 `subscribe_presence` 订阅了 news，就可以实时获取到 defy 和 cat 的状态变化。
打印信息如下：

* 来自频道：news/p   消息内容：{"action":"offline","alias":"defy","timestamp":1454321557378}
* 来自频道：news/p   消息内容：{"action":"online","alias":"defy","timestamp":1454321558995}
* 来自频道：news/p   消息内容：{"action":"join","alias":"cat","timestamp":1454321577648}
* 来自频道：news/p   消息内容：{"action":"leave","alias":"cat","timestamp":1454321585416}
