# Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

# MYSQL DATA RESTORATION

Firstly, restore MySQL data from the backup:

    sudo -u backup duplicity restore --no-encryption rsync://manmanmano@backup.clounsible.mano//home/manmanmano/mysql/ /home/backup/restore/

Lastly, paste the retrieved MySQL dump into the database:

    mysql -u agama -p < /home/backup/restore/agama.sql 

N.B: Before pasting the restored data into the database check the contents of the file.
The contents of the file can either be checked  with nano, as the example abov or using
specific commands to view zipped files, such as zless and zcat. The restored file can
be found in /home/backup/restore/ directory.

E.G: zcat *name_of_the_file.gzip*


# INFLUXDB DATA RESTORATION

Firstly, restore InfluxDB data from the backup:

    sudo -u backup duplicity restore --no-encryption rsync://manmanmano@backup.clounsible.mano//home/manmanmano/influxdb/ /home/backup/restore/
    
Secondly, stop the telegraf service with:

    service telegraf stop

Thirdly, run:

    influx -execute 'DROP DATABASE telegraf'

Lastly, take the telegraf restored dump and put it into the database:

    influxd restore -portable -database telegraf /home/backup/restore/

In case the backup was successful, we can restart the service telegraf by running the playbook:
    
    ansible-playbook infra.yaml

N.B: Before pasting the restored data into the database check the contents of the file.
The contents of the file can either be checked  with nano, as the example abov or using
specific commands to view zipped files, such as zless and zcat. The restored file can
be found in /home/backup/restore/ directory.

E.G: zcat *name_of_the_file.gzip*
