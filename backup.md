## Backup scripts for server -> backed up on windows drive


### Backup script on linux machine

**Important** - `chmod a+x` on backupscript

```
#
# Backup script for stephan
#

DIRTOBACK="/home/stephan/work/."
TARGETDIR="/home/stephan/backup/work/"
ZIPTARGET="${TARGETDIR}"
ZIPFILE="/home/stephan/backup/stefbox.zip"
TARFILE="/home/stephan/backup/stefbox.tar.gz"

MAXSIZE="100M"
LOGFILE="/home/stephan/backup/backup.log"

# First rsync the data
rsync -zavh --max-size=${MAXSIZE} --exclude '00_programs/iontorrent_git' --verbose --delete -log-file ${LOGFILE} ${DIRTOBACK} ${TARGETDIR}


# Now zip it
#rm -f ${ZIPFILE}
#zip -1 -r ${ZIPFILE} ${ZIPTARGET}
rm -f ${TARFILE}
#tar cfzv ${TARFILE} ${ZIPTARGET}
tar cvf - ${ZIPTARGET} | pigz > ${TARFILE} 1> ${LOGFILE}
```

### Cron job on linux machine

    export EDITOR=nano
    crontab -e
    0 22 * * * /home/stephan/backupscript/backup.sh



### Job on Windows machine


http://wiki.vpslink.com/Automate_Backup_Retrieval_with_WinSCP
