##### 出错原因

错误原因是

`springboot @RabbitListener()  
public void listenOrder(OrderMessage orderMessage) `

监听了test 发送的消息

* @Profile("!test") // 仅在非测试环境中激活  

* 在 `application-test.properties`: 设置 `spring.rabbitmq.listener.simple.auto-startup=false`  