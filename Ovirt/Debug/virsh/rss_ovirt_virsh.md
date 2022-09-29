

virsh console
<https://www.cyberciti.biz/faq/how-to-enable-kvm-virsh-console-access-for-ubuntu-linux-vm/>
+ <https://askubuntu.com/questions/576437/virsh-ssh-into-a-guest-vm>  ( virsh ssh into a guest vm )
#virsh list
#$ virsh console ubuntu-box1
OR
# virsh console <ID>

BUT you need 
systemctl enable [serial-getty@ttyS0.service](mailto:serial-getty@ttyS0.service)
systemctl start [serial-getty@ttyS0.service](mailto:serial-getty@ttyS0.service)
		
virsh -r list
vdsClient -s 0 getAllVmStats

 KVM/Access  !!!!!!!!
<https://help.ubuntu.com/community/KVM/Access>

Moving disk image from one KVM machine to another
<https://pve.proxmox.com/wiki/Moving_disk_image_from_one_KVM_machine_to_another>

Manage KVM Virtual Machines With Virsh Program
<https://ostechnix.com/manage-kvm-virtual-machines-with-virsh-program/>

________Tools

reate and Export Full oVirt VM Backups to NFS Storage Domain
<https://myhomelab.gr/virtualization/2020/07/13/backup-virtual-machines.html>   !!!!!!!!!  

virt-backup
<https://github.com/aruhier/virt-backup>
<https://virt-backup.readthedocs.io/>

LibVirtKvm-Scripts
<https://github.com/dguerri/LibVirtKvm-scripts>

virtnbdbackup
Backup utiliy for Libvirt kvm / qemu with Incremental backup support via NBD. 
<https://github.com/abbbi/virtnbdbackup>

Libvirt Backup Tool (backup-vms)
<https://github.com/FelixDefrance/libvirt-backup-tool>

Бэкап виртуальной машины kvm без остановки
<https://serveradmin.ru/kvm-backup/>

A collection of tips and tricks...
KVM VM Image Crash
<https://simon.holmbri.ng/2020/05/08/kvm-vm-image-crash/>

7.2. Restoring the Self-Hosted Engine Environment
<https://cloud2.login.com/ovirt-engine/docs/Self-Hosted_Engine_Guide/sect-Restoring_SHE_bkup.html>


