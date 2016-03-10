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

## 路由
---

`只需要给模块配置路由即可`

配置 `config.xml` 如下:		

```
<config>
	<modules>
	...
	</modules>
	<frontend>
		<routers>
			<helloworld>
				<use>standard</use>
				<args>
					<module>Alanstormdotcom_Helloworld</module>
					<frontName>helloworld</frontName>
				</args>
			</helloworld>
		</routers>
	</frontend>
</config>
```

+ `<frontend>` 代表 **前台**, `<admin>` 代表 **后台**
+ `<routers>` 代表 **路由**
+ `<module>` 代表 **模块全名**
+ `<frontName>` 代表 **路由名称**,比如: `http://www.dev.com/hellworld`

## 控制器
---

> 控制器放在每一个模块的 `controllers` 目录里面

控制器的形式为:		

```
class Alanstormdotcom_Helloworld_IndexController extends Mage_Core_Controller_Front_Action{ 
	publicfunctionindexAction(){ 
		echo'HelloWorld!';
	}
}
```

命名规则为:			

1. 以`<moudule>`标签的完整内容开始（Alanstormdotcom_Helloworld）
2. 紧接一个下划线（Alanstormdotcom_Helloworld_） 
3. 加上我们给控制器取的名字“Index”(Alanstormdotcom_Helloworld_Index) 
4. 最后加上关键词“Controller”（Alanstormdotcom_Helloworld_IndexController

```
自定义的控制器都必须继承 Mage_Core_Controller_Front_Action

```

### 控制器的执行顺序
比如 URL 为 http://www.dev.com/checkout/cart/add

1. 查询全局配置，找到frontName“checkout”对应的模块，Mage_Checkout
2. 找到执行控制器“Mage_Checkout_CartController”
3. 调用执行控制器的“addAction”方法

## 一些有用的方法及函数
---

+ $this->getRequest()	`获取所有传进来的参数对象`
+ $this->getRequest()->getParams() `获取所有的参数，返回key/value形式数组`
+ $this->getRequest()->getParam('username') `获取特定的参数`






