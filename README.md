# linkServer

###配置模块和日志模块
这两个模块是在别的开源项目源码中提取出来的

###packet包格式
数据包的格式是有规则的，一个数据包至少8个byte
----     ----    ----   ----
 4byte(包大小，字节数) | 4byte（协议号，心跳为0）| 真实数据
----     ----    ----   ----

ps：packet读取的时候前四个字节会只是通过包大小读取剩下内容，不会存储到packet数据结构中

###协议号（目前支持的，其他协议会根据协议路由到其他模块去，linkServer不处理逻辑）
0 ：心跳包
1 ：登录包
目前为了测试实现了简单的登录注册session，使用json格式传输注册信息，auth模块还没实现，这个应该是自定义的。
 
###说明
实现过程为了方便，很多配置都没有弄成到配置文件，一般这些也不大用修改，例如：
1. tcp的心跳包如果30s内没有收到数据，则认为链接已经失效，会断开和清楚session
2. 单个packet大小不能超过1MB，当然可以修改
