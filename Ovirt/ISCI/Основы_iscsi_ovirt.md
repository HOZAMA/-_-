# rss ovirt iscsi debug
Created Понедельник 06 сентября 2021

echo 'show config' | multipathd -k

______________Documentation / External references

scsi-target-utils configuration:
<https://fedoraproject.org/wiki/Scsi-target-utils_Quickstart_Guide>
<https://fedorahosted.org/ovirt/wiki/ISCSISetup>
<https://bugzilla.redhat.com/show_bug.cgi?id=738239>
<http://www.linuxjournal.com/content/creating-software-backed-iscsi-targets-red-hat-enterprise-linux-6>

_________________

CentOS7 – oVirt – iSCSI
<https://zipur.ca/knowledgebase/centos7-ovirt-iscsi/>

______________ Chapter 8. Troubleshooting DM Multipath
<https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_device_mapper_multipath/assembly_troubleshooting-multipath-managing-mpath>

# multipathd show config

The following command disables queueing for all devices. 
# multipathd disablequeueing maps
After you have disabled queueing for a device, it will remain disabled until multipathd is restarted or reloaded or until you one of the following commands. 
# multipathd restorequeueing map <device>
 The following command resets queueing to its previous value for all devices.
   #multipathd restorequeueing maps

Troubleshooting with the multipathd interactive console

# multipathd -k
> > show config
> > CTRL-D

# multipathd -k
> > reconfigure
> > CTRL-D

# multipathd -k
> > show paths
> > CTRL-D

____________Multipath: Active/Passive, Dual Active, and Active/Active

<https://gestaltit.com/syndicated/stephen/multipath-activepassive-dual-active-activeactive/>

____________  How to monitor the status of dm-multipathing and multipath devices (path groups) in Linux         !!!!!!!!!!!!!!!!!!!!!

<https://www.thegeekdiary.com/how-to-monitor-the-status-of-dm-multipathing-and-multipath-devices-path-groups-in-linux/>

Understanding Linux multipath (dm-multipath) - The Geek Diary
<https://www.thegeekdiary.com/understanding-linux-multipath-using-dm-multipath/>





