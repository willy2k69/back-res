# The back-res script by go0ogl3

Copyright (c) go0ogl3 gabi@eurosistems.ro
If you want to reward my work donate a small amount with Paypal (use my mail)

If you enjoy him script please register and say thank you here: 
http://www.howtoforge.com/forums/showthread.php?t=41609
This is to keep the thread alive so this script can help other people too.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

The above copyright notice and this permission notice shall be included in
all copies of the script.

# Description

Full dir, mysql and incremental backup script
Full and incremental restore script
It's meant to use minimum resources and space and keep a loooong backup.
I've tried to make as more checks as possible but I can't beat "smart" users.
Weird things can happen if your backup dirs includes the "-" or "_" chars.
Those chars are used by this script and files formed by the script.

# Use

                        ============================- Backup part -============================

Important!!! Make sure your system has a correct date. Suggestion: use ntp.
Backup is not meant to be interactive, it's meant to be run daily from cron.
That's why the log for backup is kept in logdir $BACKUPDIR/log/backup.log
On the 1st of the month a permanet full backup is made.
The rest of the time an incremental backup is made, by date.
Databases are at full allways and the script makes an automatic repair and
optimizes the databases before the backup.

Warning!!!
If you set the "del_en" variable to "yes" the script will delete the old
backups to make room for the new ones. Read on.

Warning!!!
All incremental backups and databases for a month will be deleted if space
is less than the maximum percent of used space "maxp".

You need to take care to not enter in an endless loop if you set del_en="yes"
The loop can happen if deleted files form $BACKUPDIR don't decrease the 
percent of used space
The script check for some dirs and files and it's supposed to be run as root
The script is supposed to be run daily from cron at night like
40 3 * * *      /etc/back-res 1>/dev/null 2>/dev/null
This scripts verifies and corrects all errors found in ALL mysql databases
The script also makes full backups of ALL mysql databases every time it's run

                        ============================- Restore part -============================

Restore is meant to be little interactive, the messages are on standard output
Dir's are restored verbose with tar by default.

Last minute of the day "$hm" is set to 2359 but the backup is started at 03:40
so this should be set AFTER the backup has ended! At 23:59 of the backup day 
we can have many files modified from the 03:40. The not so perfect solution is
to backup later in the day (23:00) and hope the backup finishes until 23:59
My server is still loaded on the 23:00, so I use 03:40 in cron and hm=2359
because a full backup last for more than 16 hours for tar.bz2.
For sure I will loose all files created between 03:40 and 23:59 of that day.
To prevent that I can restore files one day AFTER the day I want to restore
and use find --newer to delete unwanted files.

To restore dirs make sure you have the full backup from that month and use:

`back-res dir /etc 2009-11-23 /`  -> to restore the "/etc" dir from date 2009-11-23 to root

`back-res dir /etc 2009-11-23 /tmp`  -> is used to restore the "/etc" dir to /tmp

`back-res dir all 2009-11-23 /` -> to restore all directories from date 2009-11-23 to root

To restore databases use:

`back-res db mysql 2009-11-23` -> to restore the "mysql" database from date 2009-11-23 to local mysql server

`back-res db all 2009-11-23` -> to restore all databases from date 2009-11-23 to local mysql server
