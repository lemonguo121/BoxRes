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

顶层version为1，musicSources是站点数组；每源有唯一id、name、baseUrl和rules。aiting/zz的id沿用原值，以兼容旧歌单与缓存。站点规则以本仓库为准；lemon_os测试阶段保留assets/json调试副本。Debug运行时加`--dart-define=USE_LOCAL_RULES=true`可直接读取应用内本地音乐/小说/漫画规则，无需先提交或推送本仓库；正常模式及Release只读取订阅，下载失败明确报错，不回退或自动补入随包站点。规则修改后完整重启app重新读取。

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
| pageSize / maxPages / pageStart | 分页判断、最多10页，pageStart默认1，好听轻音乐从0开始 |
| fields.concat | 拼接多个静态提取字段，任一部分缺失则整个字段为空 |
| media.headers / useBrowserUserAgent | 音源请求头字符串模板、复用已记录浏览器UA；同时传给播放与缓存，不写入歌曲历史 |

参数支持{query}、{id}、{page}、{type}，app按URL或表单上下文编码。page决定接口的浏览器上下文，Cookie由WebView管理，Referer及可设置请求头遵循浏览器规则；需要验证时让用户在原网页手工完成，普通空列表或HTTP错误不自动认作验证码。

爱听当前入口返回安全验证页，种子从本次开发环境访问超时；规则来自原插件，尚未完成真实客户端播放验收。没有封面时沿用占位图。复杂签名、解密、登录等新站点需要另外适配相应能力。

爱听当前接口url字段是密文，网页先decodeUrl再播放；本规则已配置fetch.decode.url=decodeUrl及媒体absolute校验，需要对应新版app规则引擎。函数名不带括号或表达式，在同一个已验证的歌曲页执行；解码器缺失时明确报错，已是完整网址的响应直接沿用。相对fetch地址以实际页面地址为基准。发布本次JSON后完整重启客户端读取新配置。

2026-11-02 新增好听轻音乐（htqyy）：单曲搜索及四个榜单，桌面/移动播放页静态字段组装音频地址，后台fetch播放页HTML避免执行站点播放器；每页20首、最多200首。Apple/Android使用既有原生请求头，Windows0.2.2保留代理及每曲UA被覆盖的限制（本样本默认Dart UA仍可取音频）；Mac独立原生取页/请求头/静音播放通过，后续实际Mac Debug应用已验热播榜200首、搜索bandari结果、榜单/搜索点歌与完整缓存，其他三端仍待实机验收。规则当前仅在本地工作区修改，未提交/推送。

2026-11-02 Mac实际应用续修：榜单片段接口直接作WebView主导航返回403，现改为page=/top/{id}，同页fetch /top/musicList/{id}并带X-Requested-With；搜索改为page=/后fetch /home/search，避免直接搜索页没有列表。应用热播榜200首、搜索点歌推进02:10/03:02、完整音频缓存与样本SHA256相同；最终86项回归通过。部分封面仍HTTP403而使用占位图；未验证所有曲目与其他三端。lemon_os提供Local rules (Debug) IDE配置读取本地副本，正常模式需发布本仓库后读取新版；本次仍未提交/推送。

2026-11-02 试接歌曲宝（gequla）：新增id=gequla，与gequbao.com关系未核实，不作为其官方备用。按该站公开脚本当前使用的第三方JSON服务配置单曲搜索（最多50条）、standard音源、歌词和封面，首页热歌只读网页展示的8条，不伪装完整排行榜。搜索/媒体/歌词以普通JSON主导航读取，不跨域fetch（现引擎fetch带credentials，而服务仅声明Access-Control-Allow-Origin:*）；不执行站点播放器，不保存临时音频地址，不增加Dart站点分支/依赖。规则本地与lemon_os调试副本同步，正常模式需本仓库发布后生效；当前未提交/推送。最终应用验收结果见lemon_os交接文档。

上述gequla已完成Mac Debug应用验收：首页热歌8首，富士山下点歌和4143691字节完整缓存SHA校验通过；搜索烟花易冷后点林志炫Live推进00:52/05:16，封面/歌词及暂停通过。lemon_os同步修正LRC兼容两/三位小数，94项回归通过；原三源内容保持，不保证全曲库或其他端已验，仍未推送。
