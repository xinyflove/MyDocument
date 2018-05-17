# 前台前端页面

## input输入框：

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

## 前端图片处理：

例子:
```
<img src="<{$imgurl|storager:'t'}>" alt="">
```
前端页面显示图片的时候用函数storager处理一下  
*tip:函数位置:app/base/lib/view/helper.php modifier_storager($image_id,$size='')*  

参数信息:
1.$imgurl 图片路径为相对路径  
2.storager函数参数:  
`l`:大图  `m`:中图 `s`:小图 `t`:微图  

在php文件处理图片函数为base_storager::modifier($image_id,$size)
*tip:函数位置:app\base\lib\storager.php modifier($imageUrl,$size='')*
参数信息:
1.$image_id 图片路径为相对路径  
2.$size `l`:大图  `m`:中图 `s`:小图 `t`:微图  


