# app开发 #

## 在原有app基础上二次开发 #

一般禁止在 app/ 目录进行原有的app二次开发,默认二次开发目录为 custom/,不要把要二次开发的原有app目录整个赋值到custom目录下，只
把需要修改的文件复制到对应位置进行修改开发. 

例如:我们要修改app/sysitem/controller/admin/item.php文件,把此文件复制到custom/sysitem/controller/admin/item.php进行修改
开发. 

## 创建新的app #

以app名称为testapp为例,在 app/ 目录下创建 app/testapp/ 目录,然后创建 app/testapp/app.xml 文件,文件内容为: 

```
<app>
    <name>Test App</name><!--填写应用名称-->
    <description>Test App应用描述</description><!--填写描述-->
    <type>service</type><!--app类型-->
    <author><!--填写作者信息-->
        <name>Caffrey Xin</name><!--填写作者名称-->
        <email>xinyflove@sina.com</email><!--填写作者邮箱-->
        <url>xinyufeng.net</url><!--填写作者链接地址-->
    </author>
    <version>0.1</version><!--版本号-->
    <license>不需要证书</license><!--证书信息-->
    <depends><!--填写依赖包信息-->
        <app>desktop</app><!--填写具体依赖的app目录名称-->
    </depends>
</app>
``` 

注意:如果涉及到数据库表的使用type标签内容一定要为service,并且要在 app/ 目录下创建 app/dbschema/ 目录. 

然后在 custom/ 目录下创建 custom/testapp/ 目录,把 app/testapp/app.xml 文件,复制到 custom/testapp/app.xml 文件.

