# Web management Huawei OLT MA5683 and MA5603
### version 1.0
Installation is described here [install/install.md ](install/install.md)  

### Description
For subscribers, the vlan per user scheme is used.
Certain ranges of vlans have been selected for QnQ and for clients.
For QnQ, we use vlans (top tag Svlan) from 2501 to 2512 (for example).
For clients, we will use 1024 vlans (lower tag Cvlan) from 2100 to 3123 (this number of line-profiles will be created).
The service port will be formed as follows:
```
service = ont_id + 128 * port_id + 4096 * slot_id
```
Cvlan data will be generated in this way:
```
vlan = ont_id + 2100 + 128 * port_id - (port_id % 7)*1024
```
Svlan will be taken from the database.
*It is possible to use a smaller number of Cvlans - for example, issue a different Svlan to each gpon port.
In this case, 128 Cvlans will be used.
The formulas will need to be changed to suit you.
It will not be possible to use one Svlan for all chassis, since we are limited by the number of line-profiles that can be created on a chassis.*
For understanding, here is a table with the data that will be generated:

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 0-0 | 2501 | 2100 | 2227 | 0 | 127 |
| slot 0-1 | 2501 | 2228 | 2355 | 128 | 255 |
| slot 0-2 | 2501 | 2356 | 2483 | 256 | 383 |
| slot 0-3 | 2501 | 2484 | 2611 | 384 | 511 |
| slot 0-4 | 2501 | 2612 | 2739 | 512 | 639 |
| slot 0-5 | 2501 | 2740 | 2867 | 640 | 767 |
| slot 0-6 | 2501 | 2868 | 2995 | 768 | 895 |
| slot 0-7 | 2501 | 2996 | 3123 | 896 | 1023 |
| slot 0-8 | 2502 | 2100 | 2227 | 1024 | 1151 |
| slot 0-9 | 2502 | 2228 | 2355 | 1152 | 1279 |
| slot 0-10 | 2502 | 2356 | 2483 | 1280 | 1407 |
| slot 0-11 | 2502 | 2484 | 2611 | 1408 | 1535 |
| slot 0-12 | 2502 | 2612 | 2739 | 1536 | 1663 |
| slot 0-13 | 2502 | 2740 | 2867 | 1664 | 1791 |
| slot 0-14 | 2502 | 2868 | 2995 | 1792 | 1919 |
| slot 0-15 | 2502 | 2996 | 3123 | 1920 | 2047 |

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 1-0 | 2503 | 2100 | 2227 | 4096 | 4223 |
| slot 1-1 | 2503 | 2228 | 2355 | 4224 | 4351 |
| slot 1-2 | 2503 | 2356 | 2483 | 4352 | 4479 |
| slot 1-3 | 2503 | 2484 | 2611 | 4480 | 4607 |
| slot 1-4 | 2503 | 2612 | 2739 | 4608 | 4735 |
| slot 1-5 | 2503 | 2740 | 2867 | 4736 | 4863 |
| slot 1-6 | 2503 | 2868 | 2995 | 4864 | 4991 |
| slot 1-7 | 2503 | 2996 | 3123 | 4992 | 5119 |
| slot 1-8 | 2504 | 2100 | 2227 | 5120 | 5247 |
| slot 1-9 | 2504 | 2228 | 2355 | 5248 | 5375 |
| slot 1-10 | 2504 | 2356 | 2483 | 5376 | 5503 |
| slot 1-11 | 2504 | 2484 | 2611 | 5504 | 5631 |
| slot 1-12 | 2504 | 2612 | 2739 | 5632 | 5759 |
| slot 1-13 | 2504 | 2740 | 2867 | 5760 | 5887 |
| slot 1-14 | 2504 | 2868 | 2995 | 5888 | 6015 |
| slot 1-15 | 2504 | 2996 | 3123 | 6016 | 6143 |

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 2-0 | 2505 | 2100 | 2227 | 8192 | 8319 |
| slot 2-1 | 2505 | 2228 | 2355 | 8320 | 8447 |
| slot 2-2 | 2505 | 2356 | 2483 | 8448 | 8575 |
| slot 2-3 | 2505 | 2484 | 2611 | 8576 | 8703 |
| slot 2-4 | 2505 | 2612 | 2739 | 8704 | 8831 |
| slot 2-5 | 2505 | 2740 | 2867 | 8832 | 8959 |
| slot 2-6 | 2505 | 2868 | 2995 | 8960 | 9087 |
| slot 2-7 | 2505 | 2996 | 3123 | 9088 | 9215 |
| slot 2-8 | 2506 | 2100 | 2227 | 9216 | 9343 |
| slot 2-9 | 2506 | 2228 | 2355 | 9344 | 9471 |
| slot 2-10 | 2506 | 2356 | 2483 | 9472 | 9599 |
| slot 2-11 | 2506 | 2484 | 2611 | 9600 | 9727 |
| slot 2-12 | 2506 | 2612 | 2739 | 9728 | 9855 |
| slot 2-13 | 2506 | 2740 | 2867 | 9856 | 9983 |
| slot 2-14 | 2506 | 2868 | 2995 | 9984 | 10111 |
| slot 2-15 | 2506 | 2996 | 3123 | 10112 | 10239 |

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 3-0 | 2507 | 2100 | 2227 | 12288 | 12415 |
| slot 3-1 | 2507 | 2228 | 2355 | 12416 | 12543 |
| slot 3-2 | 2507 | 2356 | 2483 | 12544 | 12671 |
| slot 3-3 | 2507 | 2484 | 2611 | 12672 | 12799 |
| slot 3-4 | 2507 | 2612 | 2739 | 12800 | 12927 |
| slot 3-5 | 2507 | 2740 | 2867 | 12928 | 13055 |
| slot 3-6 | 2507 | 2868 | 2995 | 13056 | 13183 |
| slot 3-7 | 2507 | 2996 | 3123 | 13184 | 13311 |
| slot 3-8 | 2508 | 2100 | 2227 | 13312 | 13439 |
| slot 3-9 | 2508 | 2228 | 2355 | 13440 | 13567 |
| slot 3-10 | 2508 | 2356 | 2483 | 13568 | 13695 |
| slot 3-11 | 2508 | 2484 | 2611 | 13696 | 13823 |
| slot 3-12 | 2508 | 2612 | 2739 | 13824 | 13951 |
| slot 3-13 | 2508 | 2740 | 2867 | 13952 | 14079 |
| slot 3-14 | 2508 | 2868 | 2995 | 14080 | 14207 |
| slot 3-15 | 2508 | 2996 | 3123 | 14208 | 14335 |

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 4-0 | 2509 | 2100 | 2227 | 16384 | 16511 |
| slot 4-1 | 2509 | 2228 | 2355 | 16512 | 16639 |
| slot 4-2 | 2509 | 2356 | 2483 | 16640 | 16767 |
| slot 4-3 | 2509 | 2484 | 2611 | 16768 | 16895 |
| slot 4-4 | 2509 | 2612 | 2739 | 16896 | 17023 |
| slot 4-5 | 2509 | 2740 | 2867 | 17024 | 17151 |
| slot 4-6 | 2509 | 2868 | 2995 | 17152 | 17279 |
| slot 4-7 | 2509 | 2996 | 3123 | 17280 | 17407 |
| slot 4-8 | 2510 | 2100 | 2227 | 17408 | 17535 |
| slot 4-9 | 2510 | 2228 | 2355 | 17536 | 17663 |
| slot 4-10 | 2510 | 2356 | 2483 | 17664 | 17791 |
| slot 4-11 | 2510 | 2484 | 2611 | 17792 | 17919 |
| slot 4-12 | 2510 | 2612 | 2739 | 17920 | 18047 |
| slot 4-13 | 2510 | 2740 | 2867 | 18048 | 18175 |
| slot 4-14 | 2510 | 2868 | 2995 | 18176 | 18303 |
| slot 4-15 | 2510 | 2996 | 3123 | 18304 | 18431 |

| gpon port | QnQ Svlan | Cvlan users start | Cvlan users end | Service ports start | Service ports end |
| - | - | - | - | - | - |
| slot 5-0 | 2511 | 2100 | 2227 | 20480 | 20607 |
| slot 5-1 | 2511 | 2228 | 2355 | 20608 | 20735 |
| slot 5-2 | 2511 | 2356 | 2483 | 20736 | 20863 |
| slot 5-3 | 2511 | 2484 | 2611 | 20864 | 20991 |
| slot 5-4 | 2511 | 2612 | 2739 | 20992 | 21119 |
| slot 5-5 | 2511 | 2740 | 2867 | 21120 | 21247 |
| slot 5-6 | 2511 | 2868 | 2995 | 21248 | 21375 |
| slot 5-7 | 2511 | 2996 | 3123 | 21376 | 21503 |
| slot 5-8 | 2512 | 2100 | 2227 | 21504 | 21631 |
| slot 5-9 | 2512 | 2228 | 2355 | 21632 | 21759 |
| slot 5-10 | 2512 | 2356 | 2483 | 21760 | 21887 |
| slot 5-11 | 2512 | 2484 | 2611 | 21888 | 22015 |
| slot 5-12 | 2512 | 2612 | 2739 | 22016 | 22143 |
| slot 5-13 | 2512 | 2740 | 2867 | 22144 | 22271 |
| slot 5-14 | 2512 | 2868 | 2995 | 22272 | 22399 |
| slot 5-15 | 2512 | 2996 | 3123 | 22400 | 22527 |

## Thanks for the inspiration
https://local.com.ua/forum/topic/89222-huawei-ma5683t-oid-%D0%B8-mib/  
https://github.com/explicitnull/h-ont-activator  
https://gpon.kou.li/huawei/olt/snmp  
https://xakinfo.ru/files/mibs.txt  
https://pastebin.com/wjj68SUX  
https://pastebin.com/kS9s2Qcp  
