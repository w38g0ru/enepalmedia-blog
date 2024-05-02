---
layout: post
title:  "माईएसक्युवल डाटाबेस कसरी अटोमेटिक ब्याकअप लिने (Tutorial)"
date:   2021-05-15 12:10:10 +0545
---

भिपिएस सर्भरमा वेबहोष्ट गर्नुको सबैभन्दा चुनौती भनेको ब्याक अप हो । सर्भर आफैले वेबसाइटका फाइल, डाटाबेस केही पनि ब्याक अप गर्दैन । यद्यपि भिपिएस सर्भरवालाहरूले ब्याकअपको अप्सन दिएका हुन्छन् । त्यो भनेको कस्तो हो भने तपाईँले कुने भिपिएस सर्भर खरिद गर्नु भयो भने पुरा सर्भर नै ब्याक अप राख्दीन्छ । यसले तपाईको वेबरुट फोल्डर वा डाटाबेसलाई छुट्टै ब्याक अप लिने भन्ने हुन्न । तपाईँले भुल बस कुनै फाइल डिलिट गर्नु भो र माईएसक्युवल कमान्ड लाइन ईन्टरफेस (CLI) चल्न छोड्यो भने तपाई आपतमा पर्न सक्नु हुन्छ । समस्या सामाधान गर्ने उपाया त कयौँ निस्केलान् तर तपाईँले त्यसको तनाव लिन पर्ने हुन्छ । आउनुहोस् त्यो अवस्था आउनु पूर्व नै माईएसक्युवल डाटाबेस कसरी अटोमेटिक ब्याक अप लिने त्यसबारे जानकारी लिऔँ । 

युबुन्तुमा एउटा automysqlbackup भन्ने एप्लीकेशन हुन्छ जसले दैनिक, साप्ताहिक, मासिक रूपमा माईएसक्युवल डाटाबेसको ब्याक अप लिएर कुनै फोल्डरमा सेभ गर्ने गर्दछ । यसरी ब्याक अप लिदाँ मासिक ब्याक अप महिनाको एक पटक , साप्ताहिक ब्याक अप सप्ताहको एक पटक र डेली ब्याक अप दिनको एक पटक लिने गर्दछ ।
 
यो एप्लीकेशन रन गर्नको लागी तल दिएको कमान्ड प्रयोग गर्नु पर्दछ । 
<pre>sudo apt-get install automysqlbackup</pre>

माथिको कमान्डले एप्लीकेशन ईन्सटल हुन्छ । यसलाई चालु गर्न तल दिएको कमान्ड प्रयोग गर्नु पर्दछ । 
<pre>sudo automysqlbackup</pre>

एप्लीकेशन ईन्सटल भए नभएको निर्क्योल गर्नको लागी तल दिएको कमान्ड प्रयोग गरी त्यसमा daily  monthly weekly नामका फोल्डर छ छैन चेक गर्न सकिन्छ । छन् भने डेली ब्याक अप daily भन्ने फोल्डरमा , साप्ताहिक ब्याक अप weekly फोल्डरमा र मासिक ब्याक अप monthky फोल्डरमा सेभ भएर रहेको हुन्छ । यसको लोकेसन परिवर्तन गर्ने हो भने यसको /etc/default मा रहेको automysqlbackup फाईलमा पसेर आवश्यकता अनुसार परिमार्जन गर्न सकिन्छ ।
<pre>cd /var/lib/automysqlbackup</pre>

<blockquote>
प्रो टिप्स : माईएसक्युवलको अटोमेटिक ब्याक अप लिई सके पछि ती फाइलहरूलाई तपाई जसो पनि गर्न सक्नु हुन्छ । यदि तपाईँलाई bash script आउँछ भने बढिया ! नत्र तपाई गुगल गरेर यस सम्बन्धी सहयोग लिन सक्नु हुन्छ । ब्याक अप लिएको डाटाबेसहरूलाई जिप गरेर अर्को सर्भरमा अटोमेटिक ब्याक अप गर्न सकियो । गुगल ड्राइभ , ड्रपबक्स हरुमा सेभ गर्न सकियो तर यसको लागि तपाईँलाई अलिकति यस सम्बन्धी जानकारी हुन पदर्छ। नत् तल दिए जस्तो गर्नु भयो भने पनि सर्भर एक्सेस गर्न सक्दा सम्म तपाई (एस)एफटिपी बाट नै आफ्नो कम्प्युटरमा ति फाइलहरु ट्रान्सफर गर्न सक्नु हुन्छ । भिपिएस सर्भरमा वेबसाइट होस्ट गर्दा क्रन जब (cron job) प्रयोग गरेर वेब रुट फोल्डर र डाटाब्याकअप फोल्डर छुट्टै एक ठाँऊमा सेभ गरेर राख्नु उपयुक्त हुन्छ । 
<h3>अन्य शशुल्क सेवा</h3>
[एक्स्ट्रा ब्याकअप](https://link-url-here.org)) , [एबीमाईएसक्युवल](https://www.abmysql.com/) , [व्याकअप बर्ड](https://www.backupbird.com/)
</blockquote>

कुनै स्पेशिफिक डाटाबेस चाहिँ ब्याक अप नलिने हो भने त्यसलाई सेटिङ्गमा (तल दिएको फाईल) गएर सच्याउन सकिन्छ । जस्तो उदाहरणको लागी माईएसक्युवल ईन्सटल भए सँगै ईन्सटल भएको information_schema लाई हामी एक्सक्ल्युड गरेर सेभ गर्न सक्छौ । यसको लागि तल दिएको कमान्ड प्रयोग गरी उपलब्ध सेटिङ्गहरु आफ्नो आवश्यकता अनुसार परिवर्तन गर्नु पर्दछ । 

सेटिङ्ग परिवर्तन गर्न तल दिएको कमान्ड प्रयोग गर्नुहोस । 
<pre>sudo nano /etc/default/automysqlbackup</pre>

<pre><code>
# By default, the Debian version of automysqlbackup will use:
# mysqldump --defaults-file=/etc/mysql/debian.cnf
# but you might want to overwrite with a specific user & pass.
# To do this, simply edit bellow.

# Username to access the MySQL server e.g. dbuser
#USERNAME=`grep user /etc/mysql/debian.cnf | tail -n 1 | cut -d"=" -f2 | awk '{print $1}'`

# Username to access the MySQL server e.g. password
#PASSWORD=`grep password /etc/mysql/debian.cnf | tail -n 1 | cut -d"=" -f2 | awk '{print $1}'`

# Host name (or IP address) of MySQL server e.g localhost
DBHOST=localhost

# List of DBNAMES for Daily/Weekly Backup e.g. "DB1 DB2 DB3"
# Note that it's absolutely normal that the db named "mysql" is not in this
# list, as it's added later by the script. See the MDBNAMES directives below
# in this file (advanced options).
# This is ONLY a convenient default, if you don't like it, don't complain
# and write your own.
# The following is a quick hack that will find the names of the databases by
# reading the mysql folder content. Feel free to replace by something else.
# DBNAMES=`find /var/lib/mysql -mindepth 1 -maxdepth 1 -type d | cut -d'/' -f5 | grep -v ^mysql\$ | tr \\\r\\\n ,\ `
# This one does a list of dbs using a MySQL statement.
DBNAMES=`mysql --defaults-file=/etc/mysql/debian.cnf --execute="SHOW DATABASES" | awk '{print $1}' | grep -v ^Database$ | grep -v ^mysql$ | grep -v ^performance_schema$ | grep -v ^information_schema$ | tr \\\r\\\n ,\ `

# Backup directory location e.g /backups
# Folders inside this one will be created (daily, weekly, etc.), and the
# subfolders will be database names. Note that backups will be owned by
# root, with Unix rights 0600.
BACKUPDIR="/var/lib/automysqlbackup"

# Mail setup
# What would you like to be mailed to you?
# - log   : send only log file
# - files : send log file and sql files as attachments (see docs)
# - stdout : will simply output the log to the screen if run manually.
# - quiet : Only send logs if an error occurs to the MAILADDR.
MAILCONTENT="quiet"

# Set the maximum allowed email size in k. (4000 = approx 5MB email [see
# docs])
MAXATTSIZE="4000"

# Email Address to send mail to? (user@domain.com)
MAILADDR="root"

# ============================================================
# === ADVANCED OPTIONS ( Read the doc's below for details )===
#=============================================================

# List of DBBNAMES for Monthly Backups.
MDBNAMES="mysql $DBNAMES"

# List of DBNAMES to EXLUCDE if DBNAMES are set to all (must be in " quotes)
DBEXCLUDE="information_schema"

# Include CREATE DATABASE in backup?
CREATE_DATABASE=yes

# Separate backup directory and file for each DB? (yes or no)
SEPDIR=yes

# Which day do you want weekly backups? (1 to 7 where 1 is Monday)
DOWEEKLY=6

# Choose Compression type. (gzip or bzip2)
COMP=gzip

# Compress communications between backup server and MySQL server?
COMMCOMP=no

# Additionally keep a copy of the most recent backup in a seperate
# directory.
LATEST=no

#  The maximum size of the buffer for client/server communication. e.g. 16MB
#  (maximum is 1GB)
MAX_ALLOWED_PACKET=

#  For connections to localhost. Sometimes the Unix socket file must be
#  specified.
SOCKET=

# Command to run before backups (uncomment to use)
#PREBACKUP="/etc/mysql-backup-pre"

# Command run after backups (uncomment to use)
#POSTBACKUP="/etc/mysql-backup-post"

# Backup of stored procedures and routines (comment to remove)
ROUTINES=yes
</code></pre>

