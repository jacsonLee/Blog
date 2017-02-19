## 使用redis实现二度好友

### 二度好友实现思路

将不同用户的好友集合做交集计算,然后含有交集的,而且不在一度好友里面的就是二度好友

### 步骤

1.通过sadd把用户的好友关系存入redis里面

2.在redis里面选取所有的用户id出来,redis的读11000次/s,不用担心跟数据库一样的性能问题

3.进行差集处理:1.去掉登录用户本身的id,去掉登录用户的好友集合,剩下的就是差集.

4.迭代差集里面的所有id,然后去redis里面获取好友关系,采用sinter对比登录用户和差集用户之间是否存在交集,若存在,则表示和两者是二度好友,添加到列表数组里面。反之,并非二度好友关系！

