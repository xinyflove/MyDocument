# 主题挂件开发 

## 1. 主题挂件文件目录  

主题挂件放在主题目录下的widgets文件夹下，例如我开发的blueberrymall主题  
public/themes/blueberrymall/widgets   

## 2. 挂件文件

例如我们开发一个 Logo挂件(logo)，首先在widgets目录下创建logo文件夹  
public/themes/blueberrymall/widgets/logo/  里面含有如下文件：  

`widgets/logo/images/icon.jpg`  可选，挂件图标  
`widgets/logo/_config.html`  必选，挂件配置文件  
`widgets/logo/default.html`  必选，挂件展示模版文件  
`widgets/logo/theme_widget_logo.php`  必选，挂件展示数据处理文件 
`widgets/logo/widgets.php`  必选，挂件描述文件  

注意:挂件展示数据处理文件由theme_widget_ 链接 挂件名(logo)组成  

挂件展示由theme_widget_logo.php处理数据，theme_widget_logo.php 中的theme_widget_logo($setting)方法  
返回数据，并在default.html渲染数据，原则上default.html中可以由任意的变量来接收theme_widget_logo.php文件  
返回的数据，变量$setting接收 为了防止变量冲突和规范性，变量$datas来接收theme_widget_logo.php文件处理后返回的数据，
