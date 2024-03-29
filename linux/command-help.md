# Linux命令行操作
## all
### 查看硬件信息
#### 查看CPU信息
```bash
lscpu
```
```
Architecture:          x86_64                 # CPU架构
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian          # 小尾序
CPU(s):                48                     # 总共更有48个核
On-line CPU(s) list:   0-47
Thread(s) per core:    2                      # 每个CPU核，只能支持2个线程
Core(s) per socket:    12                     # 每个CPU有12个核
Socket(s):             2                      # 总共有2个CPU
NUMA node(s):          2
Vendor ID:             GenuineIntel           # CPU生产厂商 Intel
CPU family:            6
Model:                 62
Model name:            Intel(R) Xeon(R) CPU E5-2695 v2 @ 2.40GHz
Stepping:              4
CPU MHz:               1330.810
CPU max MHz:           3200.0000
CPU min MHz:           1200.0000
BogoMIPS:              4799.96
Virtualization:        VT-x                   # 支持CPU虚拟化技术
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              30720K
NUMA node0 CPU(s):     0,2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46
NUMA node1 CPU(s):     1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm pcid dca sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid fsgsbase smep erms xsaveopt dtherm ida arat pln pts md_clear spec_ctrl intel_stibp flush_l1d
```
#### 查看磁盘信息
```bash
lsblk
```
```
NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                   8:0    0  3.7T  0 disk
├─sda1                8:1    0    1M  0 part
├─sda2                8:2    0    1G  0 part /boot
└─sda3                8:3    0  3.7T  0 part
  ├─centos_sun-root 253:0    0   50G  0 lvm  /
  ├─centos_sun-swap 253:1    0 23.6G  0 lvm  [SWAP]
  └─centos_sun-home 253:2    0  3.6T  0 lvm  /home
```

## centos

## ubuntu
