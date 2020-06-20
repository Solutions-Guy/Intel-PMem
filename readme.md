# Enable PMEM in AppDirect mode in RHEL

Prerequisites:
* RHEL 7.7 installed on primary SSD/NVMe drive
* Parameters added for Linux kernel to support persistent memory drivers

Install ipmctl
* $ sudo yum install epel release
* $ sudo yum info ipmctl
* $ sudo yum install ipmctl

Show DIMM information
* $ sudo ipmctl show dimm

Configure PMEM to App Direct mode without interleaved option
* $ sudo ipmctl create goal persistentmemorytype appdirectnotinterleaved

Reboot RHEL 7 for applying the configuration to PMEM