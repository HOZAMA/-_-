# ovirt import
Created Четверг 17 июня 2021

chnged username in [/usr/lib64/python3.6/site-packages/ovirtsdk4/____init____.py](file:///usr/lib64/python3.6/site-packages/ovirtsdk4/__init__.py) !!!!!!!!!!!    on 1-st host togs

How to Install oVirt on CentOS 7
<https://linuxhint.com/install_ovirt_centos7/>

<https://libguestfs.org/virt-v2v.1.html?source=post_page---------------------------#environment-varibles>     !!!!!!!!!!!
VIRT_V2V_TMPDIR
LIBGUESTFS_CACHEDIR
OR
export TMPDIR=/vol06/OVA/TMP

VMware machine to KVM !!!!!!!!!!!!  
<https://docs.deistercloud.com/content/Tutorials.100/Linux.80/KVM%20virtualization.40/VMware%20machine%20to%20KVM.xml?embedded=true>
export TMPDIR=/vol06/OVA/TMP

SUCCESS convert on CONTROLLER01 (CentOS 7) !!!!!!!!!!!!!!
 LIBGUESTFS_CACHEDIR=/mnt/zabbix_vm/cucm/tmp/
 virt-v2v -i ova CUCM.ova -o local -os /mnt/zabbix_vm/cucm/out/ -of qcow2
+ SUCCESS (from CA01 ovirt host)
 virt-v2v -i libvirtxml CUCM.xml -o rhv-upload -oc <https://hosted-engine-24.rosstat.local/ovirt-engine/api> -of raw -os SAS_1 -oo rhv-cluster=Default -oo rhv-direct -op passfile -oo rhv-cafile=ca24.pem -oa preallocated --bridge ovirtmgmt 


TRY with  "-oa preallocated"  ( <https://bugzilla.redhat.com/show_bug.cgi?id=1600547> )      FAILED.....!!!!!!!!!!
[[[Cannot add Virtual Disk. Disk configuration (RAW Sparse backup-None) is incompatible with the storage domain type.]". HTTP response code is 409.\n']
qemu-img: Could not open 'json:{ "file.driver": "nbd", "file.path": "/var/tmp/rhvupload.Jd26zb/nbdkit0.sock", "file.export": "/" }': Failed to read data: Unexpected end-of-file before all bytes were read]]

#virt-v2v -i vmx -it ssh "<ssh://root@p24-esxi06.rosstat.local/vmfs/volumes/Local_ESXi06_2/CUCM/CUCM.vmx"> -o rhv-upload -oc <https://hosted-engine-24.rosstat.local/ovirt-engine/api> -of raw -os SAS_1 -oo rhv-cluster=Default -oo rhv-direct -op passfile -oo rhv-cafile=ca24.pem -oa preallocated


<https://manpages.ubuntu.com/manpages/xenial/man1/virt-v2v.1.html>
 In order to enable virtio, and hence improve performance of the guest after conversion,
   you should ensure that the minimum versions of packages are installed before conversion,
   by consulting the table below.
RHEL 5         kernel >= 2.6.18-128.el5
   lvm2 >= 2.02.40-6.el5
  selinux-policy-targeted >= 2.4.6-203.el5

saslpasswd2 -a libvirt adminuser !!!!!!!!!!!!!

eval `ssh-agent -s`

Converting virtual machines from other hypervisors to KVM with virt-v2v in RHEL 7 and RHEL 8 
<https://access.redhat.com/articles/1351473> !!!!!!!!!!!!!


Exporting a virtual machine from VMware as an OVA file and importing it into KVM 

Exporting a virtual machine from VMware as an OVA file and importing it into KVM 
<https://access.redhat.com/articles/1351963>

local convert



________________________ import in CA !!!!!!

(on CA host)
virt-v2v -i vmx /mnt/nfs_controller/ca-srv-zabbix-clone/ca-srv-zabbix-clone.vmx -o rhv-upload -oc <https://ca-oe01.tech.logic/ovirt-engine/api> -of raw -os CA-HUAWEI-15 -oo rhv-cluster=CL-APP5 -oo rhv-direct -op passfile -oo rhv-cafile=ca.pem -oa preallocated



______________________
AHCI 
Исправляем BSOD 0x0000007B при загрузке Windows 7 / Windows Server 2008 R2 !!!!!!!!!!!!!!!!!!!!
<https://winitpro.ru/index.php/2018/06/19/ispravlyaem-bsod-0x0000007b-pri-zagruzke-windows-7-windows-server-2008-r2/>
+ [/home/max/work/ONL/1_projects/RSS/DOCS/](file:///home/max/work/ONL/1_projects/RSS/DOCS)   Инструкция по настройке msahci.docx

How to Connect to an ESXi host with Ansible !!!!!!!! !!!!!!!!!!!!!!
<https://graspingtech.com/ansible-esxi/>
<https://graspingtech.com/ansible-esxi/>
   cat ~/.ssh/id_rsa.pub | ssh [root@10.1.1.11](mailto:root@10.1.1.11) 'cat >> /etc/ssh/keys-root/authorized_keys' 

cat ~/.ssh/id_rsa.pub | ssh [root@10.1.1.11](mailto:root@10.1.1.11) 'cat >> /etc/ssh/keys-root/authorized_keys' 


Community.Libvirt
<https://docs.ansible.com/ansible/latest/collections/community/libvirt/index.html>

Ansible Tip - Using the expect module
<https://blog.linuxserver.io/2018/03/23/ansible-tip-expect-module/>

Connection authentication
<https://libvirt.org/auth.html>

Run virsh and access libvirt as a regular user
<https://major.io/2015/04/11/run-virsh-and-access-libvirt-as-a-regular-user/>

Use virt-manager as a non-root user on Linux
<https://computingforgeeks.com/use-virt-manager-as-non-root-user/>



Converting virtual machines from other hypervisors to KVM with virt-v2v in RHEL 7 and RHEL 8 
<https://access.redhat.com/articles/1351473>

<https://libguestfs.org/virt-v2v.1.html>
-oo verify-server-certificate=true|false

<https://libguestfs.org/virt-v2v-input-vmware.1.html>
<https://libguestfs.org/nbdkit-vddk-plugin.1.html>
<https://libguestfs.org/nbdkit-vddk-plugin.1.html#LIBRARY-LOCATION>

6.13. Exporting and Importing Virtual Machines and Templates
<https://rhv.bradmin.org/ovirt-engine/docs/Virtual_Machine_Management_Guide/sect-Exporting_and_Importing_Virtual_Machines_and_Templates.html>

Virtual Machine Management Guide
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.0/html/virtual_machine_management_guide/index#Importing_a_Virtual_Machine_from_a_VMware_Provider>

6.12.4. Importing a Virtual Machine from a VMware Provider
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.0/html/virtual_machine_management_guide/sect-exporting_and_importing_virtual_machines_and_templates#Importing_a_Virtual_Machine_from_a_VMware_Provider>

<https://quorten.github.io/quorten-blog1/blog/2018/10/10/ovirt-howto> !!!!!!!!

5.2.3. Define a target profile in virt-v2v.conf
<https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/v2v_guide/preparation_before_the_p2v_migration-define_a_host_profile_in_virt_v2v-conf>

<https://kb.vmware.com/s/article/1031039> !!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Converting a VMware vCenter Linux virtual machine to KVM
<https://access.redhat.com/articles/1353223>

Converting a VMware vCenter Windows machine to KVM
<https://access.redhat.com/articles/1353463>

Export a virtual machine from VMware as an OVA file, and import it into KVM
<https://access.redhat.com/articles/1351963>

<https://jensd.be/489/linux/move-a-guest-from-vmware-esx-to-ovirt-or-rhev> !!!!!!!!!


<https://bugzilla.redhat.com/show_bug.cgi?id=1373863>
virt-v2v -v -x -o null -ic "<vpx://administrator@vcenter/encoded-data-center/encoded-cluster/esxi?no_verify=1">  vm-to-import

-oo verify-server-certificate=true|false

__________ articles  import

How to Migrate VMware vSphere to Oracle Linux KVM
<https://blogs.oracle.com/scoter/migrate-vmware-to-oracle-linux-kvm>

_________________succesful examples  <https://bugzilla.redhat.com/show_bug.cgi?id=1557273>

1.1 Convert a windows guest from VMware to rhv using --rhv-upload by virt-v2v,the conversion could be finished without error
# virt-v2v -ic <vpx://vsphere.local%5cAdministrator@10.73.73.141/data/10.73.75.219/?no_verify=1>  esx6.7-win2016-x86_64 -o rhv-upload -oc <https://ibm-x3250m5-03.rhts.eng.pek2.redhat.com/ovirt-engine/api> -os nfs_data -op /tmp/rhvpasswd -oo rhv-cafile=/home/ca.pem  -oo rhv-direct=true -of raw --password-file [/tmp/passwd](file:///tmp/passwd)

Scenario2:
2.1 Convert a linux guest from VMware via vddk to rhv using --rhv-upload by virt-v2v, the conversion could be finished without error
# virt-v2v -ic <vpx://vsphere.local%5cAdministrator@10.73.73.141/data/10.73.196.89/?no_verify=1> -it vddk -io vddk-libdir=/home/vmware-vix-disklib-distrib -io vddk-thumbprint=1F:97:34:5F:B6:C2:BA:66:46:CB:1A:71:76:7D:6B:50:1E:03:00:EA esx6.5-rhel6.9-x86_64 --password-file /tmp/passwd -o rhv-upload -oc <https://ibm-x3250m5-03.rhts.eng.pek2.redhat.com/ovirt-engine/api> -os nfs_data -op /tmp/rhvpasswd -oo rhv-cafile=/home/ca.pem  -oo rhv-direct -of raw -oa preallocated -b ovirtmgmt

Scenario3:
3.1 Convert a guest from VMX to rhv4.2's iSCSI data using --rhv-upload by virt-v2v
# virt-v2v -i vmx esx5.5-win2012R2-x86_64.vmx -o rhv-upload -oc <https://hp-dl360eg8-03.lab.eng.pek2.redhat.com/ovirt-engine/api> -os iscsi_data -op /tmp/rhvpasswd -oo rhv-cafile=/root/ca.pem -of raw --password-file /tmp/passwd -b ovirtmgmt -oa preallocated -oo rhv-cluster=ISCSI -oo rhv-verifypeer

Scenario4:
4.1 Convert a guest from OVA to rhv's FC data using --rhv-upload by virt-v2v
# virt-v2v -i ova esx6.7-rhel7.5-x86_64 -o rhv-upload -oc <https://hp-dl360eg8-03.lab.eng.pek2.redhat.com/ovirt-engine/api> -os fc_data -op /tmp/rhvpasswd -oo rhv-cafile=/root/ca.pem -of raw --password-file /tmp/passwd -b ovirtmgmt -oa preallocated -oo rhv-cluster=FC

Scenario5:
5.1 Convert a guest from Xen server to rhv using --rhv-upload by virt-v2v
# virt-v2v -ic xen+<ssh://root@10.73.3.21> xen-pv-rhel6.9-x86_64 -o rhv-upload -oc <https://ibm-x3250m5-03.rhts.eng.pek2.redhat.com/ovirt-engine/api> -os nfs_data -op /tmp/rhvpasswd -oo rhv-cafile=/home/ca.pem  -oo rhv-direct -of raw -oa preallocated -b ovirtmgmt

__________ to test 

virt-v2v -i libvirtxml /root/xxxx.xml -o ovirt-upload -oc https://<OLVM FQDN>/ovirt-engine/api -os KVM-LAB-REPO -op /root/ovirt.pw -of raw -oo rhv-cluster="MyCluster1" -oo rhv-cafile=/root/ca.pem


ovirt-imageio !!!!!!!!
<https://ovirt.github.io/ovirt-imageio/>

_________ ovirt vm import / export related articles 

<https://www.mail-archive.com/users@ovirt.org/msg55983.html>

_______________ convert 

Converting standalone KVM guests to an oVirt Virtualization ...  (google it !)

_____________  import from KVM  !!!!!!!!!!!

<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/html-single/virtual_machine_management_guide/index#Exporting_a_virtual_machine_to_a_host>
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/html-single/virtual_machine_management_guide#Importing_a_Virtual_Machine_from_KVM> !!!!!!!!!!!!!!
<https://bugzilla.redhat.com/show_bug.cgi?id=1426573>

 sudo -u vdsm virsh -c 'qemu+<ssh://root@ca-c5host06.tech.logic/system'> list
   30  history
   31  ssh [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   32  sudo -u vdsm virsh -c 'qemu+<ssh://root@ca-c5host06.tech.logic/system'> list
   33  ssh [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   34  ssh-copy-id [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   35  ssh-keygen
   36  ssh-copy-id [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   37  ssh [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   38  sudo -u vdsm ssh-keygen
   39  sudo -u vdsm ssh [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   40  sudo -u vdsm ssh-copy-id [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   41  sudo -u vdsm ssh [root@ca-c5host06.tech.logic](mailto:root@ca-c5host06.tech.logic)
   42  history
   43  sudo -u vdsm virsh -c 'qemu+<ssh://root@ca-c5host06.tech.logic/system'> list

saslpasswd2 -a libvirt adminuser  (  !!!!!!!  on destination host !!!!!!!!!!  )

CA1  Export DOMAIN
export domain  10.100.233.61:/Export

___________  export domain
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/html-single/administration_guide/index#sect-Importing_Existing_Storage_Domains>

10.177.176.107:/vm_data/portal_ova/

___________  prepare for NFS export domain

 getent group kvm || groupadd kvm -g 36
 getent passwd vdsm || useradd vdsm -u 36 -g 36
 chown -R 36:36 /vm_data/portal_ova
 chmod 0755 [/vm_data/portal_ova](file:///vm_data/portal_ova)

[/etc/exports](file:///etc/exports)   (  on jenkins  )
/vm_data/portal_ova *(rw,anonuid=36,anongid=36,all_squash)

 exportfs -rvv








