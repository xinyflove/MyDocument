##Drupal商派常用文档

前台前端页面

input输入框：

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
| 匹配不能纯数字、字母    | ```pattern="^(?!\d+$|[a-zA-Z]+$)[^\u4e00-\u9fa5]*$"```      |
| 匹配不能是小数          | ```pattern="^[0-9]+$"```      |
| 匹配不能用纯数字或中文  | ```pattern="^(?!\d+$)[^\u4e00-\u9fa5]*$"```      |
| 动态验证数据链接        | ```data-validate-remote-url="<{url action=topshop_ctl_passport@isExists type=account}>"```      |
| 动态验证数据name        | ```data-validate-remote-name="login_account"```      |
| 动态验证数据提示        | ```data-validate-remote-message="此帐号已被注册过，请换一个重试"```      |
| 验证错误提示信息2       | ```data-caution="请填写手机号"```      |
| 动态验证数据链接2       | ```data-remote="<{url action=topc_ctl_passport@checkLoginAccount}>"```      |
| 自动聚焦                | ```autofocus```      |
