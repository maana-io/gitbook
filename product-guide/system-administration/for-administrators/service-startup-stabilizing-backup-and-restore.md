# Service Startup, Stabilizing, Backup & Restore

## **Service Startup**

Typically, Services will fail during startup. This is normal as long as there is at least one copy of a Service in a running state at the end of startup. You can always check on the current state in your Terminal by running either: **``` docker service ls ```**

OR

**``` docker stack ps infrastructure docker stack ps core docker stack ps samples docker stack ps azure docker stack ps arbots ```**

## Service Stabilization & Performance Metrics

To determine if the system is in a stable state, go to the prometheus page at: http://&lt;cluster name&gt;:9090

Under Status/Targets verify that SAQ is reporting green. Note that it is normal for Docker to report as unavailable.

Performance Metrics are available on the Public IP Address at: http://&lt;cluster name&gt;:4000

{% hint style="info" %}
**Note:** the default login credentials for this page will be admin/admin, it is recommended that you change these credentials immediately following your first login.
{% endhint %}

## Service Deployment - Backup & Restore

#### Prerequisites

* The latest scripts and docker-compose files for Backup and Restore uploaded to the cluster 
* A storage location on the node that is running the backup capable of holding the backup
* The file containing environment variables used for the deployment \(e.g., `deploy.env.sh`\) or the environment variables themselves if used on the command line when the stack was deployed.
* Access to the docker-compose file used to bring up the environment
* Run by an account which is able to SSH to all nodes in the cluster, including the current node

#### Overview

Both Backup and Restore are done via the script do\_backup.sh. This script automates the process which consists of: 

1. Stop **all** instances of Loader, CKG, Portal, and KindDB in the environment
2. Flush the Redis cache
3. Stop **all** instances of SAQ-Server and SAQ in the environment
4. Place **all** Consul instances into Maintenance mode
5. Deregister SAQ from Consul
6. If restoring data, delete existing SAQ and Consul KV data
7. Perform the backup/restore of SAQ and Consul data
8. Restore the Maana Q stack \(to bring back up stopped services\)
9. Take **all** Consul instances out of Maintenance mode

Logs for backup and restore can be found in Graylog under the tags `maana-backup` and `maana-restore`.

#### Backup Instructions

**Before initiating a backup, please be sure that Loader is not processing any files.** This can be checked by searching `tag:maana-loader` in Graylog or looking at container resources in Grafana.

Run the script `do_backup.sh` with the `-b` flag. Additional parameters are described below. If any environment variables need to be provided as part of the Maana Q stack deploy command, these should be used with `do_backup.sh`.

There are two parts to telling the backup is complete. First, the user will see the text `Backup complete.` in Graylog when searching for `tag:maana-backup`. This indicates that the backup itself has completed. Second, the script will report `BACKUP has completed.`, indicating that platform services have been restored.

The user can validate in the folder created for their backup \(`{BACKUP_DIRECTORY}/backup.{BACKUP_TAG}`\) that they have the following files and none of them are 0-bytes in size. It is expected that if any step of the backup fails, the entire process will fail, resulting in an incomplete backup. Creating a backup does not modify the data in the system. In the event of a failure during backup, the process can be run again once any issues are resolved.

* consul.{BACKUP\_TAG}
* consul.kv.maana.{BACKUP\_TAG}.json
* PORTAL.{BACKUP\_TAG}.tgz
* SAQ.{BACKUP\_TAG}.tgz

Backup and Restore scripts will autodetect stack names, but it is recommended to keep default stack names \(i.e. infrastructure, core etc\)

`-c {MAANA_Q_DOCKER_COMPOSE_FILE}` - Provide the path to the Docker-Compose file used to launch the Maana Q Core \(usually `core.yml`\)

`-d {BACKUP_DIRECTORY}` - Provide an absolute path to where the backup should be saved.

`-t {HOST_SAQ_DATA_DIRECTORY}` - An optional parameter which specifies that the current environment was deployed with SAQ using a mapped host directory \(i.e., gluster\) for storage instead of a Docker volume. Provide the directory on the host where SAQ data is located. Default: `/maana/saq`. Not compatible with the `-v` option.

`-v` - An optional flag which specifies that the current environment was deployed with SAQ using a Docker volume for storage instead of a mapped directory. Assumes that the volume is named {STACK}\_saq\_data. Not compatible with the `-t` option.

`-q {Q_CORE_TAG}` - An optional parameter which allows the user to specify the path to a file containing the deployment configuration variables to source.

Backup and restore must be ran with the same build manifest in scope \(deploy.env.sh\)

Example **Backup** commands:

```
source deploy.env.sh

bash ./backup_restore/do_backup.sh -b -d ~/maana/data -v -q ../cluster/deploy.env.sh -c core.yml

bash ./backup_restore/do_backup.sh -b -d /maana/backups -t /gluster/saq -q ../cluster/deploy.env.sh -c core.yml
```

**Backup Tags**

Backup automatically generates an identifier \('tag'\) for the backup based on the timestamp when the process was launched. The specific tag can be found in Graylog by looking at logs for `maana-backup` and the text `Backup tag is {BACKUP_TAG}`. In addition, you can look in the directory provided for storing the backups. This directory will contain subfolders named like `backup.{BACKUP_TAG}`.

#### Restore Instructions

**Restore completely removes any data currently in the system and replaces it with the designated backup.**

Run the script `do_backup.sh` with the `-r {BACKUP_TAG}` parameter. See the description for _Backup Instructions_ for how to find `{BACKUP_TAG}` values. Additional parameters are described below. If any environment variables need to be provided as part of the Maana Q stack deploy command, these should be used with `do_backup.sh`.

There are two parts to telling that the restore is complete. First, the user will see the text `Restore complete.` in Graylog when searching for `tag:maana-restore`. This indicates that restoration of the backup has completed. Second, the script will report `RESTORE has completed.`, indicating that platform services have been restored.

`-c {MAANA_Q_DOCKER_COMPOSE_FILE}` - Provide the path to the Docker-Compose file used to launch the Maana Q stack.

`-d {BACKUP_DIRECTORY}` - Provide an absolute path to where the backup should be saved.

`-t {HOST_SAQ_DATA_DIRECTORY}` - An optional parameter which specifies that the current environment was deployed with SAQ using a mapped host directory \(i.e., gluster\) for storage instead of a Docker volume. Provide the directory on the host where SAQ data is located. Default: `/maana/saq`. Not compatible with the `-v` option.

`-v` - An optional flag which specifies that the current environment was deployed with SAQ using a Docker volume for storage instead of a mapped directory. Assumes that the volume is named {STACK}\_saq\_data. Not compatible with the `-t` option.

`-q {Q_CORE_TAG}` - An optional parameter which allows the user to specify the path to a file containing the deployment configuration variables to source.

Example **Restore** commands:

```
source deploy.env.sh

bash ./backup_restore/do_backup.sh -r 201808161855 -d ~/maana/data -v -q ../cluster/deploy.env.sh -c core.yml

bash ./backup_restore/do_backup.sh -r 201808161855 -d /maana/backups -t /gluster/saq -q ../cluster/deploy.env.sh -c core.yml
```

### Troubleshooting Backup & Restore

Problem: do\_backup.sh fails to flush Redis and put Consul into maintenance mode

After `do_backup.sh` scales down the necessary services, it will then flush the REDIS cache and put Consul into maintenance mode. These are done via scripted `ssh -A` calls to the nodes running those containers. If SSH keys are not configured correctly, you will see a series of log messages including:

```
Permission denied (publickey).
```

Solution:

This can sometimes be resolved by adding the below lines to your `.ssh/config` file under the entry used for SSH access to the environment. Otherwise, contact IT or Support to ensure your user has access to SSH to all nodes.

```
  AddKeysToAgent yes
  ForwardAgent yes
```

