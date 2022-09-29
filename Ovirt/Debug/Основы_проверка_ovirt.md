# rss ovirt debug
Created Пятница 07 мая 2021

Temporarily changed log level to debug using "vdsm-client Host setLogLevel level=DEBUG" 


WIN ISO !!!!!!! SW_DVD9_Windows_Svr_Std_and_DataCtr_2012_R2_64Bit_Russian_-4_MLF_X19-82917.ISO


<https://libguestfs.org/virt-v2v.1.html#running-virt-v2v-as-root-or-non-root>      non-root 

<https://libvirt.org/auth.html>   !!!!!!!!!!!!!!!!

ovirt kvm non-roo users virsh  !!!!!!!!
export LIBVIRT_DEFAULT_URI=qemu:///system

___________   hosted engine troubleshooting liveliness 

Chapter 3. Troubleshooting a Self-Hosted Engine Deployment
<https://cloud2.login.com/ovirt-engine/docs/Self-Hosted_Engine_Guide/Troubleshooting.html>   !!!

hosted-engine --check-liveliness: This command checks the liveliness page of the ovirt-engine service. You can also check by connecting to <https://engine-fqdn/ovirt-engine/services/health/> in a web browser. 

<https://engine-fqdn/ovirt-engine/services/health/>      !!!!!!!!!!!!

______________ diagnostic ovirt diagnosis

ping 172.31.250.4 -s 8000 -M do -c 4

ping 172.31.250.5 -s 8000 -M do -c 4

_________________  VDSM Client
<https://www.ovirt.org/develop/developer-guide/vdsm/vdsm-client.html>
About vdsm-client
vdsm-client is a command line tool provided by VDSM.
vdsm-client can used to execute commands: start virtual machines, manage storage, devices, etc.
It’s recommended to use vdsm-client at development stage, always use oVirt Engine to manage your stable environment.

Connecting to HOST
Connecting to a host is secured by default, pass –insecure to connect in an insecure way (not recommended). 
Examples:
` # vdsm-client [-h] [-a ADDRESS] [-p PORT] [–insecure] [–timeout TIMEOUT] [-f FILE] namespace method [name=value [name=value] …]`

default: If no arguments are passed, vdsm-client will connect to localhost.

_____ VDSM 

Vdsm
Vdsm is a daemon which is required by a Virtualization Manager such as oVirt-engine or Red Hat Enterprise Virtualization Manager to manage Linux hosts and their KVM virtual machine guests. Vdsm manages and monitors the host’s storage, memory and networks as well as virtual machine creation, other host administration tasks, statistics gathering, and log collection.

Vdsm Getting Started <https://www.ovirt.org/develop/developer-guide/vdsm/getting-started.html>

___________ Hosted engine status is showing 'failed liveliness check' and engine VM gets rebooted frequently 

<https://access.redhat.com/solutions/2072603>

___________ develop FAQ  <https://ovirt.org/develop/faq.html>

 What are the default mount options used when oVirt node mounts a NFS storage or when configuring a NFS storage domain?
  soft,timeo=10,retrans=6
 What are the requirements need to be met for detecting a LUN in oVirt GUI?
The LUN should be raw (no filesystem, no LVM, no data)
The LUN should be larger than 10Gb in size
The LUN should be r/w accessible from the SPM host.
	
_________ engine-cleanup | oVirt

<https://www.ovirt.org/develop/release-management/features/integration/engine-cleanup.html>

3.2. Cleaning Up a Failed Self-hosted Engine Deployment ...
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/self-hosted_engine_guide/cleaning_up_a_failed_self-hosted_engine_deployment>

check all locked entities
 ./unlock_entity.sh -q -t all -c

vdsm-client Task getInfo taskID=<UUID>

 vdsm-client Host getAllTasksInfo    (  on SPM node !!!!!!!!  )

+
<https://lists.ovirt.org/archives/list/users@ovirt.org/message/STHMCOQPG5Z5BMJ4QIN2B44DV2MUIOSD/>
<https://lists.ovirt.org/pipermail/users/2017-November/085194.html>

+
[ INFO ] Cleaning async tasks and compensations
[ INFO ] Unlocking existing entities
So one chance could be to run
engine-setup --offline (to prevent updates)
and let it do the clean stage
Putting environment into global maintenance before in case of self hosted engine


____________  job search in DB

su - postgres
psql -d engine -U postgres
select * from job order by start_time desc;
	
then delete !

select DeleteJob('<job_id>');

_________________ vm locked

Is the VM showing as locked?  You could try to manually unlocking it.  I
did this in a test environment a while back with some success after a vm
was stuck in a "locked" state.  Of course the gui and engine should handle
most of this for you, manually mucking around the internal DB can cause
some pretty serious issues if you are not careful...

sudo su postgres

psql -d engine -U postgres

SELECT vm_guid, vm_name FROM vm_static WHERE vm_name='*VM_Name_Here*';
This should return a string such as: "0ec20854-e1ca-4e49-be87-a6cd36d40c18"

Reset the lock:
update vm_dynamic SET status=0 where vm_guid='
0ec20854-e1ca-4e49-be87-a6cd36d40c18';

__________ Cancel Remove Snapshot Task  How To Kill / Abort a Task in oVirt / RHEV  

<https://computingforgeeks.com/how-to-kill-abort-a-task-in-ovirt-rhev/>





