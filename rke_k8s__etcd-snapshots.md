# ETCD_Snapshots.md

rke-v1.2.3 etcd snapshot-save \
--config cluster.yml \
--name snapshot-20210118T0745

Saves to: /opt/rke/etc-snapshots
   You can mount an NFS volume there, or you can configure RKE to copy the snapshot to S3.

Save to an S3 bucket
---------------------
$ rke etcd snapshot-save \
--config cluster.yml \
--name snapshot-name \
--s3 \
--access-key S3_ACCESS_KEY \
--secret-key S3_SECRET_KEY \
--bucket-name s3-bucket-name \
--folder s3-folder-name \ # Optional - Available as of v0.3.0
--s3-endpoint s3.amazonaws.com


The backup snapshot can be stored on a custom S3 backup like minio. If the S3 backend uses a self-signed or custom certificate, provide a custom certificate using the --s3-endpoint-ca to connect to the S3 backend.

By default: The service key value pair to set in the cluster.yml file is at:

```
services:
 ...   ...   ...      #  (near bottom of array)
  backup_config:
    interval_hours: 6   # (six is the default)
    retention: 8   # means Rancher will keep 8 back up files
    s2backupconfig:
      access_key: XXXXX
      secret_key: YYYYY
      bucket_name: <name-of-bucket>
      folder: <etcd-snapshots-folder-name>
      endpoint: s3.us-east-1.amazonaws.com
 ```     
      
In a blank cluster.yml file the service start at about line 20.    
```
services:
  etcd:
    image: ""
    extra_args: {}
    extra_binds: []
    extra_env: []
    win_extra_args: {}
    win_extra_binds: []
    win_extra_env: []
    external_urls: []
    ca_cert: ""
    cert: ""
    key: ""
    path: ""
    uid: 0
    gid: 0
    snapshot: null
    retention: ""
    creation: ""
    backup_config: null
```


### Restore
   Settings in cluster.yml

restore:
  restore: false
  snapshot_name: ""
