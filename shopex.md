# 商派系统(shopex)常用文档

## [app开发](/shopex/create_app.md 'app开发')

## [app类 (app::get('app_name'))](/shopex/app_class.md 'app类 (app::get('app_name'))')

## [db数据库操作](/shopex/db.md 'db数据库操作')

## [数据动态扩展(dbeav app)model函数](/shopex/dbeav_model.md '数据动态扩展(dbeav app)model函数')

## [API开发](/shopex/api.md 'API开发')

## [config配置文件](/shopex/config.md 'config配置文件')

## [定时任务](/shopex/crontab.md '定时任务')

## [数据表定义](/shopex/dbschema.md '数据表定义')

## [finder](/shopex/finder.md 'finder')

## [](/shopex/model.md '')

## [签名算法](/shopex/sign.md '签名算法')

## [视图相关的类和函数](/shopex/view_class_function.md '视图相关的类和函数')

## 创建一个对象

```
kernel::single($class_name,$arg=null)
//例如:
kernel::single('sysbankmember_bank')
//生成的是目录为sysbankmember/lib/bank.php 里的class为sysbankmember_bank的对象
kernel::single('sysbankmember_data_bank')
//生成的是目录为sysbankmember/lib/data/bank.php 里的class为sysbankmember_data_bank的对象
```

## 类的自动载入机制
```
$gravatar = new notebook_gravatar;
//生成的是目录为notebook/lib/gravatar.php 里的class为notebook_gravatar的对象
$gravatar = new notebook_data_gravatar;
//生成的是目录为notebook/lib/data/gravatar.php 里的class为notebook_data_gravatar的对象
```

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
| NOT IN          | ```$tmpfilter['user_id\|notin']=array(1,2,3,4,.....)```  | user_id NOT IN (1,2,3,4,...)  |
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

### 获取app的model

```
app::get('sysactivityvote')->model('active');//获取app为sysactivityvote的表active的model
```

## 函数

### 全局函数：

| 函数 | 说明          |
| ------------- |:-------------|
| request::method() == 'GET'         | 获取请求方式(GET或POST)          |
