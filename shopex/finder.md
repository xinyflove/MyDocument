# finder #
对finder不熟悉的建议看看文档 http://club.shopex.cn/doc/b2b2c-dev/500.bbc-develop/7000.desktop/2.desktop-devguide.md  

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
           'use_buildin_set_tag'=>true,
           'use_buildin_filter'=>true,
           'use_buildin_export'=>true,
           'allow_detail_popup'=>true,
           'use_view_tab'=>true,
           'base_filter'=>array( //对tab数据进行过滤筛选
               'order_refer'=>'local',
               'disabled'=>'false'
           ),
           'finder_aliasname'=>'xxxx',
       )
   );
}
```

后台的控制器必须继承desktop_controller，继承后才有finder方法，下面介绍下finder方法的几个参数：

1.第一个参数是字符串，（上例中是b2c_mdl_goods），是model里的class名，它决定了finder列表的数据源，默认情况下是b2c_mdl_goods类里的getlist方法返回的数据

2.第二个参数是数组，这个数组内涵相当丰富，解释如下：

