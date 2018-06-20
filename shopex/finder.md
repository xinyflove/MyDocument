# finder #
对finder不熟悉的建议看看文档 http://club.shopex.cn/doc/b2b2c-dev/500.bbc-develop/7000.desktop/2.desktop-devguide.md  

finder区图片:
![](./images/finder_detail.png)

## 一. finder方法 
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
               array(
                   'label'=>app::get('b2c')->_('删除'),
                   'icon' => 'download.gif',
                   'submit' => '?app=b2c&ctl=admin_goods_editor&act=doDelete',
                   'confirm' => app::get('b2c')->_('您在进行商品删除操作，平台方应承担此操作的风险后果，确定要删除选中商品？'),
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
title: 标题(图中的【1区】显示出来的内容)

actions: 自定义控制项(图中的【2区】里的内容除了显示内置的操作以外[use_buildin_set_tag,use_buildin_delete,use_buildin_export, 
use_buildin_import,use_buildin_filter等等这些是内置控制项]，还可以自定义添加新操作，参照上面格式。)

# 以下是内置控制项 

use_buildin_set_tag: 是否显示设置标签操作(值ture/false) 
use_buildin_tagedit: 是否显示标签管理操作(值ture/false)(暂未看出效果)

use_buildin_delete: 是否显示删除操作(值ture/false)

use_buildin_export: 是否显示导出操作(值ture/false)

use_buildin_import: 是否显示导入操作(值ture/false)

base_filter： 对列表数据进行过滤筛选，参照上面格式(值 数组)

top_extra_view 在finder列表头部增加其他自定义html显示,如top_extra_view=>array('app名称'=>'html模版页面路径');
use_view_tab: 是否显示finder中的tab（如果有），有无需看控制器中是否有_views方法,例如代码1-1。
use_buildin_filter: 是否使用高级筛选 图中【6区】
use_buildin_refresh: 是否显示刷新操作(列表配置项旁)
use_buildin_setcol: 是否显示列表配置项
use_buildin_selectrow: 是否显示每条记录前的复选按钮
allow_detail_popup: 是否显示查看列中的弹出查看图标（图 【4区】第二个图标）(暂未看出效果)
```

```
# 代码1-1
/**
* 列表tab
* @return array
*/
public function _views()
{
  $subMenu = array(
      0=>array(
          'label'=>app::get('sysmall')->_('待审核'),
          'optional'=>false,
          'filter'=>array(
              'status'=>'pending',
          ),
      ),
      1=>array(
          'label'=>app::get('sysmall')->_('审核通过'),
          'optional'=>false,
          'filter'=>array(
              'status'=>'onsale',
          ),

      ),
      2=>array(
          'label'=>app::get('sysmall')->_('审核驳回'),
          'optional'=>false,
          'filter'=>array(
              'status'=>'refuse',
          ),
      ),
      3=>array(
          'label'=>app::get('sysmall')->_('全部'),
          'optional'=>false,
      ),
  );
  return $subMenu;
}
```

## 二. 自定义finder

在实际业务中，会出现行数据的操作、查看等操作，这样就需要我们自己定义finder了。这里以我做的app sysmall为例： 

step1. 在sysmall中添加services.xml文件，并写入: 
```
<services>

    <service id="desktop_finder.sysmall_mdl_item">
        <class>sysmall_finder_item</class>
    </service>
    
</services>
```

step2. 在sysmall/lib/finder/目录下创建item.php文件，并写入: 
```
class sysmall_finder_item {
    public $column_edit = '操作';
    public $column_edit_order = 2;
    public $column_edit_width = 200;

    /**
     * 编辑链接
     * @param $colList
     * @param $list
     */
    public function column_edit(&$colList, $list){
        foreach($list as $k=>$row)
        {
            $editUrl = '?app=sysmall&ctl=item&act=check&finder_id='.$_GET['_finder']['finder_id'].'&p[0]='.$row['item_id'];
            $editTar = 'target="dialog::{title:\''.app::get('sysmall')->_('审核').'\', width:400, height:250}"';
            $html = '<a href="'.$editUrl.'" '.$editTar.'>'.app::get('sysmall')->_('审核').'</a>';

            $colList[$k] = $html;
        }
    }

    public $column_image_default_id = "缩略图";
    public $column_image_default_id_order = 1;

    /**
     * @param $colList
     * @param $list
     */
    public function column_image_default_id(&$colList, $list)
    {
        foreach($list as $k=>$row)
        {
            if($row['item_id'])
            {
                $item = app::get('sysitem')->model('item')
                    ->getRow('image_default_id', array('item_id'=>$row['item_id']));
                if($item['image_default_id'])
                {
                    $src = base_storager::modifier($item['image_default_id']);
                    $colList[$k] = "<a href='$src' class='img-tip pointer' target='_blank' onmouseover='bindFinderColTip(event);'><span><i class='fa fa-picture-o'></i></span></a>";
                }
            }
        }
    }

    public $detail_basic = '基本信息';
    public function detail_basic($id)
    {
        $where['mall_item_id'] = $id;
        $where['fields'] = "item_id";
        $mall_item = app::get('sysmall')->rpcCall('mall.item.get',$where);//获取选货商品详情数据

        $params['item_id'] = $mall_item['item_id'];
        $params['fields'] = "*,item_store";
        //$params['fields'] = "*,sku,item_store,item_status,item_count,item_desc,item_nature,spec_index";
        $pagedata = app::get('sysitem')->rpcCall('item.get',$params);//var_dump($pagedata);die;

        // 获取运费模板开始
        $tmpParams = array(
            'shop_id' => $pagedata['shop_id'],
            'template_id' => $pagedata['dlytmpl_id'],
            'status' => 'on',
            'fields' => 'shop_id,name,template_id',
        );
        $templateInfo = app::get('sysitem')->rpcCall('logistics.dlytmpl.get',$tmpParams);
        $pagedata['templateName'] = $templateInfo['name'];
        // 获取运费模板结束

        // 获取所属分类开始
        $catParams = array(
            'shop_id' => $pagedata['shop_id'],
            'cat_id' =>$pagedata['cat_id'],
            'fields' => 'cat_id,cat_name,is_leaf,parent_id,level');
        $pagedata['catInfo'] = app::get('sysitem')->rpcCall('category.cat.get.data',$catParams);
        // 获取所属分类结束

        // 获取店铺分类开始
        $shop_cat_id = explode(',',$pagedata['shop_cat_id']);
        $shopCatParams = array(
            'shop_id' => $pagedata['shop_id'],
            'cat_id' => $shop_cat_id['1'],
            'fields' => 'cat_id,cat_name,is_leaf,parent_id,level'
        );
        $shopCatData = app::get('sysitem')->rpcCall('shop.cat.get',$shopCatParams);
        foreach ($shopCatData as $key => $value) {
            $pagedata['childCatName'] = $value['cat_name'];
            $pagedata['parent_id'] = $value['parent_id'];
            if($value['parent_id']){
                $pagedata['parentCatInfo'] = app::get('sysitem')->rpcCall('shop.cat.get',array('shop_id' => $pagedata['shop_id'],'cat_id'=>$value['parent_id'],'fields'=>'cat_name'));
            }
        }
        // 获取店铺分类结束

        return view::make('sysmall/item/detail.html',$pagedata)->render();
    }
}
```
step3. 更新一下app 出现了 操作、缩略图、查看 列  
以 column开头的变量和方法是生成列数据的；  
以 detail开头的变量和方法是生成查看列数据的；  
