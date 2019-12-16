# nettools
Advanced Network Technology Center -University of Oregon

http://packetlife.net/captures/

http://ipv6-test.com/pingtest/

#MTU
[root@localhost ~]# `cat /sys/class/net/eth0/mtu`

1500

[root@localhost ~]# `echo "1460" > /sys/class/net/eth0/mtu`


[root@localhost ~]# `cat /sys/class/net/eth0/mtu` 

1460


#Net Tools
``` bash
apt install -y tcptraceroute
tcptraceroute 20.0.0.9 80

wget http://pingpros.com/pub/tcpping

chmod 755 tcpping

mv tcpping /usr/bin/

tcpping 20.0.0.9:80

apt install hping3
```

### 使用 MakeCert 为点到站点连接生成并导出证书
[MakeCert](https://docs.microsoft.com/zh-cn/windows/win32/seccrypto/makecert?redirectedfrom=MSDN)  
[of](https://docs.azure.cn/zh-cn/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert)  
1. 生成Root证书
``` cmd
 .\makecert.exe -sky exchange -r -n "CN=P2SRoot2012Cert" -pe -a sha256 -len 2048 -ss My
```

2. 生成客户端证书
``` cmd
 .\makecert.exe -n "CN=P2S2012ChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRoot2012Cert" -is my -a sha256
```
### Azure VPN Windows Server 2012 R2 以下 812连接报错
[关于点到站点 VPN](https://docs.azure.cn/zh-cn/vpn-gateway/point-to-site-about#tls1)
[如何在 Windows 7 和 Windows 8.1 中启用对 TLS 1.2 的支持？](https://docs.azure.cn/zh-cn/vpn-gateway/point-to-site-about#tls1)

1. 右键单击“命令提示符” 并选择“以管理员身份运行” ，使用提升的权限打开命令提示符。
2. 在命令提示符窗口中运行以下命令:
``` powershell
reg add HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13 /v TlsVersion /t REG_DWORD /d 0xfc0
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp" /v DefaultSecureProtocols /t REG_DWORD /d 0xaa0
if %PROCESSOR_ARCHITECTURE% EQU AMD64 reg add "HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp" /v DefaultSecureProtocols /t REG_DWORD /d 0xaa0
```
3. 根据使用的系统版本安装以下更新:
[KB3140245](https://www.catalog.update.microsoft.com/search.aspx?q=kb3140245)
[KB2977292](https://www.catalog.update.microsoft.com/Search.aspx?q=KB2977292)

重启后重新连接VPN

