# Magento1.8 笔记

## 基本骨架
---

### 模块路径
+ 系统模块 `app\code\core\Mage`
+ 个人模块 `app\code\local\Packagename`,Packagename是一个唯一字符串，代表自定义模块名称

### 模块目录
每一个模块都可能包含:		

+ app\code\local\Packagename\Configviewer\controllers
+ app\code\local\Packagename\Configviewer\etc
+ app\code\local\Packagename\Configviewer\Helper
+ app\code\local\Packagename\Configviewer\Model
+ app\code\local\Packagename\Configviewer\sql

注：不一定需要包含以上所有目录

### 配置项		
+ 路径 `app/code/local/Alanstormdotcom/Configviewer/etc/config.xml`
+ 模块配置项

```
<config>	
	<modules>
		<Alanstormdotcom_Configviewer>
			<version>0.1.0</version>
		</Alanstormdotcom_Configviewer>
	</modules>
</config>
```

+ `app/etc/modules/Alanstormdotcom_Configviewer.xml`
+ 系统配置项，来激活上面的模块

```
<config>
	<modules> 
		<Alanstormdotcom_Configviewer> 
			<active>true</active>
			<codePool>local</codePool><
		/Alanstormdotcom_Configviewer>
	</modules>
</config>
```




