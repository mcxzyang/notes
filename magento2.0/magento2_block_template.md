## Magento2 Block Template
---

### 模板的重写
> Mgento2 中，如果有些业务需要改掉html模板，可以用不修改框架本身的源代码，直接在自定义的模块中，覆盖原来的Block 或者 Template 即可

**举例说明**

若想修改前台的用户注册页面 `custimer/account/create`,具体实现的步骤为:

1. 找到该模板在框架核心代码中的位置，核心代码一般在 `vendor/magento` 中，然后根据 `模块名/控制器名/方法名` ，在 `view/frontend/layout` 中找到相关的 `.xml` 文件，该 示例 中就是 `customer_account_create.xml`
2. 在自定义模块的 `view/frontend/layout` 中 创建 `customer_account_create.xml`,代码如下： 

```
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" layout="1column" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceBlock name="customer_form_register" remove="true"/>
		<referenceContainer name="content">
    		<block class="Magento\Customer\Block\Form\Register" 				name="my_customer_form_register" 					template="Namespace_ModuleName::form/register.phtml">
        	<container name="form.additional.info" as="form_additional_info"/>
        	<container name="customer.form.register.fields.before" a			s="form_fields_before" label="Form Fields Before" htmlTag="div" 		htmlClass="customer-form-before"/>
    </block>
	</referenceContainer>
    </body>
</page>
```

- `<referenceBlock name="customer_form_register" remove="true"/>` 中 `customer_form_register` 要和核心代码中一样

- `<block class="Magento\Customer\Block\Form\Register" name="my_customer_form_register" template="Namespace_ModuleName::form/register.phtml">` 中 `class="Magento\Customer\Block\Form\Register"` 即可指向核心Block，也可指向自定义的Block ,`template="Namespace_ModuleName::form/register.phtml"` 指向 新的模板的位置
- Block 的格式为:  

```
<?php
namespace Jerry\Member\Block;
use Magento\Framework\View\Element\Template;

class ContactForm extends Template {
	public function __construct(Template\Context $context, array $data){
		parent::__construct($context, $data);
		$this->_isScopePrivate = true;
	}
}
```

> 需要在模板里面用到的方法就可以在这Block里面写了