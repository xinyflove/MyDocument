# API开发 #

## 文件位置 #

1. 文件统一放在如下位置：

原始文件
```
app/{$app_name}/api/
```
二开文件
```
custom/{$app_name}/api/
```

## API注册 #

1. 注册文件

原始文件
```
config/apis.php
```
二开文件
```
config/production/apis.php
```

2. 注册格式

```
'api的method' => ['uses' => '调用哪个类@哪个方法', 'version'=>['支持的版本号']],
```
例子:
```
'item.search' => ['uses' => 'sysitem_api_item_search@getList', 'version'=>['v1']],
```

3. API请求权限注册 API请求权限是注册给app的，比如topc应用可以请求systrade应用提供的api，需要注册如下信息：(tip:此项未实践)

```
//表示topc可以调用systrade的api，并且每60秒可以调用1000次
    'depends'=>array (
         'topc' => array (
             'systrade' => array ( 'appName' => 'systrade', 'path' => '*', 'limit_count' => 1000, 'limit_seconds' => 60,),
         ),
    ),
```
dev应用提供了一个命令：cmd dev:rpc depends_info命令可以获取当前代码的调用情况。直接将显示出来的数组复制到config/apis.php的depends项即可

## API实现 #

1. CLASS格式
```
<?php
/**
 * - syscontent.content.get.info
 * - 用于获取文章的详情
 */
class syscontent_api_getContentInfo {

    /**
     * api接口的名称
     * @var string
     */
    public $apiDescription = '获取文章详情';

    /**
     * 定义API传入的应用级参数
     * @desc 用于在调用接口前，根据定义的参数，过滤必填参数是否已经参入，并且定义参数的数据类型，参数是否必填，参数的描述
     * @return array 返回传入参数
     */
    public function getParams()
    {
        //接口传入的参数
        $return['params'] = array(
            'fields'     => ['type'=>'field_list', 'valid'=>'',         'title'=>'需要的字段', 'example'=>'', 'desc'=>'需要的字段'],
            'article_id' => ['type'=>'int',        'valid'=>'required', 'title'=>'文章id',    'example'=>'', 'desc'=>'文章id'],
        );

        return $return;
    }

    /**
     * 获取单个商品的详细信息
     * @desc 用于获取单个商品的详细信息
     * @return int article_id 文档ID
     * @return string title 文章标题
     * @return int modified 文章最后修改时间
     * @return string content 文章内容
     * @return int node_id 文章所属类目ID
     */
    public function getContentInfo($params)
    {
        $syscontentLibArticle = kernel::single('syscontent_article_article');
        try
        {
            $syscontentInfo = $syscontentLibArticle->getArticleInfo($params);

        }
        catch(Exception $e)
        {
            $msg = $e->getMessage();
            return $this->splash('error',null,$msg,true);
        }
        return $syscontentInfo;
    }

}
```

## 约定 #

1. 一个文件只提供给一个接口使用

2. 类的注释

将API定义文件config/apis.php中的api定义的uses别名带上，方便查找本api，便于开发， 例如

```
/**
 * - syscontent.content.get.info
 * - 用于获取文章的详情
 */
 ```
 
 3. $apiDescription 接口的名称，例如
 
 ```
 /**
 * api接口的名称
 * @var string
 */
public $apiDescription = '获取文章详情';
```

4. 入参方法

```
function getParams()内定义的是入参需要检验的字段，共5个，

[type=>'字段类型','valid'=>'验证规则','title'=>'字段名','example'=>'示例值','desc'=>'字段的详细描述','msg'=>'参数错误提示信息' ]

`valid`字段的验证规则参考文件config/validation.php
```

例如：

```
/**
 * 定义API传入的应用级参数
 * @desc 用于在调用接口前，根据定义的参数，过滤必填参数是否已经参入，并且定义参数的数据类型，参数是否必填，参数的描述
 * @return array 返回传入参数
 */
public function getParams()
{
    //接口传入的参数
    $return['params'] = array(
        'fields'     => ['type'=>'field_list', 'valid'=>'',         'title'=>'需要的字段', 'example'=>'', 'desc'=>'需要的字段'],
        'article_id' => ['type'=>'int',        'valid'=>'required', 'title'=>'文章id',    'example'=>'', 'desc'=>'文章id'],
    );

    return $return;
}
```

5. 响应方法

```
这里具体调用的api方法的注释有三个要求,例如上面例子当中的 function getContentInfo($params)
api方法的简单描述，如 `获取单个商品的详细信息`
api方法的详细描述，如 `@desc 用于获取单个商品的详细信息`
所有返回字段按照 `@return 返回类型(如int/string/array) 返回参数 返回参数描述`，如 `@return int node_id 文章所属类目ID`
```

例如1

```
/**
 * 获取单个商品的详细信息
 * @desc 用于获取单个商品的详细信息
 * @return int article_id 文档ID
 * @return string title 文章标题
 * @return int modified 文章最后修改时间
 * @return string content 文章内容
 * @return int node_id 文章所属类目ID
 */
public function getContentInfo($params)
{
    $syscontentLibArticle = kernel::single('syscontent_article_article');
    try
    {
        $syscontentInfo = $syscontentLibArticle->getArticleInfo($params);

    }
    catch(Exception $e)
    {
        $msg = $e->getMessage();
        return $this->splash('error',null,$msg,true);
    }
    return $syscontentInfo;
}
```

返回的参数如果有数组,数组主键和数组下的每个字段都写出来

例如2

```/**
 * 获取活动报名列表
 * @desc 用于获取活动报名列表
 * @return array data 活动报名列表
 * @return int data[].id 主键ID
 * @return int data[].shop_id 店铺ID
 * @return int data[].activity_id 活动ID
 * @return string data[].verify_status 审核状态
 * @return bool data[].valid_status 有效状态
 * @return string data[].refuse_reason 拒绝原因
 * @return timestamp data[].modified_time 报名最后更新时间
 * @return string count 返回数据数量
 */
public function registerList($params)
{
    # code...
}
```

## API查询 #

1. 方便开发本地就可以看api的定义，出参，入参
2. 链接： http://域名/dev

## 调用接口 #
```
//程序内部调用
app::get('topshop')->rpcCall('sysactivityvote.active.get', $apiData);
//sysactivityvote.active.get定义的接口
//$apiData传入的参数
//第三个参数为空或buyer或seller
```
```
//外部调用
//链接:
http://bbc.lo/index.php/api
//参数:
format=json //系统参数 返回格式
v=v1 //系统参数 版本
active_id=3 //定义参数 活动id
method=sysactivityvote.active.get×tamp=1511488868 //默认参数 接口名称×tamp=时间戳
sign_type=MD5 //默认参数 加密方式
sign=9DE3C6584A413A7C06A0FE9C0F823402 //默认参数 签名 [点击查看签名算法](/shopex/sign.md "签名算法")
```

## 整理常用的参数定义： #
例如:
```
public function getParams()
{
   $return['params'] = array(
      'shop_id' => ['type'=>'int', 'valid'=>'required', 'default'=>'', 'example'=>'1', 'desc'=>'店铺ID'],
   );
   return $return;
}
```

| 参数的参数定义 | 说明          | 可选值 |
| ------------- |:-------------|:-------------|
| type          | 参数类型(单个)     | int(整数)\| <br> string(字符串)\| <br> field_list(字段列表)\| <br> bool(布尔类型)\| <br> jsonArray(JSON数组)    |
| valid         | 验证条件(多个可用\|连接)     | required(必填)\| <br> integer(整数类型或者用int)\| <br> max:n(最大值，例如：max:20最大值20)\| <br> min:n(最小值，例如：min:1最小值1)\| <br> 空字符串(没有验证)\| <br> sometimes(未知含义)\| <br> boolean(布尔类型)\| <br> in:\*\*(限定值，例如：in:agree,refuse,non-reviewed,pending 取值范围在agree、refuse、non-reviewed、pending)\| <br> required_if:\*\*(未知含义 例如：required_if:status,refuse) \| <br> numeric(未知含义)\| <br>  |
| default       | 默认值              |           |
| example       | 示例值              |           |
| desc          | 描述(或者用description)          |           |
| msg          | 参数错误提示信息         |           |

