在 HaikuOS 系统上编译
=============================

* [HaikuOS](#HaikuOS)

## HaikuOS
```bash
pkgman refresh
pkgman install boost1.91_devel
# 若未安装
pkgman install make
pkgman install gcc
pkgman install git
# ^^^ 安装以上包
git clone https://github.com/PurpleI2P/i2pd.git
cd i2pd
# make -j#你的 CPU 核心数，或直接 make
make
```

编译完成后即可运行：
```bash
./i2pd
```

另外，右键点击时间，打开设置，找到同步并同步时间——这是必需的！
按 Control+C 关闭后，工作目录为 ~/config/settings/i2pd
你可以在其中创建 i2pd.conf 和 tunnels.conf，并创建隧道
HaikuOS 还有一个简单的 GUI。
