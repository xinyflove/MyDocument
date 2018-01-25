# 商派系统(shopex)常用文档

## [app开发](/shopex/create_app.md 'app开发')

## [app类 (app::get)](/shopex/app_class.md 'app类 (app::get)')

## [db数据库操作](/shopex/db.md 'db数据库操作')

## [数据动态扩展(dbeav app)model函数](/shopex/dbeav_model.md '数据动态扩展(dbeav app)model函数')

## [API开发](/shopex/api.md 'API开发')

## [config配置文件](/shopex/config.md 'config配置文件')

## [前台前端页面](/shopex/front_html_page.md '前台前端页面')

## [定时任务](/shopex/crontab.md '定时任务')

## [数据表定义](/shopex/dbschema.md '数据表定义')

## [finder](/shopex/finder.md 'finder')

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

## 函数

### 全局函数：

| 函数 | 说明          |
| ------------- |:-------------|
| request::method() == 'GET'         | 获取请求方式(GET或POST)          |
