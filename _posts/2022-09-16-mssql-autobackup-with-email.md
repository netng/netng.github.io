---
layout: post
title: "Bashscript MSSQL backup with email alert "
categories: bashscript
---

```
#!/bin/bash
#
# Created by: Nandang S.
# Created At: Jun 3, 2022 08:51 WIB
#

USER="your_sql_user"
HOST="your_sql_host"

# Deault SQL cmd execution file
SQLCMD="/opt/mssql-tools/bin/sqlcmd"

# Path where you want to put your database file backup
PATH="/path/to/your/backup/location"

# Logs backup process
LOGS="/path/to/your/backup/process/logs"

# If you want to copy your local backup to external backup
# such as nfs, etc
EXTERNAL_BACKUP_PATH="/home/vmsadmin/external-backup/vms/backup/db"

# Just a command to capture current date, needed for database file backup naming
DATE=$(/usr/bin/date +"%d%m%Y-%H%M%S")

SENDEMAIL="/usr/bin/sendemail"
FIND="/usr/bin/find"

# Put your email that you want to receive backup notifications, neither its success or failed
TO="yourmail@xxx.com"

#
# Here, all the backup functions
#

function exec() {
	$SQLCMD -S $HOST -U $USER -P $VMSSQLPWD -Q "BACKUP DATABASE [db_change_with_db_you_name_it] TO DISK = N'$PATH-$DATE.bak' WITH NOFORMAT, NOINIT, NAME = 'db_fus_vms-full-$DATE', SKIP, NOREWIND, NOUNLOAD, STATS=10" >> $LOGS/$DATE.logs

}

function main() {
	exec
	remove_older_than_30_days

	if [ $? == 0 ]; then
		/usr/bin/cp -aprf $PATH-$DATE.bak $EXTERNAL_BACKUP_PATH
		sendemail "[AUTOMATIC MAIL] Database backup success" "Backup database successfully on $(/usr/bin/date). Original backup file at $PATH-$DATE.bak and already copied to external storage at server //172.16.5.66/storage in folder backup/db (mount point on vms-server  /home/user/external-backup/app/backup/db/). See logs on $LOGS"
	else
		sendemail "[AUTOMATIC MAIL] Database backup failed" "Backup database failed on $(/usr/bin/date). See logs on server at $LOGS."
	fi
}

function sendemail() {
	local subject="$1"
	local message="$2"	

	$SENDEMAIL -f $VMSEMAIL -t $TO -u $subject -m $message  -s email.your-smtp.com:587 -o tls=yes -xu $VMSEMAIL -xp $VMSEMAILPWD
}

function remove_older_than_30_days() {
	$FIND $EXTERNAL_BACKUP_PATH -name "*.bak" -type f -mtime +30 -delete
}

main
```
