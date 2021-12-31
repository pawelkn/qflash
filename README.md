# Quectel QFlash for Linux and Android V2.0.0

Qflash, a command line upgrade tool for quectel devices.

## File Directory Tree

> If firehose directory does not exist, firehose cannot be used.
>
> If fastboot directory does not exist, fastboot cannot be used.
>

## QFlash Help Message

### Fastboot Upgrade Method

fastboot can be called when using '-m 0' (default) and '-m 2'. The difference is at the earlier process of upgrade. The '-m 0' uses sahara to get need boot files however '-m 2' using AT command to come into 'fastboot' mode and then do fastboot upgrade. The '-m 2' will save much more time than '-m 0'.

### Firehose Upgrade Method

Users want to upgrade in this way need to remove qcserial module or remove '05c6:9008' from qcserial.c.

```bash
root@ubuntu:# ./QFlash -h
[12-31_01:28:08:847] QFlash Version: LTE&LTE-A_QFlash_Linux&Android_V2.0.0
[12-31_01:28:08:847] Builded at: Dec 31 2021 01:24:53
[12-31_01:28:08:946] Host runtime enviroment check ok
[12-31_01:28:08:947] 
[12-31_01:28:08:947] The CPU is little endian
[12-31_01:28:08:947] 
[12-31_01:28:08:947] ./QFlash [fastboot|firehose] [options...]
[12-31_01:28:08:947] [protocol]
[12-31_01:28:08:947]     fastboot                                 Use fastboot upgrade protocol
[12-31_01:28:08:947]     firehose                                 Use firehose upgrade protocol
[12-31_01:28:08:947] [parameters]
[12-31_01:28:08:947]     -f [package_path]                        Upgrade package path
[12-31_01:28:08:947]     -p [ttyUSBX]                             Diagnoise port, will auto-detect if not specified
[12-31_01:28:08:947]     -m [mode]                                Qflash upgrade method
[12-31_01:28:08:947]                                              method = 1 --> streaming download protocol
[12-31_01:28:08:947]                                              method = 0 --> fastboot download protocol
[12-31_01:28:08:947]                                              method = 2 --> fastboot download protocol (at command first)
[12-31_01:28:08:947]                                              method = 3 --> firehose download protocol
[12-31_01:28:08:947]     -u [vid[:pid]]                           Specify VID and PID mannully
[12-31_01:28:08:947]     -s [size]                                Transport block size
[12-31_01:28:08:947]     -v                                       Verbose
[12-31_01:28:08:947]     -h                                       Help message
root@ubuntu:#
```
