---

layout: post

title: Gitlab数据备份到AWS S3

categories: [Gitlab,Docker,S3]

description: 将Gitlab数据备份到AWS S3

keywords: gitlab,gitlab backup,docker,s3

---

### 准备S3存储桶

region: 'cn-north-1'

aws_access_key_id

aws_secret_access_key


### 修改gitlab配置文件
```yaml
gitlab_rails['manage_backup_path'] = true
gitlab_rails['backup_path'] = "/var/opt/gitlab/backups"
gitlab_rails['backup_archive_permissions'] = 0644 # See: http://doc.gitlab.com/ce/raketasks/backup_restore.html#backup-archive-permissions
gitlab_rails['backup_pg_schema'] = 'public'
gitlab_rails['backup_keep_time'] = 604800
#gitlab_ci['backup_upload_connection'] = {
gitlab_rails['backup_upload_connection'] = {
  'provider' => 'AWS',
  'region' => 'cn-north-1',
  'aws_access_key_id' => '<yousr aws ak>',
  'aws_secret_access_key' => '<your aws sk>'
}
gitlab_rails['backup_upload_remote_directory'] = '<your bucket name>'
gitlab_rails['backup_multipart_chunk_size'] = 104857600
```
### Reconfigure gitlab

```shell
$ gitlabctl reconfiure
```

### 备份数据

```shell
$ gitlab-rake gitlab:backup:create DIRECTORY=gitlab_bakup/weekly
```
