# 利用iptables设置端口转发的shell脚本

## 项目作用

1. 便捷地设置iptables流量转发规则
2. 当域名解析的地址发生变化时，自动更新流量转发规则，不需要手动变更（适用于ddns域名）

## 用法

**国内机器使用**

> 通过Github Proxy加速下载

```shell
bash <(curl -fsSL https://us.arloor.dev/https://raw.githubusercontent.com/arloor/iptablesUtils/master/natcfg.sh)
```

**国外机器使用**

```
bash <(curl -fsSL https://raw.githubusercontent.com/arloor/iptablesUtils/master/natcfg.sh)
```

### 输出如下：

```
#############################################################
# Usage: setup iptables nat rules for domian/ip             #
# Website:  http://www.arloor.com/                          #
# Author: ARLOOR <admin@arloor.com>                         #
# Github: https://github.com/arloor/iptablesUtils           #
#############################################################

你要做什么呢（请输入数字）？Ctrl+C 退出本脚本
1) 增加转发规则          3) 列出所有转发规则
2) 删除转发规则          4) 查看当前iptables配置
#?
```

此时按照需要，输入1-4中的任意数字，然后按照提示即可。`Ctrl+C` 退出本脚本

## 卸载

**国内机器使用**

> 通过Github Proxy加速下载

```shell
bash <(curl -SsLf https://us.arloor.dev/https://raw.githubusercontent.com/arloor/iptablesUtils/master/dnat-uninstall.sh)
```

**国外机器使用**

```shell
bash <(curl -SsLf https://raw.githubusercontent.com/arloor/iptablesUtils/master/dnat-uninstall.sh)
```

## 查看日志

```shell
journalctl -exu dnat
```

## 配置文件备份和导入导出

配置文件在

```shell
/etc/dnat/conf
```

## trojan转发

总是有人说，不能转发trojan，这么说的人大部分是证书配置不对。最简单的解决方案是：客户端选择不验证证书。复杂一点是自己把证书和中转机的域名搭配好。

小白记住一句话就好：客户端不验证证书。

-----------------------------------------------------------------------------

## 推荐新项目——使用nftables实现nat转发

iptables的后继者nftables已经在debain和centos最新的操作系统中作为生产工具提供，nftables提供了很多新的特性，解决了iptables很多痛点。

因此创建了一个新的项目[/arloor/nftables-nat-rust](https://github.com/arloor/nftables-nat-rust)。该项目使用nftables作为nat转发实现，相比本项目具有如下优点：

1. 与docker兼容，与自定义的iptables规则兼容
2. 支持端口段转发
3. 转发规则使用配置文件，可以进行备份以及导入

所以**强烈推荐**使用[/arloor/nftables-nat-rust](https://github.com/arloor/nftables-nat-rust)。不用担心，本项目依然可以正常稳定使用。

PS: 新旧两个项目并不兼容，切换到新项目时，请先卸载此项目

