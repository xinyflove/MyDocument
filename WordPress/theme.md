# WordPress 主题开发 

WordPress主题目录位于 wp-content/themes/。主题的子目录拥有所有样式文件、模板文件、可选的函数文件 (functions.php)、JavaScript 文件、图片等。
比如说一个叫做 "test" 的主题就会放在 wp-content/themes/test/目录里。请避免使用数字名字，这会导致无法在主题列表中正常显示出来。

WordPress每一个发行版都会有一个默认的主题。请认真查看默认的主题，这样可能会对制作你自己的主题有帮助。

WordPress 主题除了图片和JavaScript，经常由三种文件构成。

1. 样式表文件 style.css， 控制着页面的外观
2. 函数文件 (functions.php)。
3. 模板文件，它控制着从数据库中调出的数据所呈现的外观。

## 1. 必需文件  

其中style.css和index.php这两个文件是必需文件  

### 1.1. style.css文件  

style.css文件有两个功能： 
1. 以注释的形式列出主题的详细信息  
两个不同的主题是不允许拥有相同的表述的 ， 因为这样会导致主题选择出错.如果你通过拷贝一个你已经制作的主题来制作你新的主题，请确保先更改这些头部注释.

下面是样式表头部注释的例子，被称作样式表头注释。比如主题"Twenty Seventeen":
```
/*
Theme Name: Twenty Seventeen
Theme URI: https://wordpress.org/themes/twentyseventeen/
Author: the WordPress team
Author URI: https://wordpress.org/
Description: Twenty Seventeen brings your site to life with header video and immersive featured images. With a focus on business sites, it features multiple sections on the front page as well as widgets, navigation and social menus, a logo, and more. Personalize its asymmetrical grid with a custom color scheme and showcase your multimedia content with post formats. Our default theme for 2017 works great in many languages, for any abilities, and on any device.
Version: 1.6
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentyseventeen
Tags: one-column, two-columns, right-sidebar, flexible-header, accessibility-ready, custom-colors, custom-header, custom-menu, custom-logo, editor-style, featured-images, footer-widgets, post-formats, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/
```

逐行的简单解释：

- /* 开启子主题的头部信息。
- Theme Name. (必需) 子主题的名称。
- Theme URI. (可选) 子主题的主页。
- Author URI. (可选) 作者主页。
- Author. (可选) 作者的名字。
- Description. (可选) 子主题的描述。比如：我的第一个子主题，真棒！
- Version. (可选) 子主题的版本。比如：0.1，1.0，等。
- Tags. (可选) 标签。

- */子主题头部信息的关闭标记。

2. 主题的样式代码

有了主题说明文件，在后台是不会列出这个主题信息的，因为还缺少一个必需文件index.php


### 1.2. index.php文件  

主模板.如果你的主题使用自己的模板，index.php 是必须要有的.

