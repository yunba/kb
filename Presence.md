## 实时在线

### 1. 什么是实时在线

实时在线（Presence）是云巴提供的实时获取某个频道下所有用户（别名）的上、下线通知以及订阅、取消订阅该频道的通知。

Presence 的实质是，对 [频道](https://github.com/yunba/kb/blob/master/频道和别名.md#频道topic) 下所有用户 [别名](https://github.com/yunba/kb/blob/master/频道和别名.md#别名alias) 的状态的订阅。成功订阅后，Topic 下的任何用户别名的状态一旦发生变化，都会向 Topic + '/p' 频道发送消息。

从上面的定义可以看出，监听某个频道下的 Presence 有两个条件：
* 客户端订阅了该频道
* 客户端设置了别名

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

* get_alias_list：cat defy
* 来自频道：news/p   消息内容：{"action":"offline","alias":"defy","timestamp":1454321557378}
* 来自频道：news/p   消息内容：{"action":"online","alias":"defy","timestamp":1454321558995}
* 来自频道：news/p   消息内容：{"action":"join","alias":"cat","timestamp":1454321577648}
* 来自频道：news/p   消息内容：{"action":"leave","alias":"cat","timestamp":1454321585416}
