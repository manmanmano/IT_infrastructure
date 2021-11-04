Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

    sudo -u backup duplicity restore --no-encryption rsync://manmanmano@backup.clounsible.mano//home/backup/ restore/agama.sql

The contents of the file can either be seen with nano, as the example abov or using
specific commands to view zipped files, such as zless and zcat.

E.G: zcat *name_of_the_file.gzip*
