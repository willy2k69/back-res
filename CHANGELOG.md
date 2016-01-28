# CHANGELOG:
-----------------------------------------------------------------------------
version 0.9.6 - 2014-02-04 (by Yavuz Aydin - Vrij Media)
----------------------------------------------------------------------------

- Changed mysql import routine to create database if it doesn't exist
- Changed code to import database

-----------------------------------------------------------------------------

version 0.9.5 - 2014-01-25 (by Yavuz Aydin - Vrij Media)
----------------------------------------------------------------------------

- Removed /var from DIRECTORIES
- Added code to add all subdirectories of /var excluding /var/www and
 /var/vmail to DIRECTORIES
- Added code to add /var/www excluding subdirectories of /var/www/clients,
 all subdirectories of /var/www/clients and all subdirectories of /var/vmail
 to DIRECTORIES
- Changed variable COMPUTER to take computername from hostname -f

-----------------------------------------------------------------------------
version 0.9.4 - 2010-09-13
----------------------------------------------------------------------------

- Small fix: - Corrected small bug replaced tar with $TAR in the recovery line
of the databases. (The line: mysql -u$dbuser -p$dbpassword $rdb <) 
- Thanks goes to Nimarda and colo.

-----------------------------------------------------------------------------
version 0.9.3 - 2010-08-01
----------------------------------------------------------------------------

 - Small fix: - Modified del_old_files function to remove "/" from the $to_del
variable used to delete old files
 - Removed from del_old_files function the section used to keep old
databases (It's not working if there is no space left on device). Added
in TODO section

-----------------------------------------------------------------------------
version 0.9.2 - 2010-04-18
----------------------------------------------------------------------------

Always download the latest version here: http://www.eurosistems.ro/back-res
hanks or questions: http://www.howtoforge.com/forums/showthread.php?t=41609

- Fixes: 
 - First run now does not gives errors (Thanks nokia80, Snake12, 
udolfpietersma, HyperAtom, jmp51483, bseibenick, dipeshmehta, andypl
and all others)
 - Modified the log function to accept first time dir createin
 - Modified the starting sequence to not check the free space if the
primary backup directory does not exist
 - If primary backup dir does not exist now it's created at the start
 - Added a line to remove the maildata at the start if the user stops
the script before finishing his jobs. This prevents the script to send
incorect mails.
 - Added link http://www.howtoforge.com/forums/showthread.php?t=41609
maybe some of the downloaders will visit the forum.
 - Added first TODO

-----------------------------------------------------------------------------
beta version 0.9.1 
----------------------------------------------------------------------------

- first public release last modified 2009-12-06
- moved to http://www.eurosistems.ro/back-res.0.9.1
