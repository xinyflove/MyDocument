# finder #
对finder不熟悉的建议看看文档 http://club.shopex.cn/doc/b2b2c-dev/500.bbc-develop/7000.desktop/2.desktop-devguide.md  

finder区图片:
![](./images/finder_detail.png)

举例：
```
function index(){
   $this->finder(
       'b2c_mdl_goods',
       array(
           'title'=>app::get('b2c')->_('商品列表'),
           'actions'=>array(
               array(
                   'label'=>app::get('b2c')->_('添加商品'),
                   'href'=>'index.php?app=b2c&ctl=admin_goods_editor&act=add','target'=>'_blank'
               ),
           ),
           'use_buildin_set_tag'=>true,//默认false
           'use_buildin_delete'=>true,//默认true
           'use_buildin_export'=>true,//默认false
           'use_buildin_import'=>true,//默认false
           'use_buildin_tagedit'=>true,
           'base_filter'=>array( //对列表数据进行过滤筛选
               'order_refer'=>'local',
               'disabled'=>'false'
           ),
           'top_extra_view'=>array('app名称'=>'html模版页面路径'),
           'use_view_tab'=>true,
           'use_buildin_filter' => true,//默认false
           'use_buildin_refresh' => true,//默认true
           'use_buildin_setcol' => true,//默认true
           'use_buildin_selectrow' => true,//默认true
           'allow_detail_popup' => true,
       )
   );
}
```

后台的控制器必须继承desktop_controller，继承后才有finder方法，下面介绍下finder方法的几个参数：

1.第一个参数是字符串，（上例中是b2c_mdl_goods），是model里的class名，它决定了finder列表的数据源，默认情况下是b2c_mdl_goods类里的getlist方法返回的数据

2.第二个参数是数组，这个数组内涵相当丰富，解释如下：

```
title: 图中的【1区】显示出来的内容

actions: 图中的【2区】里的内容除了显示内置的操作以外(use_buildin_set_tag,use_buildin_delete,use_buildin_export,use_buildin_import,use_buildin_filter这些是内置控制项)，还可以自定义添加新操作，参照上面格式。

use_buildin_set_tag: 是否显示设置标签操作

use_buildin_delete: 是否显示删除操作

use_buildin_export: 是否显示导出操作

use_buildin_import: 是否显示导入操作

use_buildin_tagedit: 是否显示标签管理操作(暂未看出效果)

base_filter： 对列表数据进行过滤筛选，参照上面格式

top_extra_view 在finder列表头部增加其他自定义html显示,如top_extra_view=>array('app名称'=>'html模版页面路径');
use_view_tab: 是否显示finder中的tab（如果有），有无需看控制器中是否有_views方法。(暂未看出效果)
use_buildin_filter: 是否使用高级筛选 图中【6区】
use_buildin_refresh: 是否显示刷新操作(列表配置项旁)
use_buildin_setcol: 是否显示列表配置项
use_buildin_selectrow: 是否显示每条记录前的复选按钮
allow_detail_popup: 是否显示查看列中的弹出查看图标（图 【4区】第二个图标）(暂未看出效果)
```
