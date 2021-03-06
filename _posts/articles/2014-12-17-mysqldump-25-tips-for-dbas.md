---
layout: article
title: "Mysqldump -- 25 Tips for DBAs"
modified:
categories: articles
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2014-12-17T18:10:48+08:00
---

<div class="format_text entry-content">
<p><strong>1) Is mysqldump text backup or binary backup</strong><br>
It is a text backup . If you open the backup file you will see all the statements that can be used to recreate databases and objects . It also has the insert statements to populate the tables with data</p>
<p><strong>2) What is the syntax for mysqldump ?</strong><br>
mysqldump -u [uname] -p[pass] –databases [dbname][dbname2] &gt; [backupfile.sql]</p>
<p><strong>3) How to backup all databases using mysqldump ?</strong><br>
mysqldump -u root -p –all-databases &gt; backupfile.sql</p>
<p><strong>4) How to backup specific databases using mysqldump ?</strong><br>
mysqldump -u root -p –databases school hospital &gt; backupfile.sql</p>
<p><strong>5) How to backup specific tables using mysqldump ?</strong><br>
mysqldump –user=root –password=mypassword -h localhost databasename table_name_to_dump table_name_to_dump_2 &gt; dump_only_two_tables_file.sql</p>
<p><strong>6) I do not want the data .How to get DDL only ?</strong><br>
mysqldump -u root -p –all-databases –no-data &gt; backupfile.sql</p>
<p><strong>7) How much time does a mysqldump backup take ?</strong><br>
It actually depends on the size of the database. A database of 100 GB size might take 2 hours or more</p>
<p><strong>8) How to backup remote database that resides on other server ?</strong><br>
mysqldump -h 172.16.25.126 -u root -ppass dbname &gt; dbname.sql<br>
<strong>9) What is the significane of –routines option ?</strong><br>
The output generated by using –routines containsCREATE PROCEDURE and CREATE FUNCTION statements to re-create the routines. If you have procedures or functions you need to use this option</p>
<p><strong>10) How to list all the available options in mysqldump</strong><br>
mysqldump –help<br>
<strong>11) What are the most common options used in mysqldump ?</strong></p>
<p>All-databases<br>
Databases<br>
Routines<br>
Single-transaction (It will not lock tables) – Always use for innodb databases<br>
Master-data – replication (Ignore for now)<br>
No-data – It will dump a blank database without data<br>
<strong>12) Are triggers backed up by default ?</strong><br>
Yes</p>
<p><strong>13) What is the significance of single transaction option ?</strong><br>
–singletransaction option avoids any locks during backup for innodb databases. No locking during backup if we use this option</p>
<p><strong>14) What is the most common command used to backup using mysqldump ?</strong><br>
nohup mysqldump –socket=mysql.sock –user=user1 –password=pass –single-transaction –flush-logs –master-data=2 –all-databases –extended-insert –quick –routines &gt; market_dump.sql 2&gt; market_dump.err &amp;</p>
<p><strong>15) How to compress a backup taken by mysqldump ?</strong><br>
Note: Compression might slow down the backup<br>
Mysqldump [options] | gzip &gt; backup.sql.gz</p>
<p><strong>16) Is mysqldump ideal for large databases ?</strong><br>
Depending on your hardware, including available RAM and hard drive speed, an appropriate database size is between 5GB and 20GB. While it is possible to use mysqldump to back up a 200GB database, this single thread approach takes time to execute</p>
<p><strong>17) How to restore the backup taken by mysqldump ?</strong><br>
a) Use source method<br>
b) Mysql –u root –p &lt; backup.sql</p>
<p><strong>18) I want to record the errors in a log during recovery .. I also want to see the execution time of recovery ?</strong><br>
Time Mysql –u root –p &lt; backup.sql &gt; backup.out 2&gt;&amp;1</p>
<p><strong>19) How to know if the restore is running ?</strong><br>
Show full processlist</p>
<p><strong>20) What is something you have to do if the database is huge ?</strong><br>
Run it in the background using nohup</p>
<p><strong>21) Can I take mysqldump backup on windows and restore to linux server ?</strong><br>
Yes</p>
<p><strong>22) How do I transfer files onto the target server ?</strong><br>
a) Use scp<br>
b) Use sftp<br>
c) Use winscp</p>
<p><strong>23) What happens if I use source on a big backup file to restore ?</strong></p>
<p>If you source a big backup file , it might take forever to run &nbsp;. Better way of handling this situation is using nohup to run in the background</p>
<p>Alternate solution is to use screen in unix</p>
<p><strong>24) Does mysqldump contain drop database by default ?</strong></p>
<p>You may need to add &nbsp;the option –add-drop-database</p>
<p><strong>25) How to extract one database backup out of a multiple database backup. (Assume the database name is test)</strong></p>
<pre>sed -n '/^-- Current Database: `test`/,/^-- Current Database: `/p' fulldump.sql &gt; test.sql</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
</div>

source: <a href="http://mysqlblogger.net/mysqldump-25-tips-for-dbas/">http://mysqlblogger.net/mysqldump-25-tips-for-dbas/</a>
