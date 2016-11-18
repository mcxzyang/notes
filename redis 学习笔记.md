# redis 学习笔记

## geo地理位置

> 该模块可以对二者之间的经纬度进行距离计算并且排序

+  添加 **更新也可以进行此操作**  `geoadd` `geoadd hotels 114.22323 23.4233 Guangzhou 115.23232 21.2323232 Qingyuan`
+  获取某个地方的经纬度 `geopos` `geopos hotels Guangzhou`
+  计算两个位置之间的距离 `geodist` `geodist hotels Guangzhou Qingyuan km`
+  获取指定范围内的元素 `georadiusbymember` `georadiusbymember Guangzhou 50 km withdist asc `
+  由于geo位置是存在zset中，所以可以用zrem来进行删除 `zrem` `zrem hotels Guangzhou `
+  列出所有 `zrange hotels 0 -1`

