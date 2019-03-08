# Ansible Role: DB Backup

Creates daily, weekly, monthly & yearly database backups.

After running the playbook the backups will be stored in the next structure:

    /path/to/backup
    ├── hourly
    │   └── 2019-03-08T09:29:44Z.sql.gz
    │   └── ...
    ├── daily
    │   └── 2019-03-08T09:29:44Z.sql.gz
    │   └── ...
    ├── monthly
    │   └── 2019-03-08T09:29:44Z.sql.gz
    │   └── ...
    ├── weekly
    │   └── 2019-03-08T09:29:44Z.sql.gz
    │   └── ...
    └── yearly
        └── 2019-03-08T09:29:44Z.sql.gz
        └── ...
     `
The playbook should run every hour. It automatically checks if new dump should be done and prunes stale backups.

  - **hourly:** interval - 3 hours, max age - 1 day, 8 backups to keep
  - **daily:** interval - 1 day, max age - 1 week,  7 backups to keep
  - **weekly:** interval - 1 week, max age - 4 weeks, 4 backups to keep
  - **monthly:** interval - 4 weeks, max age - 48 weeks, 12 backups to keep
  - **yearly:** interval - 48 weeks, max age - 480 weeks, 10 backups to keep

## Role Variables

    database: database_name

A database to backup.

    local_path: /path/to/backup

A path to store backups.

## Example Playbook

    - hosts: host
      vars:
        database: database_name
        local_path: /path/to/backup
      roles:
        - { role: danylevskyi.db_backup }

## License

MIT
