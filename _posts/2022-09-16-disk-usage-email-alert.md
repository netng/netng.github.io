---
layout: post
title: "Bashscript check disk usage with email alert"
categories: bashscript
---

```
#!/bin/bash
#
# Created by: Nandang 
# Created At: Sep 13, 2022 14:35 WIB
#

SENDMAIL="/bin/mailx"
DISK_LIMIT=70
TO="your-receiver-mail@xxx.xxx"
DF="/usr/bin/df"
GREP="/usr/bin/grep"
AWK="/usr/bin/awk"
CUT="/usr/bin/cut"

#
# Here, all the great functions
#

function exec() {
	get_disk_percentage_of_home
	get_disk_percentage_of_root
	get_disk_percentage_of_boot
}

function get_disk_percentage_of_home() {
	HOME=`${DF} -h |${GREP} /dev/mapper/centos-home | ${AWK} {'print $5'} | ${CUT} -d % -f1`

	if [[ $HOME -gt $DISK_LIMIT ]]; then
		sendmail "FIR DISK USAGE ALERT!" "Disk usage of /home need your attention. Current usage $HOME%"
	fi
}

function get_disk_percentage_of_root() {
	ROOT=`${DF} -h |${GREP} /dev/mapper/centos-root | ${AWK} {'print $5'} | ${CUT} -d % -f1`

	if [[ $ROOT -gt $DISK_LIMIT ]]; then
		sendmail "FIR DISK USAGE ALERT!" "Disk usage of /root need your attention. Current usage $ROOT%"
	fi
}

function get_disk_percentage_of_boot() {
	ROOT=`${DF} -h |${GREP} /boot | ${AWK} {'print $5'} | ${CUT} -d % -f1`

	if [[ $BOOT -gt $DISK_LIMIT ]]; then
		sendmail "FIR DISK USAGE ALERT!" "Disk usage of /boot need your attention. Current usage $BOOT%"
	fi
}


function sendmail() {
	local subject="$1"
	local message="$2"	

	$SENDMAIL -r "$PPEMAIL" -s "$subject" -S smtp="$PPSMTP:587" -S smtp-use-starttls -S smtp-auth=login -S smtp-auth-user="$PPEMAIL" -S smtp-auth-
password="$PPEMAILPWD" -S ssl-verify=ignore -S nss-config-dir="/etc/pki/nssdb/" $TO <<EOF
$message
EOF
	echo $?

}

function main() {
	exec
}

main
```
