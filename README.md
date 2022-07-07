# mkbackup

`mkbackup` - make compressed backups of directories.


## Overview

`mkbackup` is a take off of `mkdir`, but instead of creating directories, this
script creates backup files of target directories.
The newly created backup files are automatically datestamped, and an argument
may be used to specify how many backup files to keep.

The intention is for `mkbackup` to be executed as a cron job to perform regular
backups of particular directories.


## Usage

```
Usage: mkbackup [OPTION] ...

Options:
  -t <directory>  Target directory to backup. (default=current directory)
  -o <directory>  Output directory of backup file. (default=current directory)
  -l <name>       Name of prefix used to label backup file. (default=backup)
  -n <int>        The maximum number of backup files to keep. Files beyond
                  the limit will be automatically deleted. (default=10)
```


## Example

```
$ mkbackup -t app -o ~/backups -n 10

Archiving files ...
...

Created backup: /home/user/backup-20220707-180000.tar.gz
```

This will create a backup file of the `app` directory, placing it in a folder
called `backups`. Only the latest `10` backup files will be kept. (i.e. any
backup files beyond `10` will be removed).


## Extraction

The contents of the backup file may be extracted as follows:

```
$ tar xvf <file>
```

Or, if you ran the backup script as `root`, you may want to preserve the
ownership of the extracted files:

```
$ tar --same-owner -x -v -f <file>
```
