# QuantumultX_xyfy

<div align=center>
<img src="https://user-images.githubusercontent.com/57806936/188250273-4f02975f-9f9c-4d0f-b9d3-969400313489.png">
</div>

> 打卡最根本的问题就是通过支付宝这个接口登录需要支付宝app内部提供的auth_code用以xyfy服务器认证,但每次获取到的auth_code的有效期只有24小时,打卡的痛点又在于认证服务器的不响应,所以就想着做中间人攻击,每天拿到auth_code让脚本自己去尝试打卡.避免一直卡空白页等待.

**使用auth_code签到 auth_code的有效期为24小时 cron定时暴力美学 可以解决长时间卡白页的问题**

[//]: # (## 运行效果)

[//]: # ()
[//]: # (<div align=center>)

[//]: # (<img src="https://user-images.githubusercontent.com/57806936/187062036-a6bd9d52-addd-4f3d-8bdc-805cb82d48db.PNG" width="200px" height="440px">)

[//]: # (</div>)

[//]: # ()
[//]: # (<div align=center>)

[//]: # (<img src="https://user-images.githubusercontent.com/57806936/187062229-8650cb19-3aee-4ec9-9996-b5dc8b939594.PNG" width="200px" height="440px">)

[//]: # (</div>)

## 更新日志

2022/10/25
- 所有的弹窗通知都可以点击,跳转到相应指引位置
- 给任务适配了图标,如有需要请重新添加任务
- 尝试间隔时间100ms → 200ms

2022/09/21
- 改进打卡逻辑,脚本尝试登录直到登录成功,即一天只需执行一次.
- 取上一次的打卡数据,用于本次打卡,使用脚本无须再次填写任何数据.
- 取消通知与不通知区别的conf,获取完auth_token不通知,只在日志显示.
- 增加新版本发布提醒三遍,便于提醒更新.

2022/09/02
- 新增不提醒conf引用,避免每次打卡都弹提醒

2022/08/28
- 修改了README文档,说明脚本运行逻辑

2022/08/24
- 修复 setdata 函数的错误使用的问题
- 改进了打卡逻辑 避免无脑重复的向服务器发送打卡POST

# 正文部分


QuanX脚本->江西高校支付宝校园防疫打卡 使用方法分为三个Part 如下

- [Part1 配置QuanX](#part1-配置quanx)
- [Part2 QuanX获取auth_code](#part2-quanx获取auth_code)
- [Part3 配置定时任务](#part3-配置定时任务)


## Part1 配置QuanX

引用-资源重写-点击右上角添加新的资源

- 资源标签随便填 资源路径填 这个
- https://raw.githubusercontent.com/honue/QuantumultX_xyfy/master/QuantumultX_Token.conf

<div align=center>
<img src="https://user-images.githubusercontent.com/57806936/187061592-98af291c-1d39-40db-ba2d-54328825ec3b.PNG" width="300px">
</div>
  - 保存启用
<div align=center>
<img src="https://user-images.githubusercontent.com/57806936/187061853-a34d5695-2f29-4af4-92fe-52570b2cad94.JPEG" width="300px">
</div>

## Part2 QuanX获取auth_code

- 支付宝进入小程序即可完成auth_code的抓取 (注:现版本不弹窗通知,只要你的重写开着肯定是没问题的,抓取结果会在日志显示)
- 获取完毕就可以退出,每日进入一次获取auth_code就可以

将这个快捷指令添加到桌面,运行可以直接跳转到小程序获取auth_code https://www.icloud.com/shortcuts/0a6058ad85d14b049257060256b8b2c0

<div align=center>
<img src="https://user-images.githubusercontent.com/57806936/187061602-d26de395-3dd9-4e6c-b0c7-cb78019590b0.JPEG" width="300px">
</div>

## Part3 配置定时任务

- 点击右上角小闹钟开启定时任务
- 点击加号添加计划任务
  <div align=center>
  <img src="https://user-images.githubusercontent.com/57806936/185796529-8dbd0e13-07a0-43a5-9a24-52573d1b8b78.png" width="300px">
  </div>
- 点击文本方式添加,复制粘贴填下面的 (不要参考上图) 每天的0点,12点第5分钟会自动打卡,时间可以往后但不要往前调,服务器有一定时差.
- ```
  0 5 0,12 * * * https://raw.githubusercontent.com/honue/QuantumultX_xyfy/master/xyfy_token_task.js, tag=校园防疫, img-url=https://raw.githubusercontent.com/honue/QuantumultX/master/img/xyfy.png, enabled=true
  ```
- 配置完毕 右上角保存 请求列表右滑可以调试查看效果

## 感谢

[@chavy](https://github.com/chavyleung)

[@NobyDa](https://github.com/NobyDa)
