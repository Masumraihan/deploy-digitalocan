### Step 1: Create the Backup Script
## Create the script:
```bash
  sudo nano /usr/local/bin/mongodb-backup.sh

```

## Paste this:

```bash
  #!/bin/bash

  # Variables
  BACKUP_DIR="/var/backups/mongodb"
  DATE=$(date +%F-%H%M)
  BACKUP_PATH="$BACKUP_DIR/backup-$DATE"
  
  # Create backup directory if it doesn't exist
  mkdir -p "$BACKUP_DIR"
  
  # Run mongodump to backup ALL databases
  mongodump --out "$BACKUP_PATH"
  
  # Delete backups older than 7 days
  find "$BACKUP_DIR" -type d -mtime +7 -exec rm -rf {} \;
```
## Save and exit, then make it executable:
```bash
  sudo chmod +x /usr/local/bin/mongodb-backup.sh

```

### Step 2: Schedule Daily Cron Job
## Edit the crontab:

```bash
sudo crontab -e

```

## Add this line to run the backup every day at 12:00 AM:

```bash
  0 0 * * * /usr/local/bin/mongodb-backup.sh >> /var/log/mongodb-backup.log 2>&1
```

### Step 3: Test It

## Run the script manually once to confirm it works:

```bash
  sudo /usr/local/bin/mongodb-backup.sh
```
## Then check:

```bash
  ls /var/backups/mongodb
```

