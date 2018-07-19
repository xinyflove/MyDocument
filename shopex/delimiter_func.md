# 定界符函数

说明:  
左定界符 `<{` , 右定界符`}>`,由定界符组成的函数认为是定界符函数, 例如:`<{include }>`.  

使用定界符函数时，会调用`base/lib/view/compilers/tramsy.php`文件中的`parseTag($function, $arguments)`函数。  

1.例如：  
我们使用`<{url action=topshop_ctl_item@storeItem}>`，
打印输出变量信息`$function=string(3) "url"`、`$arguments=array(1) { ["action"]=> string(28) "'topshop_ctl_item@storeItem'"}`,
函数**存在**变量`$this->buildinTags`中，修改函数字符串为`parseTagUrl`，
在**本文件**调用`parseTagUrl函数`，并传入参数`$arguments`。  
  
2.例如：  
我们使用`<{input type="category" name="item[cat_id]" shop_id=$shopId value=$item.cat_id callback="categoryCallback"}>`，
判断`$this->_compile_ui_function($function, $arguments, $_result)`为true，  
调用`base/lib/component/ui.php`中的`input($params)`函数。  

|定界符函数|调用文件|
|---|:--|
|`<{input }>`|`base/lib/component/ui.php`的`input`函数|
|||

3.  

4.  

5.例如，我们使用`<{header app=topc}>`，`$this->_compile_custom_function($function, $arguments, $_result)`判断为true，根据情况调用不同文件。  

|定界符函数|调用文件|
|---|:--|
|`<{header }>`|`topc/lib/site/view/helper.php`的`function_header`函数|
|||
