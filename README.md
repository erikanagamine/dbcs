# dbcs

Backup on DBCS

What do you need:
 - Configure the opc library.
 

```
[oracle@orcl11g odbcs]$ java -jar opc_install.jar -opcId '<user>' -opcPass '<authToken>' -container databasebkp -walletDir $ORACLE_HOME/hsbtwallet/ -libDir $ORACLE_HOME/lib/ -configfile $ORACLE_HOME/config -host https://swiftobjectstorage.us-ashburn-1.oraclecloud.com/v1/<namespace>
Oracle Database Cloud Backup Module Install Tool, build 12.2.0.1.0DBBKPCSBP_2018-06-12
Oracle Database Cloud Backup Module credentials are valid.
Backups would be sent to container databasebkp.
Oracle Database Cloud Backup Module wallet created in directory /u01/app/oracle/product/11.2.0.4/dbhome_1/hsbtwallet.
Oracle Database Cloud Backup Module initialization file /u01/app/oracle/product/11.2.0.4/dbhome_1/config created.
Downloading Oracle Database Cloud Backup Module Software Library from file opc_linux64.zip.
Download complete.

[oracle@orcl11g odbcs]$ rman

Recovery Manager: Release 11.2.0.4.0 - Production on Wed Jan 6 18:37:57 2021

Copyright (c) 1982, 2011, Oracle and/or its affiliates.  All rights reserved.

RMAN> connect target /

connected to target database: ORCL11G (DBID=1167292754)

RMAN> CONFIGURE CHANNEL DEVICE TYPE 'SBT_TAPE' PARMS 'SBT_LIBRARY=/u01/app/oracle/product/11.2.0.4/dbhome_1/lib/libopc.so, SBT_PARMS=(OPC_PFILE=/home/oracle/config)';

using target database control file instead of recovery catalog
new RMAN configuration parameters:
CONFIGURE CHANNEL DEVICE TYPE 'SBT_TAPE' PARMS  'SBT_LIBRARY=/u01/app/oracle/product/11.2.0.4/dbhome_1/lib/libopc.so, SBT_PARMS=(OPC_PFILE=/home/oracle/config)';
new RMAN configuration parameters are successfully stored

RMAN> CONFIGURE DEFAULT DEVICE TYPE TO SBT_TAPE;
CONFIGURE BACKUP OPTIMIZATION ON;
CONFIGURE CONTROLFILE AUTOBACKUP ON;
CONFIGURE CONTROLFILE AUTOBACKUP FORMAT FOR DEVICE TYPE SBT_TAPE TO '%F';
CONFIGURE ENCRYPTION FOR DATABASE ON;

new RMAN configuration parameters:
CONFIGURE DEFAULT DEVICE TYPE TO 'SBT_TAPE';
new RMAN configuration parameters are successfully stored

RMAN>
new RMAN configuration parameters:
CONFIGURE BACKUP OPTIMIZATION ON;
new RMAN configuration parameters are successfully stored

RMAN>
new RMAN configuration parameters:
CONFIGURE CONTROLFILE AUTOBACKUP ON;
new RMAN configuration parameters are successfully stored

RMAN>
new RMAN configuration parameters:
CONFIGURE CONTROLFILE AUTOBACKUP FORMAT FOR DEVICE TYPE 'SBT_TAPE' TO '%F';
new RMAN configuration parameters are successfully stored

RMAN>
new RMAN configuration parameters:
CONFIGURE ENCRYPTION FOR DATABASE ON;
new RMAN configuration parameters are successfully stored

RMAN> SET ENCRYPTION IDENTIFIED BY "password" ONLY;

executing command: SET encryption

RMAN> BACKUP INCREMENTAL LEVEL 0 SECTION SIZE 512M DATABASE PLUS ARCHIVELOG;


Starting backup at 06-JAN-21
current log archived
RMAN-00571: ===========================================================
RMAN-00569: =============== ERROR MESSAGE STACK FOLLOWS ===============
RMAN-00571: ===========================================================
RMAN-03002: failure of backup plus archivelog command at 01/06/2021 18:39:19
ORA-19554: error allocating device, device type: SBT_TAPE, device name:
ORA-27023: skgfqsbi: media manager protocol error
ORA-19511: Error received from media manager layer, error text:
   KBHS-01002: unable to open Oracle Database Backup Service Library parameter file /home/oracle/config

RMAN> CONFIGURE CHANNEL DEVICE TYPE 'SBT_TAPE' PARMS 'SBT_LIBRARY=/u01/app/oracle/product/11.2.0.4/dbhome_1/lib/libopc.so, SBT_PARMS=(OPC_PFILE=/u01/app/oracle/product/11.2.0.4/dbhome_1/config)';

old RMAN configuration parameters:
CONFIGURE CHANNEL DEVICE TYPE 'SBT_TAPE' PARMS  'SBT_LIBRARY=/u01/app/oracle/product/11.2.0.4/dbhome_1/lib/libopc.so, SBT_PARMS=(OPC_PFILE=/home/oracle/config)';
new RMAN configuration parameters:
CONFIGURE CHANNEL DEVICE TYPE 'SBT_TAPE' PARMS  'SBT_LIBRARY=/u01/app/oracle/product/11.2.0.4/dbhome_1/lib/libopc.so, SBT_PARMS=(OPC_PFILE=/u01/app/oracle/product/11.2.0.4/dbhome_1/config)';
new RMAN configuration parameters are successfully stored

RMAN> BACKUP INCREMENTAL LEVEL 0 SECTION SIZE 512M DATABASE PLUS ARCHIVELOG;


Starting backup at 06-JAN-21
current log archived
allocated channel: ORA_SBT_TAPE_1
channel ORA_SBT_TAPE_1: SID=27 device type=SBT_TAPE
channel ORA_SBT_TAPE_1: Oracle Database Backup Service Library VER=19.0.0.1
channel ORA_SBT_TAPE_1: starting archived log backup set
channel ORA_SBT_TAPE_1: specifying archived log(s) in backup set
input archived log thread=1 sequence=1 RECID=1 STAMP=1060408748
input archived log thread=1 sequence=2 RECID=2 STAMP=1060556460
input archived log thread=1 sequence=3 RECID=3 STAMP=1061145559
input archived log thread=1 sequence=4 RECID=4 STAMP=1061145604
channel ORA_SBT_TAPE_1: starting piece 1 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 1 at 06-JAN-21
piece handle=01vjvj05_1_1 tag=TAG20210106T184005 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:55
Finished backup at 06-JAN-21

Starting backup at 06-JAN-21
using channel ORA_SBT_TAPE_1
channel ORA_SBT_TAPE_1: starting incremental level 0 datafile backup set
channel ORA_SBT_TAPE_1: specifying datafile(s) in backup set
input datafile file number=00001 name=+DATA/orcl11g_iad29f/datafile/system.261.1060408381
backing up blocks 1 through 65536
channel ORA_SBT_TAPE_1: starting piece 1 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 1 at 06-JAN-21
piece handle=02vjvj1s_1_1 tag=TAG20210106T184100 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:15
channel ORA_SBT_TAPE_1: starting incremental level 0 datafile backup set
channel ORA_SBT_TAPE_1: specifying datafile(s) in backup set
input datafile file number=00001 name=+DATA/orcl11g_iad29f/datafile/system.261.1060408381
backing up blocks 65537 through 96000
channel ORA_SBT_TAPE_1: starting piece 2 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 2 at 06-JAN-21
piece handle=02vjvj1s_2_1 tag=TAG20210106T184100 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:07
channel ORA_SBT_TAPE_1: starting incremental level 0 datafile backup set
channel ORA_SBT_TAPE_1: specifying datafile(s) in backup set
input datafile file number=00002 name=+DATA/orcl11g_iad29f/datafile/sysaux.262.1060408381
backing up blocks 1 through 65536
channel ORA_SBT_TAPE_1: starting piece 1 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 1 at 06-JAN-21
piece handle=04vjvj2j_1_1 tag=TAG20210106T184100 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:15
channel ORA_SBT_TAPE_1: starting incremental level 0 datafile backup set
channel ORA_SBT_TAPE_1: specifying datafile(s) in backup set
input datafile file number=00002 name=+DATA/orcl11g_iad29f/datafile/sysaux.262.1060408381
backing up blocks 65537 through 76800
channel ORA_SBT_TAPE_1: starting piece 2 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 2 at 06-JAN-21
piece handle=04vjvj2j_2_1 tag=TAG20210106T184100 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:01
channel ORA_SBT_TAPE_1: starting incremental level 0 datafile backup set
channel ORA_SBT_TAPE_1: specifying datafile(s) in backup set
input datafile file number=00005 name=+DATA/orcl11g_iad29f/datafile/apex.270.1060434143
input datafile file number=00003 name=+DATA/orcl11g_iad29f/datafile/undotbs1.263.1060408381
input datafile file number=00004 name=+DATA/orcl11g_iad29f/datafile/users.266.1060408757
channel ORA_SBT_TAPE_1: starting piece 1 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 1 at 06-JAN-21
piece handle=06vjvj33_1_1 tag=TAG20210106T184100 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:15
Finished backup at 06-JAN-21

Starting backup at 06-JAN-21
current log archived
using channel ORA_SBT_TAPE_1
channel ORA_SBT_TAPE_1: starting archived log backup set
channel ORA_SBT_TAPE_1: specifying archived log(s) in backup set
input archived log thread=1 sequence=5 RECID=5 STAMP=1061145714
channel ORA_SBT_TAPE_1: starting piece 1 at 06-JAN-21
channel ORA_SBT_TAPE_1: finished piece 1 at 06-JAN-21
piece handle=07vjvj3i_1_1 tag=TAG20210106T184154 comment=API Version 2.0,MMS Version 19.0.0.1
channel ORA_SBT_TAPE_1: backup set complete, elapsed time: 00:00:03
Finished backup at 06-JAN-21

Starting Control File and SPFILE Autobackup at 06-JAN-21
piece handle=c-1167292754-20210106-00 comment=API Version 2.0,MMS Version 19.0.0.1
Finished Control File and SPFILE Autobackup at 06-JAN-21

RMAN>
```

