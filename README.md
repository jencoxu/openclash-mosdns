原文见[基于 DNS 的内网透明代理分流方案](https://songchenwen.com/tproxy-split-by-dns/)
实现效果
# 完美保留了 AdGuardHome 的各种功能
## 基于 DNS 的流量分流，国内流量绕过 Clash 核心
### 用 Fake-IP 模式来解决 DNS 污染的问题，但限制 Fake-IP 的范围，不需要代理的域名仍返回正常 IP
#### 不用再费心找无污染的 DNS 服务器，使用运营商提供的 DNS 也没问题
##### 因为彻底解决了 DNS 污染，可以放心缓存 DNS 请求结果，开启 AdGuardHome 的乐观缓存后，DNS 平均处理时间降到 3ms
###### 完美兼容 IPv6。国内流量可正常使用 IPv6 服务。只要代理有 IPv6 出口，那国外也可正常使用。（使用 IPv6 居然还有意料之外的好处，后悔没早开）
####### 可以通过 AdGuardHome 的 Web 管理页面轻松切换内网设备是否走代理
