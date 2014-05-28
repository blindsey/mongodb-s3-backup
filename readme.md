# Mongodb to Amazon s3 Backup Script

## Requirements

* Running mongod process
* mongodump
* mongo
* openssl
* tar
* rm
* curl

## Usage

`bash /path/to/backup.sh -k AWS_ACCESS_KEY -s AWS_SECRET_KEY -r S3_REGION -b S3_BUCKET`

Where `S3_REGION` is in the format `us-west-2` and `S3_BUCKET` is a bucket name (no periods allowed). 

## Cron

### Daily

Add the following line to `/etc/cron.d/mongodb` to run the script every day at midnight (UTC time) 

    0 0 * * * root /bin/bash /path/to/backup.sh -k AWS_ACCESS_KEY -s AWS_SECRET_KEY -r S3_REGION -b S3_BUCKET >> /var/log/mongodb/backup.log 2>&1

Or you can create a script in /etc/cron.daily/mongodb

    #!/bin/bash
    /path/to/backup.sh -k AWS_ACCESS_KEY -s AWS_SECRET_KEY -r S3_REGION -b S3_BUCKET >> /var/log/mongodb/backup.log 2>&1
