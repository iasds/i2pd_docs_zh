匿名站点
==================

## 浏览匿名站点

### 手动配置

要在隐形互联网中浏览匿名站点，请将你的网页浏览器配置为使用 HTTP 代理 127.0.0.1:4444（i2pd 默认即启用）。建议使用 HTTP 代理进行浏览，因为 i2pd 会过滤某些 HTTP 请求头。

在 Firefox 中：设置 -> 常规 -> 网络设置 -> 配置访问互联网的代理服务器 -> 选择 手动配置代理，输入 HTTP 代理 127.0.0.1，端口 4444

![img](media/http-1.png)

对于 Chromium ：使用参数运行可执行文件

    chromium --proxy-server="http://127.0.0.1:4444"

注意，如果你也希望保持匿名，你需要对浏览器进行隐私强化设置。请自行研究，[可以从这里起步](http://www.howtogeek.com/102032/how-to-optimize-mozilla-firefox-for-maximum-privacy/)。

### 最简单方案：I2PD 浏览器

如果你不想手动配置浏览器，可以使用 **[I2PD 浏览器](https://github.com/PurpleI2P/i2pdbrowser)**，这是一个官方捆绑包，会下载最新的 Firefox ESR，预先配置好与 i2pd 配合使用，使隐形互联网的浏览更加简单。

请参阅仓库中的平台特定说明。

即使使用 I2PD 浏览器，仍然建议**自行研究**额外的隐私加固措施，以获得最大匿名性。

众多隐形互联网网站的列表可在 [identiguy.i2p](http://identiguy.i2p) 找到。

## 托管匿名站点

如果你希望在隐形互联网中运行自己的网站，请按以下步骤操作：

1) 运行你的 Web 服务器，并找出它使用的主机:端口（例如 127.0.0.1:8080）。

2) 配置 i2pd 创建 HTTP 服务器隧道。在你的 ~/.i2pd/tunnels.conf 文件中加入：

    [anon-website]
    type = http
    host = 127.0.0.1
    port = 8080
    keys = anon-website.dat

3) 重启 i2pd 或发送 SIGHUP 信号。

4) 查找你的网站的 b32 目的地。

   前往 web 控制台 -> [I2P 隧道页面](http://127.0.0.1:7070/?page=i2p_tunnels)。查找 Server tunnels，你会在 anon-website 旁边看到类似 \<很长的一串字母\>.b32.i2p 的地址。

  你的网站已在隐形互联网中，访问该地址即可。

5)（可选）在 [reg.i2p](http://reg.i2p) 上注册一个简短且易记的 .i2p 域名。你也可以使用 [i2pd-tools](https://github.com/PurpleI2P/i2pd-tools) 中的 `regaddr` 生成认证字符串。