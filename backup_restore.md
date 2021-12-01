# Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

# MYSQL DATA RESTORATION

1) Login into the backup user:

    sudo su backup

2) Restore MySQL data from the backup with the following command:

    duplicity restore --no-encryption rsync://manmanmano@backup.clounsible.mano//home/manmanmano/mysql/ /home/backup/restore/

3) Exit from the backup user:

    exit

4) Login into the root user:

    sudo su

5) Paste the retrieved MySQL dump into the database as root using the following command:

    mysql < /home/backup/restore/agama.sql 

N.B: Before pasting the restored data into the database check the contents of the file.
The contents of the file can either be checked  with nano, as the example abov or using
specific commands to view zipped files, such as zless and zcat. The restored file can
be found in /home/backup/restore/ directory.

E.G: zcat *name_of_the_file.gzip*


# INFLUXDB DATA RESTORATION

1) Login into the root user:

    sudo su 

2) Stop the telegraf service with the following command:

    service telegraf stop

3) Run:

    influx -execute 'DROP DATABASE telegraf'

4) Login into the backup user:

    sudo su backup

5) Restore InfluxDB data from the backup with the following command:

    duplicity restore --no-encryption rsync://manmanmano@backup.clounsible.mano//home/manmanmano/influxdb/ /home/backup/restore/

6) Take the telegraf restored dump and put it into the database:

    influxd restore -portable -database telegraf /home/backup/restore/

In case the backup was successful, we can restart the service telegraf by running the playbook:
    
    ansible-playbook infra.yaml

N.B: Before pasting the restored data into the database check the contents of the file.
The contents of the file can either be checked  with nano, as the example abov or using
specific commands to view zipped files, such as zless and zcat. The restored file can
be found in /home/backup/restore/ directory.

E.G: zcat *name_of_the_file.gzip*
