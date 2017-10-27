# Drupal商派常用文档

## 前台前端页面

### input输入框：

| 说明        | 代码          |
| ------------- |:-------------|
| 文本输入框              | ```type="text"```     |
| 密码输入框              | ```type="password"```      |
| 数字输入框 	          | ```type="number"```      |
| 必填信息                | ```required```      |
| 最小值                  | ```min="0"```      |
| 最大值                  | ```max="100"```      |
| 输入框内提示文字        | ```placeholder="6-20个字符,不能纯数字,字母"```     |
| 输入字符最小长度        | ```minlength="10"```      |
| 输入字符最大长度        | ```maxlength="20"```      |
| 验证输入字符最小长度    | ```data-validate-length-min="6"```      |
| 验证输入字符最大长度    | ```data-validate-length-max="16"```      |
| 验证错误提示信息        | ```data-validate-regexp-message="不能纯数字、字母"```     |
| 匹配不能纯数字、字母    | ```pattern="^(?!\d+$\|[a-zA-Z]+$)[^\u4e00-\u9fa5]*$"```      |
| 匹配不能是小数          | ```pattern="^[0-9]+$"```      |
| 匹配不能用纯数字或中文  | ```pattern="^(?!\d+$)[^\u4e00-\u9fa5]*$"```      |
| 匹配整数或小数二位      | ```pattern="^[0-9]+(.[0-9]{1,2})?$"```      |
| 动态验证数据链接        | ```data-validate-remote-url="<{url action=topshop_ctl_passport@isExists type=account}>"```      |
| 动态验证数据name        | ```data-validate-remote-name="login_account"```      |
| 动态验证数据提示        | ```data-validate-remote-message="此帐号已被注册过，请换一个重试"```      |
| 验证错误提示信息2       | ```data-caution="请填写手机号"```      |
| 动态验证数据链接2       | ```data-remote="<{url action=topc_ctl_passport@checkLoginAccount}>"```      |
| 自动聚焦                | ```autofocus```      |

## 数据库操作

### 列表操作符查询：
例如:app::get('sysuser')->model('account')->getList('user_id',$tmpfilter);

| 操作符        | 代码          | 代表SQL语句   |
| ------------- |:-------------|:-------------|
| IN              | ```$tmpfilter['user_id\|in']=array(1,2,3,4,.....)```     | user_id IN (1,2,3,4,...)      |
| LIKE            | ```$tmpfilter['user_name\|has']='小明'```                | user_name LIKE '%小明%'        |
| LIKE            | ```$tmpfilter['user_name\|head']='小明'```               | user_name LIKE '小明%'         |
| LIKE            | ```$tmpfilter['user_name\|foot']='小明'```               | user_name LIKE '%小明'         |
| NOT LIKE        | ```$tmpfilter['user_name\|nohas']='小明'```              | user_name NOT LIKE '%小明%'    |
| >               | ```$tmpfilter['user_age\|than']='18'```                 | user_age > '18'    |
| <               | ```$tmpfilter['user_age\|lthan']='18'```                | user_age < '18'    |
| =               | ```$tmpfilter['user_age\|nequal']='18'```或<br>```$tmpfilter['user_age\|tequal']='18'``` 或<br>```$tmpfilter['user_age']='18'```  | user_age = '18'    |
| <>              | ```$tmpfilter['user_age\|noequal']='18'```              | user_age <> '18'   |
| >=              | ```$tmpfilter['user_age\|bthan']='18'```                | user_age >= '18'   |
| <=              | ```$tmpfilter['user_age\|sthan']='18'```                | user_age <= '18'   |
| BETWEEN         | ```$tmpfilter['user_age\|between']=array(18,20)```       | user_age BETWEEN 18 AND 20 (未验证)  |

## 接口

### 接口参数定义：
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
| valid         | 验证条件(多个可用\|连接)     | required(必填)\| <br> integer(整数类型或者用int)\| <br> max:n(最大值，例如：max:20最大值20)\| <br> min:n(最小值，例如：min:1最小值1)\| <br> 空字符串(没有验证)\| <br> sometimes(未知含义)\| <br> boolean(布尔类型)\| <br> in:\*\*(限定值，例如：in:agree,refuse,non-reviewed,pending 取值范围在agree、refuse、non-reviewed、pending)\| <br> required_if:\*\*(未知含义 例如：required_if:status,refuse) \| <br>   |
| default       | 默认值              |           |
| example       | 示例值              |           |
| desc          | 描述(或者用description)          |           |

### 接口描述：
public $apiDescription = "接口描述";
