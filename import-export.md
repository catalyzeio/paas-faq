---
title: Data Import, Export, Backup
---

Data Import & Export
======================

_Catalyze CLI Version: >= 1.4.0_


## Import
All of the import functionality in the CLI starts with preparing a file to import. Here is a table outlining the file types appropriate for each supported database on the Catalyze platform.

```
Supported Import Filetype: (Database) - (File Extension)
PostgreSQL - .sql
MySQL      - .sql
MongoDB    - .tar.gz
```

In general, the import command is to be used **only** when importing data to your database rather than migrating databases from another database service. Importing a dump into Catalyze from a different database is not recommended and poses the risk of data loss. If you need to import another database, we recommend uploading this locally and then performing a data only dump to be importing into Catalyze. You also **should not** import a file retrieved from the "export" command. The export downloads a full backup of your database including users, permissions, and data. The import command should only be used to import data.

### SQL Imports
Make sure you have associated an environment and are currently in the directory of the associated git repo. Let’s create a short script to create a table and insert a few rows.

```
$ cat myimport.sql

CREATE TABLE user_roles (
    id text primary key,
    val text
);
INSERT INTO user_roles (id, val) VALUES ('1', 'admin');
INSERT INTO user_roles (id, val) VALUES ('2', 'user');
```

Now let’s import the script!

```
$ catalyze db import db01 myimport.sql
```

After it successfully finishes importing your script, the CLI will dump the output of the command back to your terminal. 

### MongoDB Imports

In this example we will start with an empty database and add some data which will be uploaded to our Catalyze database. First sign into your mongo database, we'll switch to a new database ("catalyze") and create a new collection and insert a few rows. 

```
> use catalyze
switched to db catalyze
> db.createCollection('user_roles')
{ "ok" : 1 }
> db.user_roles.insert({"id":"1", "val":"admin"})
WriteResult({ "nInserted" : 1 })
> db.user_roles.insert({"id":"2", "val":"user"})
WriteResult({ "nInserted" : 1 })
> exit
bye
```

Now create a dump of the collection:

```
$ mongodump --db=catalyze --collection=user_roles
2015-08-11T11:45:05.128+0000    writing catalyze.user_roles to dump/catalyze/user_roles.bson
2015-08-11T11:45:05.131+0000    writing catalyze.user_roles metadata to dump/catalyze/user_roles.metadata.json
2015-08-11T11:45:05.132+0000    done dumping catalyze.user_roles (2 documents)
```

This will output a directory structure in `dump/`from the same directory as where the mongodump command was run. Now all you need to do is tar the `dump/` folder and perform a similar import command. Just specify the mongo database to import data into!

```
$ tar -cvzf mymongodump.tar.gz dump/
dump/
dump/catalyze/
dump/catalyze/user_roles.metadata.json
dump/catalyze/user_roles.bson
$ catalyze db import db01 mymongodump.tar.gz --mongo-database catalyze
```

While you are using the CLI check out the "console" command to log into the mongo database shell; read [here]() for more information about the secure console command.

## Export
> ***Important Note:*** When exporting data from your database be aware that you maybe downloading PHI onto the local hard drive. Proceed with caution and insure that the appropriate disk-level encryption and access controls have been established prior to initiating a database export. 

Using the Catalyze CLI "export" command allows you to download the latest dump of your database service. The export command is easy to use and is equivalent to download a backup of your database. This may be helpful for running metrics collections offline against a production database or a variety of other uses. You **should not** import anything exported with the "export" command. To use the "export" command, you'll specify the name of the database service to export and a file path for the download location. Here is an example usage:

```
$ catalyze db export db01 ./mydbexport.sql
…
```

Please note that you should not give the export command the location of a directory but the full path to a file. This file does not need to exist as it will be created.

'db01' is the name of your database service and './mydbexport.sql' is the path where you want the export saved to. Exports are similar to using the backup process described later in this article. An export first creates a backup of your entire database. When the backup is finished it is encrypted and stored in cloud storage. Once finished, a unique temporary signed URL is retrieved and used to securely download your encrypted backup. This temporary URL will expire shortly after the download completes. Once downloaded, the file is then decrypted on your local machine and stored at the given path. Since the export creates a backup you will be able to see the record of your export when listing the backups for the database service (more about this in the Backup section below).

## Backup
The backup command of the CLI is there for you to create snapshots of your data, perhaps, in preparation for a software upgrade or data migration. A nightly backup of your database is also automated. All of these backups can be viewed with the CLI backup commands. Backups are encrypted and stored in cloud storage and retained for 7 days. The following examples will show you how to create and list database backups performed via the CLI.

### Create a Backup

For CLI versions previous to version 2.1.0, run

```
$ catalyze backup create db01
```

For CLI version 2.1.0 and above, run

```
$ catalyze db backup db01
```

List the backups for a database service. Take note that each of the backups has a corresponding ID that should be used in the case of restoring that specific backup. Also of note, if your database service is part of an HA configuration only the database identified as a primary (or master) node will be backed up nightly. Therefore when you display the backups for a secondary database node you will not see nightly backup entries but will on the primary node. 

For CLI versions previous to version 2.1.0, run

```
$ catalyze backup list db01
```

For CLI version 2.1.0 and above, run

```
$ catalyze db list db01
```

### Download a Backup
> ***Important Note:*** When downloading a database backup be aware that you maybe downloading PHI onto the local hard drive. Proceed with caution and insure that the appropriate disk-level encryption and access controls have been established prior to initiating a database export. 

If you would like to download yesterday's database backup to inspect it or maybe assist tracking down a bug you can do so with the backup download command. This command is quite similar to the database export command but in the command you'll specify the ID of the backup to download and the file path of where to download the file. The file downloaded will be of the same file format as expected for a database import (Postgres and MySQL backups will be SQL files and MongoDB backups will be downloaded as gzipped tarballs). Please note that since a downloaded backup and an export are identical, as with exports you **should not** import a downloaded backup. For CLI versions previous to version 2.1.0, run

```
$ catalyze backup list db01
```

For CLI version 2.1.0 and above, run

```
$ catalyze db list db01
```

Now choose the one you want to download and copy its ID and download it. For CLI versions previous to version 2.1.0, run

```
$ catalyze backup download db01 {backupID} ./mydbdownload.sql
```

For CLI version 2.1.0 and above, run

```
$ catalyze db download db01 {backupID} ./mydbdownload.sql
```
