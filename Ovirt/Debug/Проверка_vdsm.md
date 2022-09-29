# rss ovirt debug vdsm
Created Четверг 13 мая 2021

<https://www.ovirt.org/develop/developer-guide/vdsm/vdsm-client.html> !!!!!!!!

_____________ Examples

Listing virtual machines

` # vdsm-client Host getVMList`

` # vdsm-client Host getVMList fullStatus=True`
Getting HOST capabilities

` # vdsm-client Host getCapabilities`
Getting host statistics

` # vdsm-client Host getStats`
Getting statistics of running VMs

` # vdsm-client Host getAllVmStats`
Getting storage VG details

` # vdsm-client Host getLVMVolumeGroups`
Stopping a VM

1) Get the vmId:

` # vdsm-client Host getVMList fullStatus=True`

2) Destroy the VM

` # vdsm-client VM destroy vmID=`
Resuming a VM

1) Get the vmId:

` # vdsm-client Host getVMList fullStatus=True`

2) Resume the VM

` # vdsm-client VM cont vmID=`
Setting up vnc to a Virtual Machine in case oVirt Engine is out

Get VM id and displayPort

` # vdsm-client Host getVMList fullStatus=True`

Setting vnc password to VM

` # vdsm-client VM setTicket vmID= password= ttl=0 existingConnAction=keep params={val:key}`

Now try to use vnc client

` # vncviewer :`
Invoking complex commands

For invoking methods with many or complex parameters, you can read the parameters from a JSON format file:

` # vdsm-client -f lease.json Lease info`

where lease.json file content is:

   {
"lease": {
"sd_id": "75ab40e3-06b1-4a54-a825-2df7a40b93b2",
"lease_id": "b3f6fa00-b315-4ad4-8108-f73da817b5c5"
}
}

It is also possible to read parameters from standard input, creating complex parameters interactively:

   # cat <<EOF | vdsm-client -f - Lease info
 {
 "lease": {
 "sd_id": "75ab40e3-06b1-4a54-a825-2df7a40b93b2",
 "lease_id": "b3f6fa00-b315-4ad4-8108-f73da817b5c5"
 }
 }
 EOF
	
_________________  more on vdsm-client

<https://lists.ovirt.org/pipermail/users/2017-June/082344.html>
When you say "not visible in oVirt" you mean that you do not see them in
the UI?  Do you know the specific uuids for the missing volumes?  You could
use lvm to check if the LVs are visible to the host.

lvs --config 'global {use_lvmetad=0}' -o +tags

For each LV, the tag beginning with IU_ indicates the image the volume
belongs to.

You could also try to use the vdsm commands:

# Get the storage pool id
sudo vdsm-client Host getConnectedStoragePools

# Get a list of storagedomain IDs
sudo vdsm-client Host getStorageDomains # gives you a list of
storagedomainIDs

# Get a list of image ids on a domain
sudo vdsm-client StorageDomain getImages sdUUID=<domain id>

# Get a list of volume ids in an image
sudo vdsm-client Image getVolumes imageID=<image> storagepoolID=<pool>
storagedomainID=<domain>


If the wanted images are present on the host but not in engine then you had
a problem with import.  If the images are not visible to the host then you
probably have some storage connection issue.
_____________________________

EXAMPLE 
vdsm-client Image getVolumes imageID=22d5b161-9af9-4e8f-b321-1c570d7f3e29 storagepoolID=5fe33940-616d-11eb-bf35-00163e2f480f storagedomainID=9b5d39b6-c802-490c-9b6b-2c3a5e2af9ae







