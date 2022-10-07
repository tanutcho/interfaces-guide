# VISTEC DGX Cluster

[https://scads.ist.vistec.ac.th/cluster/system/](https://scads.ist.vistec.ac.th/cluster/system/)

### ตรวจสอบว่า PID จาก container ไหนใช้ GPUs

```bash
brain2@IST-DGX02:~$ nvidia-smi
Tue Apr 26 18:48:10 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.119.03   Driver Version: 450.119.03   CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla V100-SXM2...  On   | 00000000:06:00.0 Off |                    0 |
| N/A   29C    P0    46W / 163W |   3884MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  Tesla V100-SXM2...  On   | 00000000:07:00.0 Off |                    0 |
| N/A   30C    P0    51W / 163W |   4837MiB / 32510MiB |     25%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  Tesla V100-SXM2...  On   | 00000000:0A:00.0 Off |                    0 |
| N/A   31C    P0    48W / 163W |   4574MiB / 32510MiB |     11%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   3  Tesla V100-SXM2...  On   | 00000000:0B:00.0 Off |                    0 |
| N/A   28C    P0    44W / 163W |  31243MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   4  Tesla V100-SXM2...  On   | 00000000:85:00.0 Off |                    0 |
| N/A   27C    P0    44W / 163W |  31121MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   5  Tesla V100-SXM2...  On   | 00000000:86:00.0 Off |                    0 |
| N/A   29C    P0    44W / 163W |  31379MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   6  Tesla V100-SXM2...  On   | 00000000:89:00.0 Off |                    0 |
| N/A   32C    P0    46W / 163W |  30968MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   7  Tesla V100-SXM2...  On   | 00000000:8A:00.0 Off |                    0 |
| N/A   28C    P0    53W / 163W |  31136MiB / 32510MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A   2750430      C   ...envs/ppg_apnea/bin/python     1791MiB |
|    1   N/A  N/A   3086677      C   /usr/bin/python3                 2966MiB |
|    2   N/A  N/A   1732733      C   /usr/bin/python3                 1559MiB |
|    7   N/A  N/A   3286632      C   /usr/bin/python3                30519MiB |
+-----------------------------------------------------------------------------+
```

Exsample:

```bash
PID=1732733 ; docker ps --no-trunc | grep $(cat /proc/$PID/cgroup | grep -oE '[0-9a-f]{64}' | head -1) | sed 's/^.* //'
```

Result:

```bash
brain2@IST-DGX02:~$ PID=1732733 ; docker ps --no-trunc | grep $(cat /proc/$PID/cgroup | grep -oE '[0-9a-f]{64}' | head -1) | sed 's/^.* //'
narin-jupyter4
```
