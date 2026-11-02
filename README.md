<h1>
本项目仅用于学习，不存在传播或售卖</h1>

# 仓库配置说明

### 自用仓库：

https://gh-proxy.com/https://raw.githubusercontent.com/lemonguo121/BoxRes/main/Myuse/cat.json

### 自用多线路仓库：

https://gh-proxy.com/https://raw.githubusercontent.com/lemonguo121/BoxRes/main/Myuse/lemon.json

### 直播源：

https://gh-proxy.com/https://raw.githubusercontent.com/lemonguo121/BoxRes/main/Myuse/live.txt

# app介绍

## 1、柠檬影视 手机竖屏版

> 最低支持安卓 **7.0**  📱
 <div>
<a href="https://gh-proxy.com/https://raw.githubusercontent.com/lemonguo121/BoxRes/main/Myuse/LMBox_Mobile1.0.12.apk" target="_self">
📃点击下载
</a>
</div>

### 功能介绍：

> 在基础tvbox功能上加入以下功能

1、应用内自动检测升级;

2、兼容大部分tvbox接口;

3、影视资源下载，下载管理，本地视频播放;

4、投屏功能功能（需配置柠檬影视（tv版）或其他集成dlan 播放SDK应用）;

5、支持二维码扫码识别接口，自动键入订阅管理;

6、深色、浅色主题切换;

7、分享功能;

## 2、柠檬TV  TV横屏版

> 最低支持安卓 **5.0** 📱
<div>
<a href="https://gh-proxy.com/https://raw.githubusercontent.com/lemonguo121/BoxRes/main/Myuse/LMBox_v1.0.2.apk" target="_self">
📃点击下载</a>
</div>

### 功能介绍：

> 在基础tvbox功能上加入以下功能

1、应用内自动检测升级;

2、兼容大部分tvbox接口;

3、集成dlan（投屏）播放功能;

## 3、小猫TV  TV横屏版 （后续不维护）

> 最低支持安卓 **4.1** 📱
<div>
<a href="https://gh-proxy.com/https://github.com/lemonguo121/BoxRes/raw/main/Myuse/LMBox_Mobile1.0.11.apk" target="_self">
📃点击下载</a>
</div>
<br/>

### 飞机讨论群

✈️：https://t.me/lemontvtvbox

## Flutter 音乐规则

新版lemon_os使用 [Myuse/music.json](Myuse/music.json)，不再通过独立Node音乐服务取数。旧music_plugin.json留给旧客户端，music_plugings作为迁移参考。

顶层version为1，musicSources是站点数组；每源有唯一id、name、baseUrl和rules。aiting/zz的id沿用原值，以兼容旧歌单与缓存。app自带同内容assets/json/music.json，仅默认远程配置网络失败时备用；发布规则后完整重启app重新读取。

| 字段 | 用途 |
| --- | --- |
| rules.search.music/album/artist/sheet | 各类搜索，未配置类型返回空 |
| rules.topLists / topListDetail | 榜单分组、榜单歌曲 |
| rules.media / lyric | 播放地址、歌词 |
| url / page | GET地址或接口请求前的浏览器页面 |
| fetch.url / method / query / form | 同浏览器内的GET或表单POST |
| fetch.decode | JSON字段路径到当前页面解码函数名，例如 {"url":"decodeUrl"}；支持返回字符串或Promise |
| format / list | html/json/text；CSS列表选择器或JSON数组路径 |
| fields内absolute | 配合url=true要求完整域名，避免将密文误作相对网址 |
| fields | selector+attribute，或path；value表示常量 |
| regex/group、split/index/remainder、replace、seconds、url | 正则、拆分/替换、时长秒数及相对URL转换 |
| pageSize / maxPages | 分页判断和请求上限，引擎最多10页 |

参数支持{query}、{id}、{page}、{type}，app按URL或表单上下文编码。page决定接口的浏览器上下文，Cookie由WebView管理，Referer及可设置请求头遵循浏览器规则；需要验证时让用户在原网页手工完成，普通空列表或HTTP错误不自动认作验证码。

爱听当前入口返回安全验证页，种子从本次开发环境访问超时；规则来自原插件，尚未完成真实客户端播放验收。没有封面时沿用占位图。复杂签名、解密、登录等新站点需要另外适配相应能力。

爱听当前接口url字段是密文，网页先decodeUrl再播放；本规则已配置fetch.decode.url=decodeUrl及媒体absolute校验，需要对应新版app规则引擎。函数名不带括号或表达式，在同一个已验证的歌曲页执行；解码器缺失时明确报错，已是完整网址的响应直接沿用。相对fetch地址以实际页面地址为基准。发布本次JSON后完整重启客户端读取新配置。
