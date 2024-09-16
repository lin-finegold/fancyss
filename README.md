# [fancyss - 科学上网](https://hq450.github.io/fancyss/)

- Fancyss is a project providing tools to across the GFW on asuswrt/merlin based router with software center. 
- 此项目提供用于asuswrt、asuswrt-merlin为基础的，带软件中心固件（≥384）路由器的科学上网功能。



## 插件特色

- 多平台支持：博通armv7，博通arm64，联发科Filogic 830 MT7986A
- 多客户端支持：Shadowsocks、ShadowsocksR、V2ray、Xray、Trojan、NaïveProxy、TuicV5、Hysteria2
- shadowsocks支持SIP003插件：simple-obfs和v2ray-plugin；V2ray和Xray支持多种协议配置
- 多种模式支持：gfwlist模式、大陆白名单、游戏模式、全局模式、回国模式
- 提供多种现成的DNS方案，并且可以自由方便的进行DNS方案自定义配置
- 支持SS/SSR/V2ray/Xray/Trojan节点的在线订阅，支持节点生成二维码用以分享
- 故障转移、主备切换、负载均衡、定时重启、定时订阅、规则更新、二进制更新
- 支持kcptun、udpspeeder、udp2raw，可以实现代理加速，游戏加速，应对丢包等
- 同时提供full版本和lite版本，hnd_lite版本安装后占用不到8MB的空间，适合小jffs机型
- armv8机型支持tcp fast open和ss/ssr/trojan多核心运行

## 支持机型/固件

> 以下为fancyss 3.0支持的机型/固件，点击机型可以前往相应固件下载地址
> 
> 最新固件下载地址：[https://fw.koolcenter.com/](https://fw.koolcenter.com/)


## 版本选择

fancyss 3.0支持hnd、hnd_v8、qca、arm、mtk 五个平台，每个平台又有full版本和lite版本

full版本为全功能版本，支持SS、 SSR、V2ray、 Xray、Trojan、NaïveProxy、TuicV5、Hysteria2 八种客户端，安装包体积较大

lite版本为精简版本，支持SS、 SSR、 V2ray、 Xray、 Trojan 五种客户端，安装包小巧，以下为lite版本精简内容：

1. lite版本移除了NaïveProxy支持及其相关二进制文件：naive、ipt2socks
2. lite版本移除了shadowsocks的v2ray-plugin插件功能及其对应的二进制文件：v2ray-plugin
3. lite版本移除了UDP加速功能及其二进制文件：speederv1、speederv2、udp2raw
4. lite版本移除了KCP加速功能及其二进制文件：kcptun
5. lite版本移除了负载均衡支持及其页面和二进制文件：haproxy
6. lite版本移除了直连解析的DNS方案及其二进制：chinadns、chinadns、https_dns_proxyy
7. lite版本移除了haveged，因为现在较新的固件系统自带了熵增软件
8. lite版本移除了shadowsocks-rust替换shadowsocks-libev功能，默认由shadowsocks-libev运行ss协议
9. lite版本移除了socks5页面及其脚本及其acl规则文件

如果是不折腾以上被精简功能的用户，完全可以使用体积更小的lite版本

RT-AX56U_V2、RT-AX57 这种jffs分区极小(15MB)的机型，直接使用lite版本即可

要切换为lite版本，直接安装lite版本的离线安装包即可，以后在线更新也会维持为lite版本

要切换为full版本，直接安装full版本的离线安装包即可，以后在线更新也会维持为full版本

RT-AX86U、GT-AX6000等armv8机型（见上表），从3.0.6开始建议安装fancyss_hnd_v8版本，当然fancyss_hnd同样兼容

## 插件安装

1. 离线安装：下载并校验好离线安装包后，在软件中心内使用**离线安装**/**手动安装**功能，选择安装包后上传并安装即可。

2. 命令安装：(以fancyss_hnd_lite.tar.gz为例，先下载好安装包，并将其上传到路由器的/tmp目录)

   ```bash
   mv /tmp/fancyss_hnd_lite.tar.gz /tmp/shadowsocks.tar.gz
   tar -zxvf /tmp/shadowsocks.tar.gz
   sh /tmp/shadowsocks/install.sh
   ```

## 关于皮肤

目前插件皮肤支持以下版本：

asuswrt：经典asuswrt皮肤

rog：华硕红色rog皮肤

tuf：华硕橙色tuf皮肤

tx：华硕天选青色皮肤

## 注意事项

* 强烈建议使用chrome或者chrouium内核的浏览器！以保证最佳兼容性！
* 强烈建议在`最新版本的固件`和`最新版本软件中心`上使用fancyss_hnd！
* 插件会自动跟随当前固件的皮肤类型，支持assuwrt、rog、tuf三种皮肤。
* 一些机型的联名版，只要刷了官改/梅林改版固件的，均能安装本插件！

## 目录说明

1. **fancyss**：插件代码主目录，由build.sh打包成不同路由器的离线安装包
2. **binaries**：一些在线更新的二进制程序，如v2ray、xray
3. **packages**：不同平台的离线安装包的最新版本，用于插件的在线更新
4. **rules**：插件的规则文件，如gfwlist.conf、chnroute.txt、cdn.txt

## 打包插件

> 打包过程就是将fancyss目录下相关二进制和代码文件通过脚本生成不同平台，不同版本的离线安装包。
>
> 为保证在不同路由器/固件版本中都能运行，项目提供的所有二进制都是预编译好的，且尽量提供全静态编译版本。

1. 克隆本项目：使用linux系统，比如Ubuntu 20.04

   ```bash
   git clone https://github.com/hq450/fancyss.git
   ```

2. 切换到3.0分支

   ```bash
   cd fancyss
   git checkout 3.0
   ```

3. 修改代码：根据自己需要修改代码主目录fancyss目录下的相关文件，如`./fancyss/ss/ssconfig.sh`

4. 打包插件，运行打包命令后会自动同步rules下最新的规则和binaries下最新的二进制

   如需要开发，请使用`sh build.sh debug`命令，将会额外打包带`debug`字样的安装包，安装包内网页文件等保留了注释信息

   ```bash
   sh build.sh
   ```

5. 打包好的离线安装包位于`./packages/`目录，包含以下5个平台的离线安装文件，每个平台分为full版本和lite版本

   ```bash
   fancyss_arm_full.tar.gz
   fancyss_arm_lite.tar.gz
   fancyss_hnd_full.tar.gz
   fancyss_hnd_lite.tar.gz
   fancyss_hnd_v8_full.tar.gz
   fancyss_hnd_v8_lite.tar.gz
   fancyss_qca_full.tar.gz
   fancyss_qca_lite.tar.gz
   fancyss_mtk_full.tar.gz
   fancyss_mtk_lite.tar.gz
   ```

## 相关链接

* **fancyss 3.0**更新日志：https://github.com/hq450/fancyss/blob/3.0/Changelog.txt

* 官改/梅改固件下载【网方网站】（最新固件）：[https://www.koolcenter.com](https://www.koolcenter.com/)
* 官改/梅改固件下载【固件镜像】（次新固件）：[https://fw.koolcenter.com](https://fw.koolcenter.com)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hq450/fancyss&type=Date)](https://star-history.com/#hq450/fancyss&Date)

[^1]: RT-AC86U从384_81918_koolshare固件版本开始，使用的是asuswrt风格ui，而不是rog风格。
[^2]: RT-AX89X采用的SoC为ipq8074/ipq8074A，支持64位系统，但是其固件是32位系统。
