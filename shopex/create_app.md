# app开发

## 在原有app基础上二次开发

    一般禁止在 app/ 目录进行原有的app二次开发,默认二次开发目录为 custom/,不要把要二次开发的原有app目录整个赋值到custom目录下，只把需要修改的文件复制到
对应位置进行修改开发。
例如:我们要修改app/sysitem/controller/admin/item.php文件,把此文件复制到custom/sysitem/controller/admin/item.php进行修改开发。
