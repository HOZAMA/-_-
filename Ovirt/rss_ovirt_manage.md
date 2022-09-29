# rss ovirt manage
Created Суббота 08 мая 2021

Restart Hosted Engine VM
<https://zipur.ca/knowledgebase/restart-hosted-engine-vm/>
ON HOST
hosted-engine --set-maintenance --mode=global
hosted-engine --vm-shutdown
hosted-engine --vm-status                       hosted-engine --vm-status | grep -i status
hosted-engine --check-liveliness
#make sure that the status is shutdown before restarting
hosted-engine --vm-start
hosted-engine --vm-status
#make sure the status is health before leaving maintenance mode
hosted-engine --set-maintenance --mode=none

______________  removing / readding host from cluster

<https://wiki.it-kb.ru/ovirt/remove-host-with-engine-status-unknown-stale-data-from-hosted-engine-configuration>

# hosted-engine --vm-status
# hosted-engine --vm-status | grep -e 'Host ID\|Engine status\|Hostname'
(looking for HOST with Engine status: unknown stale-data )

#hosted-engine --clean-metadata --force-cleanup --host-id=<Host ID>

_______________  manage various settings
KEYs
he_local : ['bridge', 'ca_cert', 'ca_subject', 'conf', 'conf_image_UUID', 'conf_volume_UUID', 'connectionUUID', 'console', 'domainType', 'fqdn', 'gateway', 'host_id', 'iqn', 'iscsi_paths_blacklist', 'lockspace_image_UUID', 'lockspace_volume_UUID', 'metadata_image_UUID', 'metadata_volume_UUID', 'mnt_options', 'network_test', 'nfs_version', 'password', 'port', 'portal', 'sdUUID', 'spUUID', 'storage', 'tcp_t_address', 'tcp_t_port', 'user', 'vdsm_use_ssl', 'vm_disk_id', 'vm_disk_vol_id', 'vmid']
KEYs
he_shared : ['bridge', 'ca_cert', 'ca_subject', 'conf', 'conf_image_UUID', 'conf_volume_UUID', 'connectionUUID', 'console', 'domainType', 'fqdn', 'gateway', 'host_id', 'iqn', 'iscsi_paths_blacklist', 'lockspace_image_UUID', 'lockspace_volume_UUID', 'metadata_image_UUID', 'metadata_volume_UUID', 'mnt_options', 'network_test', 'nfs_version', 'password', 'port', 'portal', 'sdUUID', 'spUUID', 'storage', 'tcp_t_address', 'tcp_t_port', 'user', 'vdsm_use_ssl', 'vm_disk_id', 'vm_disk_vol_id', 'vmid']

examples 
hosted-engine --get-shared-config storage --type=he_shared

<https://bugzilla.redhat.com/show_bug.cgi?id=1449561>       !!!!!!!!!!
#hosted-engine --get-shared-config gateway  --type=he_shared
# hosted-engine --get-shared-config gateway  --type=he_local
# hosted-engine --set-shared-config gateway 8.8.8.8  --type=he_shared



____________________________________
Chapter 3. Troubleshooting a Self-Hosted Engine Deployment
<https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.2/html/self-hosted_engine_guide/troubleshooting>

Check the following logs:
 [/var/log/messages](file:///var/log/messages)
[/var/log/ovirt-engine/engine.log](file:///var/log/ovirt-engine/engine.log)
[/var/log/ovirt-engine/server.log](file:///var/log/ovirt-engine/server.log)
	
Check the ovirt-ha-agent logs in 
/var/log/ovirt-hosted-engine-ha/agent.log 
	
Check the VDSM logs in 
/var/log/vdsm/vdsm.log 
	
Check the ovirt-ha-agent logs in 
/var/log/ovirt-hosted-engine-ha/agent.log

health status  <https://engine-fqdn/ovirt-engine/services/health/>  !!!!!!!!!!!!!!!!!

<https://hosted-engine-><НОМЕР_РЕГИОНА>.rosstat.local/ovirt-engine/services/health/

________________________________________ manage storage  storage tasks              ovirt unlock disks   <https://www.ovirt.org/develop/developer-guide/db-issues/helperutilities.html>

/usr/share/ovirt-engine/setup/dbutils

 If the upload times out and you see the message, Reason: timeout due to transfer inactivity, increase the timeout value:
# engine-config -s TransferImageClientInactivityTimeoutInSeconds=6000
Restart the ovirt-engine service:
# systemctl restart ovirt-engine

<https://angrysysadmins.tech/index.php/2018/10/grassyloki/ovirt-unlock-virtual-disks/>
oVirt: Unlock Virtual Disks

Unlock all disks 
/usr/share/ovirt-engine/setup/dbutils/unlock_entity.sh -t all

Unlock specific VM disk 
/usr/share/ovirt-engine/setup/dbutils/unlock_entity.sh -t vm UUID_OF_VM

+ <https://www.ovirt.org/develop/developer-guide/db-issues/helperutilities.html>

___________debug 

# multipath -r -v3 | grep no_path_retry

<https://lists.ovirt.org/archives/list/users@ovirt.org/thread/S3LXEJV3V4CIOTQXNGZYVZFUSDSQZQJS/>

_____________  dwh postgres

<https://www.ovirt.org/develop/developer-guide/db-issues/helperutilities.html>

Please ensure that data warehouse is properly installed and configured

<https://www.mail-archive.com/devel@ovirt.org/msg14376.html>
su - postgres
scl enable rh-postgresql10 bash
psql


'DWH_DB_URL' is 'jdbc:<postgresql://localhost:5432/ovirt_engine_history?sslfactory=org.postgresql.ssl.NonValidatingFactory'> 

Unable to retrieve dashboard data: org.ovirt.engine.ui.frontend.server.dashboard.DashboardDataException: Error whil
e running SQL query

Caused by: org.postgresql.util.PSQLException: ERROR: could not open file "base/16401/1996932060.1" (target block 4294937268): previous segment is only 16543 blocks


rh-postgresql10-postgresql.service 

/etc/ovirt-engine/engine.conf.d/10-setup-dwh-database.conf
DWH_DB_USER="ovirt_engine_history"
DWH_DB_PASSWORD="dHHW47zn3ojZREAmc3yyKV"


 PGPASSWORD=XXXXXXX ./fkvalidator.sh -u ovirt_engine_history -d ovirt_engine_history -v

 [/etc/ovirt-engine/engine.conf.d/10-setup-database.conf](file:///etc/ovirt-engine/engine.conf.d/10-setup-database.conf)
ENGINE_DB_USER="engine"
ENGINE_DB_PASSWORD=""
ENGINE_DB_DATABASE="engine"
ENGINE_DB_URL="jdbc:<postgresql://localhost:5432/engine?sslfactory=org.postgresql.ssl.NonValidatingFactory">

PGPASSWORD=4LvCVwFw6D8soRq2fBfItX /usr/share/ovirt-engine/setup/dbutils/fkvalidator.sh -u engine -d engine -v

postgres learn 
<https://www.educba.com/postgresql-list-tables/>
<https://www.postgresqltutorial.com/postgresql-list-users/>

ps auxww | grep dwhd


/usr/share/ovirt-engine/dbscripts/engine-psql.sh -c "SELECT * FROM dwh_history_timekeeping;"

_____________-errors

|Can not sample data, oVirt Engine is not updating the statistics. Please check your oVirt Engine status

 ERROR [org.ovirt.engine.ui.frontend.server.dashboard.DashboardDataServlet] (default task-95) [] Unable to retrieve dashboard data: org.ovirt.engine.ui.frontend.server.dashboard.DashboardDataException: Error while running SQL query

Caused by: org.postgresql.util.PSQLException: ERROR: could not open file "base/16401/1996932060.1" (target block 4294937268): previous segment is only 16543 blocks

ERROR [org.ovirt.engine.ui.frontend.server.dashboard.DashboardDataServlet.CacheUpdate.Utilization] (EE-ManagedThreadFactory-default-Thread-3) [] Could not update the Utilization Cache: Error while running SQL query: org.ovirt.engine.ui.frontend.server.dashboard.DashboardDataException: Error while running SQL query

Caused by: org.postgresql.util.PSQLException: ERROR: could not open file "base/16401/1996932060.1" (target block 4294937268): previous segment is only 16543 blocks

.PSQLException:ERROR: current transaction is aborted, commands ignored until end of transaction block

PSQLException:ERROR: could not read block 36504 in file "base/16401/1996932060": read only 0 of 8192 bytes |1


<https://bugzilla.redhat.com/show_bug.cgi?id=1277591>
<https://bugzilla.redhat.com/show_bug.cgi?id=1076902>
<https://bugzilla.redhat.com/show_bug.cgi?id=1073529>
<https://bugzilla.redhat.com/show_bug.cgi?id=1705132>
<https://users.ovirt.narkive.com/OHwMisdK/ovirt-users-etl-service-and-winter-hour>

sql from engine table
select * from dwh_history_timekeeping;


solution ??
<https://lists.ovirt.org/pipermail/users/2017-January/079112.html>
ovirt ETL service sampling has encountered an error. Please consult the service log for more details.
<https://access.redhat.com/solutions/2046103>
<https://access.redhat.com/solutions/3251541>
<https://bugzilla.redhat.com/show_bug.cgi?id=1718165>   !!!!!!!!!
<https://support.oracle.com/knowledge/Oracle%20Linux%20and%20Virtualization/2766658_1.html>


The ETL sampling process collects the configurations and statistics for the
new dashboards.
The engine has a heartbeat that should update every 15 seconds. Sampling
runs every 20 seconds.
If the engine is busy and the heartbeat does not update for some reason ,
the dwh will send an error. It compares the last sync with the heartbeat.
Heartbeat should be newer than the last sync...

______________ certificate
<https://www.ovirt.org/develop/release-management/features/infra/pki-renew/>

_____________  no unique id  
<https://lists.ovirt.org/archives/list/users@ovirt.org/thread/WIODSRPHL4GSYAYDNGBU6ZKJX2KGOWEC/#7Y3UFKE6FMQQNYDR2VZWUTFOACXXCAKB>
uuidgen > [/etc/vdsm/vdsm.id](file:///etc/vdsm/vdsm.id)






