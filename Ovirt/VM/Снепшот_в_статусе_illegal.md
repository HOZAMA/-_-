# rss ovirt illegal status of snapshot
Created Понедельник 30 мая 2022

ovirt snapshot remove delete rss illegal state disk image

<https://lists.ovirt.org/archives/list/users@ovirt.org/thread/5RXICTXUZMYMO5KFSFX67D2W4J75T4UV/#OWXUTJCQM4SZVCNGPFDM7Q5O6OQICECO>

+ <https://bugzilla.redhat.com/show_bug.cgi?id=1649129>


Here some notes I got to resolve such cases (verified at ovirt 4.2, should
apply at 4.3 also). This should do.

*# Recover VM from corrupted snapshot with disk in illegal state: (not
clean solution as it leaves orphaned snapshots at the storage domains)*


1. Login at engine DB

ssh to engine and run:

psql -s engine !!!!!!!

_____
select snapshot_id,snapshot_type,status,description from snapshots where vm_id=''
delete from snapshots where snapshot_id='';
_______


su - postgres -c 'scl enable rh-postgresql95 -- psql'
\c engine


2. Get the VM ID (from GUI or DB) and  find the broken snapshot in the

snapshots table and delete it.

engine=# select snapshot_id,snapshot_type,status,description from snapshots
where vm_id='0aff510b-b55a-4986-9d12-8407748fcd8b
';
2dd4c31d-7c57-4f87-b863-4fb3de1a5196 | REGULAR       | OK     | MyVM
 6a93187c-2b3f-409f-9831-3c11d36f3efb | ACTIVE        | OK     | Active VM
 818c46ff-4c32-496d-a4ca-12459e4ca917 | REGULAR       | OK     | Backup


4. Get the UUID of the affected VM disk (from GUI or DB) and find the image

linked to the broken snapshot

select
image_guid,parentid,imagestatus,vm_snapshot_id,volume_type,volume_format,active
from images where image_group_id='0994f9c0-568e-4e4c-b0ea-0370de64d2a7';
 cf8707f2-bf1f-4827-8dc2-d7e6ffcc3d43 |
3f54c98e-07ca-4810-82d8-cbf3964c7ce5 |           1 |
2dd4c31d-7c57-4f87-b863-4fb3de1a5196 |           2 |             4 | f
 1e75898c-9790-4163-ad41-847cfe84db40 |
cf8707f2-bf1f-4827-8dc2-d7e6ffcc3d43 |           4 |
818c46ff-4c32-496d-a4ca-12459e4ca917 |           2 |             4 | f
 604d84c3-8d5f-4bb6-a2b5-0aea79104e43 |
1e75898c-9790-4163-ad41-847cfe84db40 |           1 |
6a93187c-2b3f-409f-9831-3c11d36f3efb |           2 |             4 | t


5. Delete the broken snapshot from the snapshots table.

engine# delete from snapshots where snapshot_id='818c46ff-4c32-496d-a4ca-12459e4ca917';
DELETE 1


6. Delete the associated image to the broken snapshots.

engine=# delete from images where
image_guid='1e75898c-9790-4163-ad41-847cfe84db40';
DELETE 1

At this time, the snapshot is no longer shown on the 'Snapshots' tab of the
VM.


7. check the status of volumes in the data domain. At SPM run:


vdsm-tool -vvv dump-volume-chains 142bbde6-ef9d-4a52-b9da-2de533c1f1bd | grep ILLEGAL


8. In case no ILLLEGAL volumes are listed just start the VM.

In case you still get ILLEGAL volumes of the affected VM, then make them
legal:

To get the volume ID startup the VM and observe vdsm log:

tail -f /var/log/vdsm/vdsm.log |grep prepareImage

Example:
INFO (vm/5bf9a0bb) [vdsm.api] START
prepareImage(sdUUID=u'bc0480e2-85fe-42a4-91ae-f733b23c801f',
spUUID=u'75bf8f48-970f-42bc-8596-f8ab6efb2b63',
imgUUID=u'870f7e85-d9b6-494a-9541-b419fb0e1b32',
leafUUID=u'd7fa8c51-8cad-4695-b90a-a8d1dc146371', allowIllegal=False)
from=internal, task_id=89770233-103d-47f3-acc1-45d2e96d9e91 (api:46)

Now, go to the SPM and run a command like this:

vdsm-client -a host0.localdomain.local Volume setLegality
storagedomainID=bc0480e2-85fe-42a4-91ae-f733b23c801f
storagepoolID=75bf8f48-970f-42bc-8596-f8ab6efb2b63
imageID=870f7e85-d9b6-494a-9541-b419fb0e1b32
volumeID=d7fa8c51-8cad-4695-b90a-a8d1dc146371 legality=LEGAL

In case you still get ILLEGAL image status, although no ILLEGAL images are
reported from SPM and not chain issues are observed at image file, then you
may just flag the image as ok in the DB:
Example: update images set imagestatus='1' where image_guid='snapshot
id';

