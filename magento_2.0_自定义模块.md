# Magento 2.0 自定义模块
---

1. 在code目录下面建立 `(namespace)`\ `(module)` 文件夹 例如 Jerry\Member
2. 在 `Member` 文件夹下建立如下文件夹:
	+ Controller	`控制器目录`
	+ etc `模块管理配置`
3. 在 `Member` 文件夹下建立 注册文件 `registration.php`

```
<?php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    '命名空间_模块名',
    __DIR__
);
```

4. 在 `etc` 目录下面建立 `module.xml`

```
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="命令空间_模块名" setup_version="2.0.0"/>
</config>
```

5. 在 `Controller` 目录下面建立 `Index\Index.php`控制器

```
<?php
namespace 命令空间\模块名\Controller\Index;
use \Magento\Framework\App\Action\Action;
class Index extends Action
{
    /** @var  \Magento\Framework\View\Result\Page */
    protected $resultPageFactory;
    /**
     * @param \Magento\Framework\App\Action\Context $context
     */
    public function __construct(\Magento\Framework\App\Action\Context $context,
                                \Magento\Framework\View\Result\PageFactory $resultPageFactory)
    {
        $this->resultPageFactory = $resultPageFactory;
        parent::__construct($context);
    }
    /**
     * Blog Index, shows a list of recent blog posts.
     *
     * @return \Magento\Framework\View\Result\PageFactory
     */
    public function execute()
    {
    	echo '123';die;
        return $this->resultPageFactory->create();
    }
}
```
## 注意修改以上的命令空间和模块名称

- 在项目文件主目录运行 `sudo bin\magento module:status`
- `sudo bin\magento module:enable 命名空间_模块名`
- `sudo bin\magento setup:upgrade`
- `sudo bin\magento module:status`