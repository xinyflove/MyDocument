# config配置文件 #

配置文件放在/config/目录下，生产环境配置文件在/config/production/目录下。

## 获取与配置设置 #

例子:
```
config::get('storepermission.common.nologin'));
```
获取的是:

/config/production/storepermission.php文件的 数组中 ['common']的['nologin']中的数组值。
```
return array(

    'common' => [
        'permission' =>[  //公共权限的路由
			    'topstore.signin',
			    'topstore.simpleSignin',
			    'topstore.postsignin',
			    'topstore.nopermission',
			    'topstore.postnosignin',
        ],
        'nologin' => [	//不需要登录的路由
			    'topstore.signin',
			    'topstore.simpleSignin',
			    'topstore.postsignin',
			    'topstore.nopermission',
			    'topstore.postnosignin',
         ]
    ],
    
);
```
