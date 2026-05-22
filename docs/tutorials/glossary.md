术语表
=======

`地址簿（Addressbook）`
i2pd 内置组件，管理 I2P 网络中的服务目标地址，将 Base64 哈希映射为人类可读的名称（例如 .i2p 域名）。可通过手动添加或订阅 hosts.txt 文件来添加目标地址。

`Base32（B32）/ Base64（B64）`
Base32 地址（始终以 .b32.i2p 结尾）是 Base64 目标地址的哈希值。对于 I2P 网络上的服务，Base64 哈希通常映射到地址簿中的 .i2p 域名。

`BOB`
BOB（基本开放桥接协议，Basic Open Bridge）是一个简单的应用层到路由器协议，i2pd 仍支持该协议。

`目标地址（Destination）`
隧道入站端点的唯一加密标识，提供对 I2P 网络上服务的访问，以公钥的 Base32 或 Base64 哈希形式表示。相当于 IP 地址和端口。

`Eepsite`
托管在 I2P 网络上的网站。在 i2pd 中，可通过在 tunnels.conf 中配置 HTTP 服务器隧道并将其指向本地 Web 服务器来托管。

`Floodfill`
I2P 网络中负载提供和接收其他路由器信息的路由器。带宽充足（至少 128 KB/s 共享）的路由器可充当 floodfill；如有必要，可在 i2pd.conf 中强制启用。

`大蒜路由（Garlic Routing）`
洋葱路由的一种变体。它将多条消息（称为 "大蒜瓣"）及其各自的传递指令打包到单个加密有效载荷中。这使得流量分析更加困难，同时减少了开销并提高了数据传输效率。

`I2CP`
I2P 客户端协议（I2CP）允许外部应用（客户端）通过单一 TCP 套接字与 i2p 路由器通信，默认端口 7654。

`I2NP（I2P 网络协议）`
负责在 I2P 路由器之间路由和混合消息的协议层。它在传输层（NTCP2 / SSU2）之上运行，用于 NetDB 操作、隧道构建和端到端大蒜消息传递。

`授权（Lease）`
定义特定隧道有权接收发往某个目标地址的消息的信息。

`LeaseSet`
一组隧道入口点（Lease），属于同一个目标地址。注意：0 跳服务器隧道无论配置了多少条隧道，都只有一个 Lease。i2pd 支持高级 LeaseSet 类型，如加密 LeaseSet2。

`多宿（Multihoming）`
通过共享同一目标地址的私钥，服务可在多台路由器上同时托管。这通过提供冗余增强了安全性和稳定性；如果一台路由器下线，服务仍可用。

`网络数据库（NetDb）`
分布式数据库，包含路由器联系信息（RouterInfo）和目标地址联系信息（LeaseSet）。每台 i2p 路由器维护一个用于通信的数据库子集（NetDb）。存储在磁盘上，启动时加载到内存。

`NTCP / NTCP2`
NTCP2 是基于 TCP 的传输协议，用于在路由器之间传递 I2NP 消息。它改进了针对主动和被动攻击的安全性和混淆能力，提供了更好的流量识别抵抗能力，并使用现代加密技术（默认使用 ChaCha20-Poly1305，并支持可选的抗量子变体）。

`SSU / SSU2`
SSU2（安全半可靠 UDP 版本 2）是当前基于 UDP 的传输协议。它在路由器之间提供加密、半可靠的 I2NP 消息传递。

`出站代理（Outproxy）`
I2P 网络上的一个服务，提供连接到明网的代理。

`参与（Participation）`
允许其他路由器通过你的 i2pd 路由器构建隧道，从而为 I2P 网络做出贡献的行为。需要至少 12 KB/s 的上行共享带宽。被防火墙限制的路由器参与度有限。

`补种（Reseeding）`
获取路由器身份信息的过程，通常来自明网服务器，确保你的 i2p 路由器能连接到 I2P 网络。对新安装进行引导至关重要。

`路由器（Router）`
核心 i2pd 软件，在 I2P 网络上路由加密数据包。默认情况下，所有路由器都参与网络（无基于国家的限制）。

`路由器身份（Router Identity）`
定义 I2P 网络上路由器唯一身份的信息，包括其 IP 地址（或引荐节点）、监听端口和公钥。也称为 RouterInfo；对应于 NetDb 中的对等节点。

`SAM`
SAM（简单匿名消息传递，Simple Anonymous Messaging）是一种协议，允许使用任何语言的客户端应用通过套接字接口与 i2pd 路由器进行 I2P 通信。

`隧道（Tunnel）`
I2P 网络上客户端或服务器之间的单向加密通信路径。类似于 Tor 电路，但为单向。

`隧道终点（Tunnel Endpoint）`
隧道中的最后一个路由器：要么是出站终点（Outbound Endpoint，客户端隧道在此与目标地址的入站网关相遇），要么是入站终点（Inbound Endpoint，连接到目标服务器）。

`隧道网关（Tunnel Gateway）`
隧道中的第一个路由器。对于入站隧道，该信息列在 NetDb 的 LeaseSet 中。对于出站隧道，它是发起路由器。

`中转隧道（Transit Tunnels）`
你的路由器代表其他用户参与的隧道。中转流量使 I2P 真正去中心化。

`探测隧道（Exploratory Tunnels）`
路由器用于 NetDB 操作、路由器发现和测试自身客户端隧道的特殊隧道池。它们使用更广泛的对等节点选择，无需高带宽。

`家庭（Family）】
家庭是由同一实体或个人运营的一组路由器。[了解更多](https://i2p.net/en/docs/overview/network-database/#family-options)。

`DHT（分布式哈希表）`
用于某些项目中，通过以键值对形式在分布式环境中存储信息，使对等节点相互连接。

`客户端隧道（Client Tunnels）】
出站 TCP 隧道，允许本地应用连接到 I2P 网络上的远程服务。它们将流量从指定本地端口转发到远程 I2P 目标地址（通常为 .b32.i2p 地址）。

`路由器能力（Router Caps）】
路由器能力是一组发布在网络数据库（NetDb）中 [RouterInfo](https://i2p.net/en/docs/overview/network-database/#routerinfo) 条目内的简短标志。

`网络状态（Network Status）】
显示你的路由器在 I2P 网络中的当前集成度和可达性。**OK** - 路由器已完全集成。**Firewalled** - 路由器无法接收直接入站连接，仍可作为客户端工作，但依赖引荐节点和仅出站路径。**Testing** - 启动或可达性探测期间的临时状态。[了解更多](https://i2p.medium.com/i2p-for-beginners-java-software-guide-685d7a7ed57b#ac59)。
