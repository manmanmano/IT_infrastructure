# BACKUP COVERAGE

From our structure we backup three services: database servers MySQL and InfluxDB (the data present on the databases)
and our Ansible repository (configuration management), which contains all of the configurations done to our IT
Infrastructure services.


# RECOVERY POINT OBJECTIVE 

Backups are created every day at midnight. We can accept only 12h of data loss since the last backup.


# VERSIONING AND RETENTION

Our backups are held for a maximum of 30 days. Since we use incremental backuping, every day we store a different version, 
so 30 versions in total.


# USABILITY CHECKS

On the first day of the week we check the data that was backed up the week before. We rebuild the infrastructure from zero using 
Ansible and check the data present on the databases.


# RESTORATION CRITERIA

If within 6h the infrastructure does not respond to any of the fixing approaches and remains 
unavailable, we restore everything from the latest backup.


# RECOVERY TIME OBJECTIVE

To restore the services it will take from 2 to 4 hours.
