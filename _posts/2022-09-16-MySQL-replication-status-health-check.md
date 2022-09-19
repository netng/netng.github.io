---
layout: post
title: "MySQL replication status health check"
categories: bashscript
---

```
#!/bin/bash
#
# Created by: Nandang S.
# Created At: Exuseme, I forget :P
#

maximumSecondsBehind=300

email="email@example.xxx"
reportStatusPath="/scripts/healthcheck/mysql/replication"
logsPath="/scripts/healthcheck/mysql/replication/logs"
date=$(/usr/bin/date +%d-%m-%Y_%H:%M:%S)


check_status() {
	mysql -e 'SHOW SLAVE STATUS \G' | grep 'Running:\|Master:\|Error:\|Slave_SQL_Running_State:' > $reportStatusPath/replicationStatus.txt
}

show_to_console() {
	echo "Results:"
	cat $reportStatusPath/replicationStatus.txt
}

check_each_status() {
	slaveRunning="$(cat $reportStatusPath/replicationStatus.txt | grep "Slave_IO_Running: Yes" | wc -l)"
	slaveSQLRunning="$(cat $reportStatusPath/replicationStatus.txt | grep "Slave_SQL_Running: Yes" | wc -l)"
	secondsBehind="$(cat $reportStatusPath/replicationStatus.txt | grep "Seconds_Behind_Master" | tr -dc '0-9')"
}

send_email_alert() {
	mail -s "$(hostname) (DB Local) - MySQL replication issue found" $email < $reportStatusPath/replicationStatus.txt 
}

logging_it() {
	cp $reportStatusPath/replicationStatus.txt $logsPath/replicationError_$date
}

main() {
	check_status
	show_to_console
	check_each_status

	if [[ $slaveRunning != 1 || $slaveSQLRunning != 1 || $secondsBehind -gt $maximumSecondsBehind ]]; then
	  logging_it
	  echo ""
	  echo "Sending email"
	  send_email_alert
	else
	  echo ""
	  echo "Replication looks fine."
	fi
}

main
```
