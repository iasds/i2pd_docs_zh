匿名文件共享
============

**支持 I2P 的 BitTorrent 软件**

- [qBittorrent](http://qbittorrent.org/)（qBittorrent 有实验性的 I2P 支持）。qBittorrent 使用 SAM 协议，可在混合模式或 I2P-only 模式下使用。目前为 qBittorrent 配置 I2P 支持不够用户友好，且没有官方文档，因此需结合[此](qBittorrent.md)、[此](http://www.i2pforum.net/viewtopic.php?t=1224)和[此](https://strict3443.codeberg.page/i2p-info/hugo/public/posts/how-to-use-i2p-on-qbittorrent-nox/)指南进行设置。请注意，这是实验性功能，需使用 qBittorrent v4.6.0 或更高版本，可能会出现 bug。*小心使用并注意设置。该软件同时支持 I2P 和明网，可能会意外泄露你的地址。*

- [I2PSnark 独立版](https://gitlab.com/i2pplus/I2P.Plus/-/jobs/artifacts/master/raw/i2psnark-standalone.zip?job=Java8)（由 [I2P+ 项目](https://i2pplus.github.io/)提供的独立构建）。I2PSnark 使用 I2CP 协议，运行 i2pd 时需设置参数 `--i2cp.enabled=true` 或在配置文件中进行类似设置。

- [Vuze](https://en.wikipedia.org/wiki/Vuze) 和 [BiglyBT](https://www.biglybt.com)（Vuze 的分支）。Vuze 和 BiglyBT 使用 I2CP 协议，运行 i2pd 时需设置参数 `--i2cp.enabled=true` 或在配置文件中进行类似设置。*小心使用并注意设置。该软件同时支持 I2P 和明网，可能会意外泄露你的地址。*

- [XD](https://github.com/majestrate/XD)。*警告：XD 使用 SAM API，当前可能会导致 i2pd 崩溃。*

- [Robert](http://en.wikipedia.org/wiki/Robert_%28P2P_Software%29)。Robert 使用 BOB 协议，运行 i2pd 时需设置参数 `--bob.enabled=true` 或在配置文件中进行类似设置。

另请访问 [postman tracker](http://tracker2.postman.i2p)、[simp tracker](http://simp.i2p/)、[nyaa2p tracker](http://tracker.nyaa2p.i2p)、[nyaaplus tracker](http://nyaaplus.i2p) 及 [psa tracker](http://psa.i2p)。

*警告：如果不先停止使用 SAM API 的应用程序就尝试停止 i2pd，SAM API 当前可能会导致 i2pd 崩溃。*
