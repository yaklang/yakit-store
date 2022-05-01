## 使用
Fofa API KEY请参考 https://fofa.info/personalData  
Fofa帮助请参考 https://fofa.info/static_pages/api_help

## 高级语法
可以使用括号 和 && || !=等符号，如  
title="powered by" && title!="discuz"
body="content=WordPress" || (header="X-Wingback" && header="/xmlrpc.php" && body="/wp-includes/") && host="qq.cn"

关于建站软件的搜索语法请参考：https://fofa.info/library

## 语法

title="beijing" 从标题中搜索“北京"

header="elastic" 从http头中搜索“elastic"

body="网络空间测绘" 从html正文中搜索“网络空间测绘"

domain="qq.com" 搜索根域名带有qq.com的网站。

icon_hash="-247388890" 搜索使用此icon的资产。 仅限FOFA高级会员使用

host=".qq.cn" 从url中搜索".qq.cn" 搜索要用host作为名称

port="6379" 查找对应“6379"端口的资产

icp="京ICP证030173号" 查找备案号为“京ICP证030173号"的网站 搜索网站类型资产

ip="1.1.1.1" 从ip中搜索包含“1.1.1.1"的网站 搜索要用ip作为名称

ip="220.181.111.1/24" 查询IP为“220.181.111.1"的C网段资产

status_code="402" 查询服务器状态为“402"的资产

protocol="quic" 查询quic协议资产 搜索指定协议类型(在开启端口扫描的情况下有效)

country="CN" 搜索指定国家(编码)的资产。

region="HeNan" 搜索指定行政区的资产。

city="HanDan" 搜索指定城市的资产。

cert="baidu" 搜索证书(https或者imaps等)中带有baidu的资产。

cert.subject="Oracle Corporation" 搜索证书持有者是Oracle Corporation的资产

cert.issuer="DigiCert" 搜索证书颁发者为DigiCert Inc的资产

cert.is_valid=true 验证证书是否有效，true有效，false无效，仅限FOFA高级会员使用

banner=users && protocol=ftp 搜索FTP协议中带有users文本的资产。

type=service 搜索所有协议资产，支持subdomain和service两种。

os="centos" 搜索操作系统为CentOS资产。

server=="Microsoft-IIS/10" 搜索IIS 10服务器。

app="Microsoft-Exchange" 搜索Microsoft-Exchange设备

after="2017" && before="2017-10-01" 时间范围段搜索

asn="19551" 搜索指定asn的资产。

org="Amazon.com, Inc." 搜索指定org(组织)的资产。

base_protocol="udp" 搜索指定udp协议的资产。

is_fraud=false 排除仿冒/欺诈数据

is_honeypot=false 排除蜜罐数据，仅限FOFA高级会员使用

is_ipv6=true 搜索ipv6的资产,只接受true和false。

is_domain=true 搜索域名的资产,只接受true和false。

port_size="6" 查询开放端口数量等于"6"的资产，仅限FOFA会员使用

port_size_gt="6" 查询开放端口数量大于"6"的资产，仅限FOFA会员使用

port_size_lt="12" 查询开放端口数量小于"12"的资产，仅限FOFA会员使用

ip_ports="80,161" 搜索同时开放80和161端口的ip资产(以ip为单位的资产数据)

ip_country="CN" 搜索中国的ip资产(以ip为单位的资产数据)。

ip_region="Zhejiang" 搜索指定行政区的ip资产(以ip为单位的资产数据)。

ip_city="Hangzhou" 搜索指定城市的ip资产(以ip为单位的资产数据)。

ip_after="2021-03-18" 搜索2021-03-18以后的ip资产(以ip为单位的资产数据)。

ip_before="2019-09-09" 搜索2019-09-09以前的ip资产(以ip为单位的资产数据)。