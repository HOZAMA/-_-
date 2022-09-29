# rss ovirt vdsm
Created Четверг 24 июня 2021

How To Kill / Abort a Task in oVirt / RHEV
<https://computingforgeeks.com/how-to-kill-abort-a-task-in-ovirt-rhev/>
How To Kill / Abort a Task in oVirt / RHEV | [ComputingForGeeks](./ComputingForGeeks.md)
<https://computingforgeeks.com/how-to-kill-abort-a-task-in-ovirt-rhev/>

(on SPM HOST !!!!)
#vdsm-client Host getAllTasksInfo
#vdsm-client Task getStatus taskID=<TASKID>
#vdsm-client Task stop taskID=<TaskID>
   #vdsm-client Task clear taskID=<TaskID>


Helper utilities
<https://www.ovirt.org/develop/developer-guide/db-issues/helperutilities.html>

on ENGINE !!!!!!!

[/usr/share/ovirt-engine/setup/dbutils](file:///usr/share/ovirt-engine/setup/dbutils)

_______________ how to clean stuck task

<https://angrysysadmins.tech/index.php/2018/10/grassyloki/ovirt-stop-all-running-tasks/>     !!!!!!!!!!!!!!!!!!!!

SSH into ovirt-engine as root, then run:
#su postgres
#psql -d engine -U postgres
#select * from job order by start_time desc;

Grab the job_id for the task you want to delete, then use the DeleteJob procedure:

select DeleteJob('UUID_HERE');

If when you try and run psql you get command not found, try using this after switching to the postgres user:

scl enable rh-postgresql10 "psql -d engine -U postgres"

___________________
search in db snapshots

select snapshot_id,description from snapshots where vm_id = 'c847130e-230d-47ee-a124-54d46e1dd928';




*****


<https://lists.ovirt.org/pipermail/users/2017-November/085194.html>
<https://lists.ovirt.org/pipermail/users/2017-November/085198.html>

