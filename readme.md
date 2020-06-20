# PMEM Performance in AppDirect Mode

This repo contains requirements to configure PMEM on Supermicro servers for AppDirect Mode, optimized for Storage-Class memory applications.

Check out the Wiki to see how to enable PMEM in AppDirect mode with RHEL.

FIO results are also available in the Wiki.

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

Reboot RHEL 7 for applying the configuration to PMEM. After reboot, use ipmctl to show and verify provisioned
capacity
* $ sudo ipmctl show memoryresources

Run the following command to see if the device was created.

* $ sudo ls /dev/ pmem

Create a DAX enabled file system such as XFS or EXT4 on the new persistent memory device.
* $ sudo vg_pmem /dev/pmem0 /dev/pmem1 /dev/pmem2 /dev/pmem3
* $ sudo vgdisplay vg_pmem
* $ sudo lvcreate n vol_pmem l 100%FREE vg_pmem
* $ sudo lvdisplay / vg_pmem vol_pmem
* $ sudo mkfs.ext4 /dev/ vg_pmem vol_pmem
* $ sudo lsblk

Result should look like this:

![](https://github.com/Solutions-Guy/PMEM/blob/master/File%20System.PNG)
