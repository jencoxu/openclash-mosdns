原文见[基于 DNS 的内网透明代理分流方案](https://songchenwen.com/tproxy-split-by-dns/)

## OpenClash配置

OpenClash 配置繁多，初始配置请自行参考 OpenClash 的 wiki，下面只说换成本文方案所需的配置。

插件设置 - 模式设置 - 运行模式： 切换到 Fake-IP（增强）模式

插件设置 - DNS 设置 - 本地 DNS 劫持 选择 禁用

插件设置 - 流量控制 - 绕过中国大陆 IP 取消勾选

插件设置 - 流量控制 - 仅允许内网 开启

插件设置 - IPv6 设置 这页的选项全都关闭就行了

覆写设置 - 常规设置 这里都不用改，只需要记住 DNS 监听，后面配置 mosdns 要用

覆写设置 - DNS 设置 - 自定义上游 DNS 服务器 勾选

覆写设置 - DNS 设置 - 追加上游 DNS 勾选

覆写设置 - DNS 设置 - 追加默认 DNS 勾选

覆写设置 - DNS 设置 - Fake-IP 持久化 勾选

覆写设置 - DNS 设置 页面下方 NameServer，FallBack，Default-NameServer 里的 DNS 服务器全都取消勾选，我们只用运营商提供的 DNS 服务器就够了，一般运营商 DNS 都是最快的，也是 CDN 最优化的。

插件设置 - GEO 数据库订阅 把 GeoIP Dat 和 GeoSite 这两个库的自动更新打开，都选 Loyalsoldier 的版本，这个是用来给 mosdns 用的。

插件设置 - 开发者选项里，我们自定义一下 iptables 规则。其中 /etc/mosdns/rule/geoip2ipset.sh 这个脚本可以根据 GeoIP 数据库来生成对应的 ipset，我这里只处理了 IPv4 的规则。IPv6 没管，因为也用不到。内容如下，这个文件放到路由器上后，记得要执行 chmod a+x /etc/mosdns/rule/geoip2ipset.sh 给它赋予可执行权限。

## Mosdns配置

选自定义配置文件，取消 DNS 转发的勾，然后我就直接贴配置了，注意 Clash DNS 端口要改成你自己在 OpenClash 里的配置，LAN IP-CIDR 也要改成你自己的内网配置，这里 mosdns 监听了 5335 端口。
