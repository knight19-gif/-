## 飞书笔记地址

https://wcn6txjin710.feishu.cn/wiki/EPH2wY5mDipO2pkUwsBc2ftanYe?edition_id=wuVxhF

[‌⁠‌⁠‍‍‍‌⁠⁠⁠‬‌‬⁠‍⁠‌‍‍⁠﻿‍‌‍‌‬﻿详细设计 - 飞书云文档](https://i8tqkikctf.feishu.cn/docx/BiaddJVZaoj7NbxnwM1c6Uzxn8c)



## 接入层，MQ，Handle

每一种渠道建立一个Kafka的Topic，然后建立多个Listener来监听消费

3y的策略：1个topic，多个消费者，根据消息进行分流



## 链路追踪，规则引擎，去重，限流，设计模式

xhy社区课程



## 架构图

![架构图](assets/架构图.png)



## 接入层

在austini-api模块下定义发送消息的接口，在austin-api-impl下实现具体的逻辑。

```java
public interface SendService {
    /**
     * 单模板单文案发送接口
     * @param sendRequest
     * @return
     */
    SendResponse send(SendRequest sendRequest);


    /**
     * 单模板多文案发送接口
     * @param batchSendRequest
     * @return
     */
    SendResponse batchSend(BatchSendRequest batchSendRequest);

}
```

对外提供的接口，除了需要提供Single接口，**最好还提供个Batch接口**。

因为很有可能业务方是需要一次批量执行的（如果只有Single接口，那就需要多次远程调用，这样对业务而言就不太合适了）



## SendResponse

send方法接收一个SendRequest参数 return一个SendResponse，这个SendResponse是立即返回的吗，其中的属性怎么确定的



## Api接入层：发送消息责任链

**详情见飞书 4.2**

<img src="assets/发送消息责任链.png" alt="发送消息责任链" style="zoom:67%;" />





## handle逻辑下发层：消息消费责任链