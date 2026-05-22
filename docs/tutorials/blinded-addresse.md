加密 LeaseSet2 配置
=====================

[加密 LeaseSet](https://i2p.net/en/docs/specs/encryptedleaseset/) 是 [LeaseSets2 (LS2)](https://i2p.net/en/docs/specs/common-structures/#leaseset2) 的盲化加密变体，它向 floodfill 节点隐藏信息。

加密 LeaseSet 仅支持服务器隧道（类型：`server`、`http`、`irc`）。客户端隧道不能发布加密 LeaseSet。

### 启用加密 LeaseSet2：

- 签名类型必须为 Red25519（`signatureType=11`）
- 在隧道配置中设置 I2CP 参数 `i2cp.leaseSetType=5`

隧道启动后，i2pd 会自动生成盲化密钥，加密 LeaseSet，并以加密 LeaseSet2 的形式发布。

### 示例（无认证）

将其添加到你的 `~/.i2pd/tunnels.conf`：

```
[MyEncryptedService]
type = http    
host = 127.0.0.1
port = 8080              # 你的 Web 服务器监听的本地端口
keys = encrypted.dat     # 持久密钥文件（若不存在将自动创建）
signatureType = 11
i2cp.leaseSetType = 5
```

保存文件并重新加载隧道配置（[Web 控制台](http://127.0.0.1:7070/?page=commands)）或重启 i2pd。

注意：要访问该服务，你需要 b33 地址。你可以在 [Web 控制台](http://127.0.0.1:7070/?page=i2p_tunnels) 中你的隧道（例如 MyEncryptedService）的加密 B33 地址（Encrypted B33 address）下找到它。

### 添加客户端认证

基本参数：

```
i2cp.leaseSetAuthType = 0     # 0 = 无认证（默认），1 = DH，2 = PSK
i2cp.leaseSetPrivKey = ...    # （仅客户端）你的私钥/base64 格式 PSK
```

选项 1：DH 认证

1. 为每个客户端生成 [X25519](https://github.com/PurpleI2P/i2pd-tools/blob/master/x25519.cpp) 密钥对（使用 [i2pd-tools](https://github.com/PurpleI2P/i2pd-tools/) 中的 `x25519` 工具）：

```bash
x25519
```

   例如输出：
```
PublicKey:  Ihr8wZS8fuA5Q-Exwb-9tGHpyV6lZfFilYPCx8bNoG0=
PrivateKey: 8HlgzxO-pJ3A1rtcc~7nnz774nyKXLLsVeuDGGlc63o=
```

2. 在服务端：

```
signatureType = 11
i2cp.leaseSetType = 5
i2cp.leaseSetAuthType = 1
i2cp.leaseSetClient.dh.1 = friend1:Ihr8wZS8fuA5Q-Exwb-9tGHpyV6lZfFilYPCx8bNoG0=
# 添加更多客户端：i2cp.leaseSetClient.dh.<整数> = 名称:公钥
```

3. 在客户端：

```
destination = <b33 地址>
i2cp.leaseSetPrivKey = 8HlgzxO-pJ3A1rtcc~7nnz774nyKXLLsVeuDGGlc63o=
```

选项 2：PSK 认证（使用共享密钥）

1. 生成一个随机的 32 字节 base64 格式 PSK（`openssl rand -base64 32` 或任何安全来源）。

   例如：
```
$ openssl rand -base64 32
dGhpcyBpcyBhIHJhbmRvbSAzMi1ieXRlIHByZS1zaGFyZWQga2V5Cg==
```

2. 在服务端：

```
i2cp.leaseSetAuthType = 2
i2cp.leaseSetClient.psk.1 = friend1:dGhpcyBpcyBhIHJhbmRvbSAzMi1ieXRlIHByZS1zaGFyZWQga2V5Cg==
# 多个客户端可共享同一个 PSK。
# 添加更多客户端：i2cp.leaseSetClient.psk.<整数> = 名称:<base64 编码的 32 字节 PSK>
```

3. 在客户端：

```
destination = <b33 地址>
i2cp.leaseSetPrivKey = dGhpcyBpcyBhIHJhbmRvbSAzMi1ieXRlIHByZS1zaGFyZWQga2V5Cg==
```

**注意**：先从不带认证的配置开始，确认 b33 地址可用后再添加认证。
