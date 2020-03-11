## Nessus Scan Summary 19_02_2020
New Scan: ESTL Scan Policy (NEW), February 19 at 1:55 PM  
Old Scan: NONE  

### New Vulnerabilities (None: 398, Low: 5, Critical: 1, Medium: 31)
#### Risk: Critical (1)
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| Unix Operating System Unsupported Version Detection | 33850 | 10.0.1.5 | tcp/0 [New 24] | New | KIV | See if OPNSense upgrade will fix this |
#### Risk: Medium (31) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| Network Time Protocol (NTP) Mode 6 Scanner | 97861 | 10.0.1.5 | udp/123  [New 30] | New | KIV | See if OPNSense upgrade will fix this |
| DNS Server Cache Snooping Remote Information Disclosure | 12217 | core-svcs1.cc.com | udp/53  [New 56] | New | Accepted | Internal usage |
| DNS Server Cache Snooping Remote Information Disclosure | 12217 | lb1.cc.com | udp/53  [New 369] | New | Accepted | Internal |
| SSL Medium Strength Cipher Suites Supported (SWEET32) | 42873 | core-svcs1.cc.com | tcp/6443  [New 82] | New | Accepted | Internal Use |
| SSL Medium Strength Cipher Suites Supported (SWEET32) | 42873 | dolly1.cc.com | tcp/6443  [New 172]<br>tcp/10250  [New 173] | New | Fixed | nano /etc/kubernetes/manifest/kube-apiserver.yaml<br>- --tls-min-version=VersionTLS12<br>- --tls-cipher-suites=TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>- --tls-min-version=VersionTLS12<br><br>nano /var/lib/kubelet/config.yaml<br>tlsMinVersion: VersionTLS12 <br> tlsCipherSuites: ['TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256','TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384','TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256'] |
| SSL Medium Strength Cipher Suites Supported (SWEET32) | 42873 | dolly4.cc.com | tcp/10250  [New 255] | New | Fixed | nano /var/lib/kubelet/config.yaml<br>tlsMinVersion: VersionTLS12 <br> tlsCipherSuites: ['TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256','TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384','TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256'] |
| SSL Medium Strength Cipher Suites Supported (SWEET32) | 42873 | etcd1.cc.com | tcp/2379  [New 311]<br>tcp/2380  [New 312] | New | Fixed | nano /etc/kubernetes/manifest/etcd.yaml<br>- --tls-cipher-suites=TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>- --tls-min-version=VersionTLS12 |
| SSL Medium Strength Cipher Suites Supported (SWEET32) | 42873 | lb1.cc.com | tcp/6443  [New 395] | New | Fixed | Fixed K8s API-Server SWEET32 |
| SSL Certificate Cannot Be Trusted | 51192 | core-svcs1.cc.com | tcp/25  [New 93]<br>tcp/6443  [New 94] | New | Accepted | Internal usage |
| SSL Certificate Cannot Be Trusted | 51192 | dolly1.cc.com | tcp/6443  [New 185]<br>tcp/10250  [New 186]<br>tcp/30626  [New 187] | New | Accpeted | Internal usage |
| SSL Certificate Cannot Be Trusted | 51192 | dolly4.cc.com | tcp/10250  [New 266]<br>tcp/30626  [New 267] | New | Accepted | Internal usage |
| SSL Certificate Cannot Be Trusted | 51192 | etcd1.cc.com | tcp/2379  [New 314]<br>tcp/2380  [New 315] | New | Accepted | Internal usage |
| SSL Certificate Cannot Be Trusted | 51192 | lb1.cc.com | tcp/25  [New 405]<br>tcp/6443  [New 406] | New | Accepted | Internal usage |
| SSL Self-Signed Certificate | 57582 | core-svcs1.cc.com | tcp/25  [New 99] | New | Accepted | Internal usage |
| SSL Self-Signed Certificate | 57582 | dolly1.cc.com | tcp/10250  [New 195] | New | Accepted | Internal usage |
| SSL Self-Signed Certificate | 57582 | dolly4.cc.com | tcp/10250  [New 273] | New | Accepted | Internal usage |
| SSL Self-Signed Certificate | 57582 | lb1.cc.com | tcp/25  [New 411] | New | Accepted | Internal usage |
| SSL/TLS Protocol Initialization Vector Implementation Information Disclosure Vulnerability (BEAST) | 58751 | core-svcs1.cc.com | tcp/25  [New 100] | New | Accepted | Internal usage |
| SSL/TLS Protocol Initialization Vector Implementation Information Disclosure Vulnerability (BEAST) | 58751 | dolly1.cc.com | tcp/30626  [New 196] | New | Accepted | kube-proxy: Internal usage |
| SSL/TLS Protocol Initialization Vector Implementation Information Disclosure Vulnerability (BEAST) | 58751 | dolly4.cc.com | tcp/30626  [New 274] | New | Accepted | kube-proxy: Internal usage |
| SSL/TLS Protocol Initialization Vector Implementation Information Disclosure Vulnerability (BEAST) | 58751 | lb1.cc.com | tcp/25  [New 412] | New | Fixed | nano /etc/postfix/main.cf<br><br>smtpd_tls_mandatory_protocols = !SSLv2,!SSLv3,!TLSv1<br>smtp_tls_mandatory_protocols  = !SSLv2,!SSLv3,!TLSv1<br>smtpd_tls_protocols           = !SSLv2,!SSLv3,!TLSv1<br>smtp_tls_protocols            = !SSLv2,!SSLv3,!TLSv1<br>smtpd_tls_security_level = encrypt<br>smtp_tls_security_level  = encrypt<br>smtpd_tls_exclude_ciphers = aNULL, LOW, EXP, MEDIUM, ADH, AECDH, MD5, DSS, ECDSA, CAMELLIA128, 3DES, CAMELLIA256,RSA+AES, eNULL |
| SSL Certificate with Wrong Hostname | 45411 | dolly1.cc.com | tcp/30626  [New 181] | New | Accepted | Internal usage |
| SSL Certificate with Wrong Hostname | 45411 | dolly4.cc.com | tcp/30626  [New 262] | New | Accepted | Internal usage |
#### Risk: Low (5) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| SSH Server CBC Mode Ciphers Enabled | 70658 | 10.0.1.222 | tcp/22  [New 12] | New | - | - |
| Web Server Transmits Cleartext Credentials | 26194 | core-svcs1.cc.com | tcp/8900  [New 71] | New | - | - |
| Web Server Transmits Cleartext Credentials | 26194 | lb1.cc.com | tcp/8900  [New 384] | New | - | - |
| SSL Anonymous Cipher Suites Supported | 31705 | core-svcs1.cc.com | tcp/25  [New 72] | New | - | - |
| SSL Anonymous Cipher Suites Supported | 31705 | lb1.cc.com | tcp/25  [New 385] | New | - | - |
#### Risk: None (398) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | 10.0.1.222 | icmp/0  [New 1] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | 10.0.1.5 | icmp/0  [New 15] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | core-svcs1.cc.com | icmp/0  [New 33] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | dolly1.cc.com | icmp/0  [New 126] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | dolly4.cc.com | icmp/0  [New 219] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | etcd1.cc.com | icmp/0  [New 290] | New | Accepted | - |
| ICMP Timestamp Request Remote Date Disclosure | 10114 | lb1.cc.com | icmp/0  [New 346] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | 10.0.1.222 | tcp/22  [New 2] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | core-svcs1.cc.com | tcp/22  [New 35] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | dolly1.cc.com | tcp/22  [New 127] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | dolly4.cc.com | tcp/22  [New 220] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | etcd1.cc.com | tcp/22  [New 291] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | jumpy0.cc.com | tcp/22  [New 332] | New | Accepted | - |
| SSH Server Type and Version Information | 10267 | lb1.cc.com | tcp/22  [New 348] | New | Accepted | - |
| Traceroute Information | 10287 | 10.0.1.222 | udp/0  [New 3] | New | Accepted | - |
| Traceroute Information | 10287 | 10.0.1.5 | udp/0  [New 16] | New | Accepted | - |
| Traceroute Information | 10287 | core-svcs1.cc.com | udp/0  [New 36] | New | Accepted | - |
| Traceroute Information | 10287 | dolly1.cc.com | udp/0  [New 128] | New | Accepted | - |
| Traceroute Information | 10287 | dolly4.cc.com | udp/0  [New 221] | New | Accepted | - |
| Traceroute Information | 10287 | etcd1.cc.com | udp/0  [New 292] | New | Accepted | - |
| Traceroute Information | 10287 | jumpy0.cc.com | udp/0  [New 333] | New | Accepted | - |
| Traceroute Information | 10287 | lb1.cc.com | udp/0  [New 349] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | 10.0.1.222 | tcp/22  [New 4] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | core-svcs1.cc.com | tcp/22  [New 42] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | dolly1.cc.com | tcp/22  [New 132] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | dolly4.cc.com | tcp/22  [New 224] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | etcd1.cc.com | tcp/22  [New 295] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | jumpy0.cc.com | tcp/22  [New 334] | New | Accepted | - |
| SSH Protocol Versions Supported | 10881 | lb1.cc.com | tcp/22  [New 355] | New | Accepted | - |
| Nessus SYN scanner | 11219 | 10.0.1.222 | tcp/22  [New 5] | New | Accepted | - |
| Nessus SYN scanner | 11219 | 10.0.1.5 | tcp/53  [New 20] | New | Accepted | - |
| Nessus SYN scanner | 11219 | core-svcs1.cc.com | tcp/22  [New 46]<br>tcp/25  [New 47]<br>tcp/53  [New 48]<br>tcp/6443  [New 49]<br>tcp/8060  [New 50]<br>tcp/8900  [New 51]<br>tcp/9094  [New 52] | New | Accepted | - |
| Nessus SYN scanner | 11219 | dolly1.cc.com | tcp/22  [New 133]<br>tcp/179  [New 134]<br>tcp/6443  [New 135]<br>tcp/10250  [New 136]<br>tcp/10251  [New 137]<br>tcp/10252  [New 138]<br>tcp/10256  [New 139]<br>tcp/30626  [New 140]<br>tcp/30820  [New 141]<br>tcp/31564  [New 142] | New | Accepted | - |
| Nessus SYN scanner | 11219 | dolly4.cc.com | tcp/22  [New 226]<br>tcp/179  [New 227]<br>tcp/10250  [New 228]<br>tcp/10256  [New 229]<br>tcp/30626  [New 230]<br>tcp/30820  [New 231]<br>tcp/31564  [New 232] | New | Accepted | - |
| Nessus SYN scanner | 11219 | etcd1.cc.com | tcp/22  [New 296]<br>tcp/2379  [New 297]<br>tcp/2380  [New 298] | New | Accepted | - |
| Nessus SYN scanner | 11219 | jumpy0.cc.com | tcp/22  [New 335] | New | Accepted | - |
| Nessus SYN scanner | 11219 | lb1.cc.com | tcp/22  [New 359]<br>tcp/25  [New 360]<br>tcp/53  [New 361]<br>tcp/6443  [New 362]<br>tcp/8060  [New 363]<br>tcp/8900  [New 364]<br>tcp/9094  [New 365] | New | Accepted | - |
| OS Identification | 11936 | 10.0.1.222 | tcp/0  [New 6] | New | Accepted | - |
| OS Identification | 11936 | 10.0.1.5 | tcp/0  [New 21] | New | Accepted | - |
| OS Identification | 11936 | core-svcs1.cc.com | tcp/0  [New 54] | New | Accepted | - |
| OS Identification | 11936 | dolly1.cc.com | tcp/0  [New 143] | New | Accepted | - |
| OS Identification | 11936 | dolly4.cc.com | tcp/0  [New 233] | New | Accepted | - |
| OS Identification | 11936 | etcd1.cc.com | tcp/0  [New 299] | New | Accepted | - |
| OS Identification | 11936 | lb1.cc.com | tcp/0  [New 367] | New | Accepted | - |
| Nessus Scan Information | 19506 | 10.0.1.222 | tcp/0  [New 7] | New | Accepted | - |
| Nessus Scan Information | 19506 | 10.0.1.5 | tcp/0  [New 22] | New | Accepted | - |
| Nessus Scan Information | 19506 | core-svcs1.cc.com | tcp/0  [New 58] | New | Accepted | - |
| Nessus Scan Information | 19506 | dolly1.cc.com | tcp/0  [New 146] | New | Accepted | - |
| Nessus Scan Information | 19506 | dolly4.cc.com | tcp/0  [New 236] | New | Accepted | - |
| Nessus Scan Information | 19506 | etcd1.cc.com | tcp/0  [New 302] | New | Accepted | - |
| Nessus Scan Information | 19506 | jumpy0.cc.com | tcp/0  [New 337] | New | Accepted | - |
| Nessus Scan Information | 19506 | lb1.cc.com | tcp/0  [New 371] | New | Accepted | - |
| Service Detection | 22964 | 10.0.1.222 | tcp/22  [New 8] | New | Accepted | - |
| Service Detection | 22964 | core-svcs1.cc.com | tcp/22  [New 61]<br>tcp/25  [New 62]<br>tcp/6443  [New 63]<br>tcp/6443  [New 64]<br>tcp/8060  [New 65]<br>tcp/8900  [New 66] | New | Accepted | - |
| Service Detection | 22964 | dolly1.cc.com | tcp/22  [New 150]<br>tcp/179  [New 151]<br>tcp/6443  [New 152]<br>tcp/6443  [New 153]<br>tcp/10250  [New 154]<br>tcp/10251  [New 155]<br>tcp/10252  [New 156]<br>tcp/10256  [New 157]<br>tcp/30626  [New 158]<br>tcp/30626  [New 159]<br>tcp/30820  [New 160]<br>tcp/31564  [New 161] | New | Accepted | - |
| Service Detection | 22964 | dolly4.cc.com | tcp/22  [New 239]<br>tcp/179  [New 240]<br>tcp/10250  [New 241]<br>tcp/10250  [New 242]<br>tcp/10256  [New 243]<br>tcp/30626  [New 244]<br>tcp/30626  [New 245]<br>tcp/30820  [New 246]<br>tcp/31564  [New 247] | New | Accepted | - |
| Service Detection | 22964 | etcd1.cc.com | tcp/22  [New 305]<br>tcp/2379  [New 306]<br>tcp/2380  [New 307] | New | Accepted | - |
| Service Detection | 22964 | jumpy0.cc.com | tcp/22  [New 338] | New | Accepted | - |
| Service Detection | 22964 | lb1.cc.com | tcp/22  [New 374]<br>tcp/25  [New 375]<br>tcp/6443  [New 376]<br>tcp/6443  [New 377]<br>tcp/8060  [New 378]<br>tcp/8900  [New 379] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | 10.0.1.222 | tcp/0  [New 9] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | 10.0.1.5 | tcp/0  [New 23] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | core-svcs1.cc.com | tcp/0  [New 70] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | dolly1.cc.com | tcp/0  [New 169] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | dolly4.cc.com | tcp/0  [New 253] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | etcd1.cc.com | tcp/0  [New 308] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | jumpy0.cc.com | tcp/0  [New 339] | New | Accepted | - |
| TCP/IP Timestamps Supported | 25220 | lb1.cc.com | tcp/0  [New 383] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | 10.0.1.222 | tcp/0  [New 10] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | 10.0.1.5 | tcp/0  [New 26] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | core-svcs1.cc.com | tcp/0  [New 87] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | dolly1.cc.com | tcp/0  [New 182] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | dolly4.cc.com | tcp/0  [New 263] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | etcd1.cc.com | tcp/0  [New 313] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | jumpy0.cc.com | tcp/0  [New 341] | New | Accepted | - |
| Common Platform Enumeration (CPE) | 45590 | lb1.cc.com | tcp/0  [New 399] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | 10.0.1.222 | tcp/22  [New 11] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | core-svcs1.cc.com | tcp/22  [New 104] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | dolly1.cc.com | tcp/22  [New 202] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | dolly4.cc.com | tcp/22  [New 278] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | etcd1.cc.com | tcp/22  [New 325] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | jumpy0.cc.com | tcp/22  [New 343] | New | Accepted | - |
| SSH Algorithms and Languages Supported | 70657 | lb1.cc.com | tcp/22  [New 416] | New | Accepted | - |
| No Credentials Provided | 110723 | 10.0.1.222 | tcp/0  [New 13] | New | Accepted | - |
| No Credentials Provided | 110723 | core-svcs1.cc.com | tcp/0  [New 120] | New | Accepted | - |
| No Credentials Provided | 110723 | dolly1.cc.com | tcp/0  [New 213] | New | Accepted | - |
| No Credentials Provided | 110723 | dolly4.cc.com | tcp/0  [New 287] | New | Accepted | - |
| No Credentials Provided | 110723 | etcd1.cc.com | tcp/0  [New 330] | New | Accepted | - |
| No Credentials Provided | 110723 | lb1.cc.com | tcp/0  [New 432] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | 10.0.1.222 | tcp/0  [New 14] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | core-svcs1.cc.com | tcp/0  [New 121] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | dolly1.cc.com | tcp/0  [New 214] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | dolly4.cc.com | tcp/0  [New 288] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | etcd1.cc.com | tcp/0  [New 331] | New | Accepted | - |
| Local Checks Not Enabled (info) | 117886 | lb1.cc.com | tcp/0  [New 433] | New | Accepted | - |
| Network Time Protocol (NTP) Server Detection | 10884 | 10.0.1.5 | udp/123  [New 17] | New | Accepted | - |
| DNS Server Detection | 11002 | 10.0.1.5 | tcp/53  [New 18]<br>udp/53  [New 19] | New | Accepted | - |
| DNS Server Detection | 11002 | core-svcs1.cc.com | tcp/53  [New 43]<br>udp/53  [New 44] | New | Accepted | - |
| DNS Server Detection | 11002 | lb1.cc.com | tcp/53  [New 356]<br>udp/53  [New 357] | New | Accepted | - |
| DNS Server hostname.bind Map Hostname Disclosure | 35371 | 10.0.1.5 | udp/53  [New 25] | New | Accepted | - |
| Device Type | 54615 | 10.0.1.5 | tcp/0  [New 27] | New | Accepted | - |
| Device Type | 54615 | dolly1.cc.com | tcp/0  [New 188] | New | Accepted | - |
| Device Type | 54615 | dolly4.cc.com | tcp/0  [New 268] | New | Accepted | - |
| Device Type | 54615 | etcd1.cc.com | tcp/0  [New 316] | New | Accepted | - |
| DNS Server Version Detection | 72779 | 10.0.1.5 | tcp/53  [New 28] | New | Accepted | - |
| DNS Server Version Detection | 72779 | core-svcs1.cc.com | tcp/53  [New 105] | New | Accepted | - |
| DNS Server Version Detection | 72779 | lb1.cc.com | tcp/53  [New 417] | New | Accepted | - |
| Unbound DNS Resolver Remote Version Detection | 87872 | 10.0.1.5 | tcp/53  [New 29] | New | Accepted | - |
| HTTP Server Type and Version | 10107 | core-svcs1.cc.com | tcp/8060  [New 31]<br>tcp/8900  [New 32] | New | Accepted | - |
| HTTP Server Type and Version | 10107 | dolly1.cc.com | tcp/30626  [New 124]<br>tcp/31564  [New 125] | New | Accepted | - |
| HTTP Server Type and Version | 10107 | dolly4.cc.com | tcp/30626  [New 217]<br>tcp/31564  [New 218] | New | Accepted | - |
| HTTP Server Type and Version | 10107 | lb1.cc.com | tcp/8060  [New 344]<br>tcp/8900  [New 345] | New | Accepted | - |
| SMTP Server Detection | 10263 | core-svcs1.cc.com | tcp/25  [New 34] | New | Accepted | - |
| SMTP Server Detection | 10263 | lb1.cc.com | tcp/25  [New 347] | New | Accepted | - |
| Web Server robots.txt Information Disclosure | 10302 | core-svcs1.cc.com | tcp/8900  [New 37] | New | Accepted | - |
| Web Server robots.txt Information Disclosure | 10302 | lb1.cc.com | tcp/8900  [New 350] | New | Accepted | - |
| Web Server No 404 Error Code Check | 10386 | core-svcs1.cc.com | tcp/8900  [New 38] | New | Accepted | - |
| Web Server No 404 Error Code Check | 10386 | lb1.cc.com | tcp/8900  [New 351] | New | Accepted | - |
| Web mirroring | 10662 | core-svcs1.cc.com | tcp/8900  [New 39] | New | Accepted | - |
| Web mirroring | 10662 | lb1.cc.com | tcp/8900  [New 352] | New | Accepted | - |
| SSL Certificate Information | 10863 | core-svcs1.cc.com | tcp/25  [New 40]<br>tcp/6443  [New 41] | New | Accepted | - |
| SSL Certificate Information | 10863 | dolly1.cc.com | tcp/6443  [New 129]<br>tcp/10250  [New 130]<br>tcp/30626  [New 131] | New | Accepted | - |
| SSL Certificate Information | 10863 | dolly4.cc.com | tcp/10250  [New 222]<br>tcp/30626  [New 223] | New | Accepted | - |
| SSL Certificate Information | 10863 | etcd1.cc.com | tcp/2379  [New 293]<br>tcp/2380  [New 294] | New | Accepted | - |
| SSL Certificate Information | 10863 | lb1.cc.com | tcp/25  [New 353]<br>tcp/6443  [New 354] | New | Accepted | - |
| Web Server Directory Enumeration | 11032 | core-svcs1.cc.com | tcp/8900  [New 45] | New | Accepted | - |
| Web Server Directory Enumeration | 11032 | dolly4.cc.com | tcp/10250  [New 225] | New | Accepted | - |
| Web Server Directory Enumeration | 11032 | lb1.cc.com | tcp/8900  [New 358] | New | Accepted | - |
| smtpscan SMTP Fingerprinting | 11421 | core-svcs1.cc.com | tcp/25  [New 53] | New | Accepted | - |
| smtpscan SMTP Fingerprinting | 11421 | lb1.cc.com | tcp/25  [New 366] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | core-svcs1.cc.com | tcp/0  [New 55] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | dolly1.cc.com | tcp/0  [New 144] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | dolly4.cc.com | tcp/0  [New 234] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | etcd1.cc.com | tcp/0  [New 300] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | jumpy0.cc.com | tcp/0  [New 336] | New | Accepted | - |
| Host Fully Qualified Domain Name (FQDN) Resolution | 12053 | lb1.cc.com | tcp/0  [New 368] | New | Accepted | - |
| IP Protocols Scan | 14788 | core-svcs1.cc.com | tcp/0  [New 57] | New | Accepted | - |
| IP Protocols Scan | 14788 | dolly1.cc.com | tcp/0  [New 145] | New | Accepted | - |
| IP Protocols Scan | 14788 | dolly4.cc.com | tcp/0  [New 235] | New | Accepted | - |
| IP Protocols Scan | 14788 | etcd1.cc.com | tcp/0  [New 301] | New | Accepted | - |
| IP Protocols Scan | 14788 | lb1.cc.com | tcp/0  [New 370] | New | Accepted | - |
| SSL Cipher Suites Supported | 21643 | core-svcs1.cc.com | tcp/25  [New 59]<br>tcp/6443  [New 60] | New | Accepted | - |
| SSL Cipher Suites Supported | 21643 | dolly1.cc.com | tcp/6443  [New 147]<br>tcp/10250  [New 148]<br>tcp/30626  [New 149] | New | Accepted | - |
| SSL Cipher Suites Supported | 21643 | dolly4.cc.com | tcp/10250  [New 237]<br>tcp/30626  [New 238] | New | Accepted | - |
| SSL Cipher Suites Supported | 21643 | etcd1.cc.com | tcp/2379  [New 303]<br>tcp/2380  [New 304] | New | Accepted | - |
| SSL Cipher Suites Supported | 21643 | lb1.cc.com | tcp/25  [New 372]<br>tcp/6443  [New 373] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Information | 24260 | core-svcs1.cc.com | tcp/6443  [New 67]<br>tcp/8060  [New 68]<br>tcp/8900  [New 69] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Information | 24260 | dolly1.cc.com | tcp/6443  [New 162]<br>tcp/10251  [New 163]<br>tcp/10252  [New 164]<br>tcp/10256  [New 165]<br>tcp/30626  [New 166]<br>tcp/30820  [New 167]<br>tcp/31564  [New 168] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Information | 24260 | dolly4.cc.com | tcp/10250  [New 248]<br>tcp/10256  [New 249]<br>tcp/30626  [New 250]<br>tcp/30820  [New 251]<br>tcp/31564  [New 252] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Information | 24260 | lb1.cc.com | tcp/6443  [New 380]<br>tcp/8060  [New 381]<br>tcp/8900  [New 382] | New | Accepted | - |
| CGI Generic Tests Load Estimation (all tests) | 33817 | core-svcs1.cc.com | tcp/8900  [New 73] | New | Accepted | - |
| CGI Generic Tests Load Estimation (all tests) | 33817 | lb1.cc.com | tcp/8900  [New 386] | New | Accepted | - |
| SSL Service Requests Client Certificate | 35297 | core-svcs1.cc.com | tcp/6443  [New 74] | New | Accepted | - |
| SSL Service Requests Client Certificate | 35297 | dolly1.cc.com | tcp/6443  [New 170]<br>tcp/10250  [New 171] | New | Accepted | - |
| SSL Service Requests Client Certificate | 35297 | dolly4.cc.com | tcp/10250  [New 254] | New | Accepted | - |
| SSL Service Requests Client Certificate | 35297 | etcd1.cc.com | tcp/2379  [New 309]<br>tcp/2380  [New 310] | New | Accepted | - |
| SSL Service Requests Client Certificate | 35297 | lb1.cc.com | tcp/6443  [New 387] | New | Accepted | - |
| CGI Generic Tests Timeout | 39470 | core-svcs1.cc.com | tcp/8900  [New 75] | New | Accepted | - |
| CGI Generic Tests Timeout | 39470 | lb1.cc.com | tcp/8900  [New 388] | New | Accepted | - |
| Backported Security Patch Detection (SSH) | 39520 | core-svcs1.cc.com | tcp/22  [New 76] | New | Accepted | - |
| Backported Security Patch Detection (SSH) | 39520 | jumpy0.cc.com | tcp/22  [New 340] | New | Accepted | - |
| Backported Security Patch Detection (SSH) | 39520 | lb1.cc.com | tcp/22  [New 389] | New | Accepted | - |
| CGI Generic Tests HTTP Errors | 40406 | core-svcs1.cc.com | tcp/8900  [New 77] | New | Accepted | - |
| CGI Generic Tests HTTP Errors | 40406 | lb1.cc.com | tcp/8900  [New 390] | New | Accepted | - |
| Web Server Allows Password Auto-Completion | 42057 | core-svcs1.cc.com | tcp/8900  [New 78] | New | Accepted | - |
| Web Server Allows Password Auto-Completion | 42057 | lb1.cc.com | tcp/8900  [New 391] | New | Accepted | - |
| SMTP Service STARTTLS Command Support | 42088 | core-svcs1.cc.com | tcp/25  [New 79] | New | Accepted | - |
| SMTP Service STARTTLS Command Support | 42088 | lb1.cc.com | tcp/25  [New 392] | New | Accepted | - |
| Strict Transport Security (STS) Detection | 42822 | core-svcs1.cc.com | tcp/8900  [New 80] | New | Accepted | - |
| Strict Transport Security (STS) Detection | 42822 | lb1.cc.com | tcp/8900  [New 393] | New | Accepted | - |
| Non-compliant Strict Transport Security (STS) | 42823 | core-svcs1.cc.com | tcp/8900  [New 81] | New | Accepted | - |
| Non-compliant Strict Transport Security (STS) | 42823 | lb1.cc.com | tcp/8900  [New 394] | New | Accepted | - |
| HTTP Methods Allowed (per directory) | 43111 | core-svcs1.cc.com | tcp/8060  [New 83]<br>tcp/8900  [New 84] | New | Accepted | - |
| HTTP Methods Allowed (per directory) | 43111 | dolly1.cc.com | tcp/10251  [New 174]<br>tcp/10252  [New 175]<br>tcp/10256  [New 176]<br>tcp/30626  [New 177]<br>tcp/30820  [New 178]<br>tcp/31564  [New 179] | New | Accepted | - |
| HTTP Methods Allowed (per directory) | 43111 | dolly4.cc.com | tcp/10250  [New 256]<br>tcp/10256  [New 257]<br>tcp/30626  [New 258]<br>tcp/30820  [New 259]<br>tcp/31564  [New 260] | New | Accepted | - |
| HTTP Methods Allowed (per directory) | 43111 | lb1.cc.com | tcp/8060  [New 396]<br>tcp/8900  [New 397] | New | Accepted | - |
| SSL Certificate 'commonName' Mismatch | 45410 | core-svcs1.cc.com | tcp/25  [New 85]<br>tcp/6443  [New 86] | New | Accepted | - |
| SSL Certificate 'commonName' Mismatch | 45410 | dolly1.cc.com | tcp/30626  [New 180] | New | Accepted | - |
| SSL Certificate 'commonName' Mismatch | 45410 | dolly4.cc.com | tcp/30626  [New 261] | New | Accepted | - |
| SSL Certificate 'commonName' Mismatch | 45410 | lb1.cc.com | tcp/25  [New 398] | New | Accepted | - |
| CGI Generic Injectable Parameter | 47830 | core-svcs1.cc.com | tcp/8900  [New 88] | New | Accepted | - |
| CGI Generic Injectable Parameter | 47830 | lb1.cc.com | tcp/8900  [New 400] | New | Accepted | - |
| External URLs | 49704 | core-svcs1.cc.com | tcp/8900  [New 89] | New | Accepted | - |
| External URLs | 49704 | lb1.cc.com | tcp/8900  [New 401] | New | Accepted | - |
| Web Server Harvested Email Addresses | 49705 | core-svcs1.cc.com | tcp/8900  [New 90] | New | Accepted | - |
| Web Server Harvested Email Addresses | 49705 | lb1.cc.com | tcp/8900  [New 402] | New | Accepted | - |
| Missing or Permissive Content-Security-Policy frame-ancestors HTTP Response Header | 50344 | core-svcs1.cc.com | tcp/8900  [New 91] | New | Accepted | - |
| Missing or Permissive Content-Security-Policy frame-ancestors HTTP Response Header | 50344 | lb1.cc.com | tcp/8900  [New 403] | New | Accepted | - |
| OpenSSL Detection | 50845 | core-svcs1.cc.com | tcp/25  [New 92] | New | Accepted | - |
| OpenSSL Detection | 50845 | dolly1.cc.com | tcp/30626  [New 184] | New | Accepted | - |
| OpenSSL Detection | 50845 | dolly4.cc.com | tcp/30626  [New 265] | New | Accepted | - |
| OpenSSL Detection | 50845 | lb1.cc.com | tcp/25  [New 404] | New | Accepted | - |
| SSL / TLS Versions Supported | 56984 | core-svcs1.cc.com | tcp/25  [New 95]<br>tcp/6443  [New 96] | New | Accepted | - |
| SSL / TLS Versions Supported | 56984 | dolly1.cc.com | tcp/6443  [New 189]<br>tcp/10250  [New 190]<br>tcp/30626  [New 191] | New | Accepted | - |
| SSL / TLS Versions Supported | 56984 | dolly4.cc.com | tcp/10250  [New 269]<br>tcp/30626  [New 270] | New | Accepted | - |
| SSL / TLS Versions Supported | 56984 | etcd1.cc.com | tcp/2379  [New 317]<br>tcp/2380  [New 318] | New | Accepted | - |
| SSL / TLS Versions Supported | 56984 | lb1.cc.com | tcp/25  [New 407]<br>tcp/6443  [New 408] | New | Accepted | - |
| SSL Perfect Forward Secrecy Cipher Suites Supported | 57041 | core-svcs1.cc.com | tcp/25  [New 97]<br>tcp/6443  [New 98] | New | Accepted | - |
| SSL Perfect Forward Secrecy Cipher Suites Supported | 57041 | dolly1.cc.com | tcp/6443  [New 192]<br>tcp/10250  [New 193]<br>tcp/30626  [New 194] | New | Accepted | - |
| SSL Perfect Forward Secrecy Cipher Suites Supported | 57041 | dolly4.cc.com | tcp/10250  [New 271]<br>tcp/30626  [New 272] | New | Accepted | - |
| SSL Perfect Forward Secrecy Cipher Suites Supported | 57041 | etcd1.cc.com | tcp/2379  [New 319]<br>tcp/2380  [New 320] | New | Accepted | - |
| SSL Perfect Forward Secrecy Cipher Suites Supported | 57041 | lb1.cc.com | tcp/25  [New 409]<br>tcp/6443  [New 410] | New | Accepted | - |
| TLS Next Protocols Supported | 62564 | core-svcs1.cc.com | tcp/6443  [New 101] | New | Accepted | - |
| TLS Next Protocols Supported | 62564 | dolly1.cc.com | tcp/6443  [New 197]<br>tcp/10250  [New 198] | New | Accepted | - |
| TLS Next Protocols Supported | 62564 | dolly4.cc.com | tcp/10250  [New 275] | New | Accepted | - |
| TLS Next Protocols Supported | 62564 | etcd1.cc.com | tcp/2379  [New 321]<br>tcp/2380  [New 322] | New | Accepted | - |
| TLS Next Protocols Supported | 62564 | lb1.cc.com | tcp/6443  [New 413] | New | Accepted | - |
| SSL Cipher Block Chaining Cipher Suites Supported | 70544 | core-svcs1.cc.com | tcp/25  [New 102]<br>tcp/6443  [New 103] | New | Accepted | - |
| SSL Cipher Block Chaining Cipher Suites Supported | 70544 | dolly1.cc.com | tcp/6443  [New 199]<br>tcp/10250  [New 200]<br>tcp/30626  [New 201] | New | Accepted | - |
| SSL Cipher Block Chaining Cipher Suites Supported | 70544 | dolly4.cc.com | tcp/10250  [New 276]<br>tcp/30626  [New 277] | New | Accepted | - |
| SSL Cipher Block Chaining Cipher Suites Supported | 70544 | etcd1.cc.com | tcp/2379  [New 323]<br>tcp/2380  [New 324] | New | Accepted | - |
| SSL Cipher Block Chaining Cipher Suites Supported | 70544 | lb1.cc.com | tcp/25  [New 414]<br>tcp/6443  [New 415] | New | Accepted | - |
| HSTS Missing From HTTPS Server | 84502 | core-svcs1.cc.com | tcp/6443  [New 106] | New | Accepted | - |
| HSTS Missing From HTTPS Server | 84502 | dolly1.cc.com | tcp/6443  [New 203]<br>tcp/30626  [New 204] | New | Accepted | - |
| HSTS Missing From HTTPS Server | 84502 | dolly4.cc.com | tcp/10250  [New 279]<br>tcp/30626  [New 280] | New | Accepted | - |
| HSTS Missing From HTTPS Server | 84502 | lb1.cc.com | tcp/6443  [New 418] | New | Accepted | - |
| TLS ALPN Supported Protocol Enumeration | 84821 | core-svcs1.cc.com | tcp/6443  [New 107] | New | Accepted | - |
| TLS ALPN Supported Protocol Enumeration | 84821 | dolly1.cc.com | tcp/6443  [New 205]<br>tcp/10250  [New 206]<br>tcp/30626  [New 207] | New | Accepted | - |
| TLS ALPN Supported Protocol Enumeration | 84821 | dolly4.cc.com | tcp/10250  [New 281]<br>tcp/30626  [New 282] | New | Accepted | - |
| TLS ALPN Supported Protocol Enumeration | 84821 | etcd1.cc.com | tcp/2379  [New 326]<br>tcp/2380  [New 327] | New | Accepted | - |
| TLS ALPN Supported Protocol Enumeration | 84821 | lb1.cc.com | tcp/6443  [New 419] | New | Accepted | - |
| Web Application Cookies Not Marked Secure | 85602 | core-svcs1.cc.com | tcp/6443  [New 108]<br>tcp/8060  [New 109]<br>tcp/8900  [New 110] | New | Accepted | - |
| Web Application Cookies Not Marked Secure | 85602 | lb1.cc.com | tcp/6443  [New 420]<br>tcp/8060  [New 421]<br>tcp/8900  [New 422] | New | Accepted | - |
| TLS NPN Supported Protocol Enumeration | 87242 | core-svcs1.cc.com | tcp/6443  [New 111] | New | Accepted | - |
| TLS NPN Supported Protocol Enumeration | 87242 | dolly1.cc.com | tcp/6443  [New 209]<br>tcp/10250  [New 210] | New | Accepted | - |
| TLS NPN Supported Protocol Enumeration | 87242 | dolly4.cc.com | tcp/10250  [New 284] | New | Accepted | - |
| TLS NPN Supported Protocol Enumeration | 87242 | etcd1.cc.com | tcp/2379  [New 328]<br>tcp/2380  [New 329] | New | Accepted | - |
| TLS NPN Supported Protocol Enumeration | 87242 | lb1.cc.com | tcp/6443  [New 423] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Redirect Information | 91634 | core-svcs1.cc.com | tcp/8900  [New 112] | New | Accepted | - |
| HyperText Transfer Protocol (HTTP) Redirect Information | 91634 | lb1.cc.com | tcp/8900  [New 424] | New | Accepted | - |
| Web Application Sitemap | 91815 | core-svcs1.cc.com | tcp/8900  [New 113] | New | Accepted | - |
| Web Application Sitemap | 91815 | lb1.cc.com | tcp/8900  [New 425] | New | Accepted | - |
| Web Application Cookies Are Expired | 100669 | core-svcs1.cc.com | tcp/6443  [New 114]<br>tcp/8060  [New 115]<br>tcp/8900  [New 116] | New | Accepted | - |
| Web Application Cookies Are Expired | 100669 | lb1.cc.com | tcp/6443  [New 426]<br>tcp/8060  [New 427]<br>tcp/8900  [New 428] | New | Accepted | - |
| TLS Version 1.0 Protocol Detection | 104743 | core-svcs1.cc.com | tcp/25  [New 117] | New | Accepted | - |
| TLS Version 1.0 Protocol Detection | 104743 | dolly1.cc.com | tcp/30626  [New 212] | New | Accepted | - |
| TLS Version 1.0 Protocol Detection | 104743 | dolly4.cc.com | tcp/30626  [New 286] | New | Accepted | - |
| TLS Version 1.0 Protocol Detection | 104743 | lb1.cc.com | tcp/25  [New 429] | New | Accepted | - |
| nginx HTTP Server Detection | 106375 | core-svcs1.cc.com | tcp/8060  [New 118]<br>tcp/8900  [New 119] | New | Accepted | - |
| nginx HTTP Server Detection | 106375 | lb1.cc.com | tcp/8060  [New 430]<br>tcp/8900  [New 431] | New | Accepted | - |
| TLS Version 1.1 Protocol Detection | 121010 | core-svcs1.cc.com | tcp/25  [New 122] | New | Accepted | - |
| TLS Version 1.1 Protocol Detection | 121010 | dolly1.cc.com | tcp/30626  [New 215] | New | Accepted | - |
| TLS Version 1.1 Protocol Detection | 121010 | dolly4.cc.com | tcp/30626  [New 289] | New | Accepted | - |
| TLS Version 1.1 Protocol Detection | 121010 | lb1.cc.com | tcp/25  [New 434] | New | Accepted | - |
| Kubernetes Web API Detection | 121471 | core-svcs1.cc.com | tcp/6443  [New 123] | New | Accepted | - |
| Kubernetes Web API Detection | 121471 | dolly1.cc.com | tcp/6443  [New 216] | New | Accepted | - |
| Kubernetes Web API Detection | 121471 | lb1.cc.com | tcp/6443  [New 435] | New | Accepted | - |
| Additional DNS Hostnames | 46180 | dolly1.cc.com | tcp/0  [New 183] | New | Accepted | - |
| Additional DNS Hostnames | 46180 | dolly4.cc.com | tcp/0  [New 264] | New | Accepted | - |
| HTTP/2 Cleartext Detection | 85805 | dolly1.cc.com | tcp/31564  [New 208] | New | Accepted | - |
| HTTP/2 Cleartext Detection | 85805 | dolly4.cc.com | tcp/31564  [New 283] | New | Accepted | - |
| SSL Root Certification Authority Certificate Information | 94761 | dolly1.cc.com | tcp/10250  [New 211] | New | Accepted | - |
| SSL Root Certification Authority Certificate Information | 94761 | dolly4.cc.com | tcp/10250  [New 285] | New | Accepted | - |
| OS Identification Failed | 50350 | jumpy0.cc.com | tcp/0  [New 342] | New | Accepted | - |

---

### Removed Vulnerabilities (None: 1, Low: 0, Critical: 0, Medium: 0)
#### Risk: High (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: Medium (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: Low (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: None (1) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | -/-  [Old 1] | Removed | - | - |

---

### Same Vulnerabilities (None: 0, Low: 0, Critical: 0, Medium: 0)
#### Risk: High (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: Medium (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: Low (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |
#### Risk: None (0) 
| Vulnerability | Plugin ID | Host | Affected Port(s) + [File Row]| Status | Action | Comments |
| --- | --- | --- | --- | --- | --- | --- |
| - | - | - | - | - | - | - |

---

