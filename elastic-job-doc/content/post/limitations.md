+++
date = "2016-01-27T16:14:21+08:00"
title = "使用限制"
weight=7
+++

# 使用限制

* 作业一旦启动成功后不能修改作业名称，如果修改名称则视为新的作业。

* 同一台作业服务器只能运行一个相同的作业实例，因为作业运行时是按照`IP`注册和管理的。

* 一旦有服务器波动，或者修改分片项，将会触发重新分片；触发重新分片将会导致运行中的流式处理的作业在执行完本次作业后不再继续执行，等待分片结束后再恢复正常。

* 开启`monitorExecution`才能实现分布式作业幂等性（即不会在多个作业服务器运行同一个分片）的功能，但`monitorExecution`对短时间内执行的作业（如每5秒一触发）性能影响较大，建议关闭并自行实现幂等性。

* `elastic-job`没有自动删除作业服务器的功能，因为无法区分是服务器崩溃还是正常下线。所以如果要下线服务器，需要手工删除`zookeeper`中相关的服务器节点。由于直接删除服务器节点风险较大，暂时不考虑在运维平台增加此功能。