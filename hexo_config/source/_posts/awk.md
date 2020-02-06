---
title: awk
date: 2020-02-06 21:23:58
categories:
tags:
---
# users and their home paths in macOS
```bash
$ cat /tmp/user_home
BEGIN {
    print "Users and thier corresponding home"
    print " UserName \t HomePath"
    print "___________ \t __________"
    FS=":"
}
{
    if( NR> 10)
    {
        print $1 "  \t  " $6
    }
}
END {
    print "The end"
}
$ awk -f /tmp/user_home /etc/passwd
Users and thier corresponding home
 UserName 	 HomePath
___________ 	 __________
nobody  	  /var/empty
root  	  /var/root
daemon  	  /var/root
_uucp  	  /var/spool/uucp
_taskgated  	  /var/empty
_networkd  	  /var/networkd
_installassistant  	  /var/empty
_lp  	  /var/spool/cups
_postfix  	  /var/spool/postfix
_scsd  	  /var/empty
_ces  	  /var/empty
_appstore  	  /var/db/appstore
_mcxalr  	  /var/empty
_appleevents  	  /var/empty
_geod  	  /var/db/geod
_devdocs  	  /var/empty
_sandbox  	  /var/empty
_mdnsresponder  	  /var/empty
_ard  	  /var/empty
_www  	  /Library/WebServer
_eppc  	  /var/empty
_cvs  	  /var/empty
_svn  	  /var/empty
_mysql  	  /var/empty
_sshd  	  /var/empty
_qtss  	  /var/empty
_cyrus  	  /var/imap
_mailman  	  /var/empty
_appserver  	  /var/empty
_clamav  	  /var/virusmails
_amavisd  	  /var/virusmails
_jabber  	  /var/empty
_appowner  	  /var/empty
_windowserver  	  /var/empty
_spotlight  	  /var/empty
_tokend  	  /var/empty
_securityagent  	  /var/db/securityagent
_calendar  	  /var/empty
_teamsserver  	  /var/teamsserver
_update_sharing  	  /var/empty
_installer  	  /var/empty
_atsserver  	  /var/empty
_ftp  	  /var/empty
_unknown  	  /var/empty
_softwareupdate  	  /var/db/softwareupdate
_coreaudiod  	  /var/empty
_screensaver  	  /var/empty
_locationd  	  /var/db/locationd
_trustevaluationagent  	  /var/empty
_timezone  	  /var/empty
_lda  	  /var/empty
_cvmsroot  	  /var/empty
_usbmuxd  	  /var/db/lockdown
_dovecot  	  /var/empty
_dpaudio  	  /var/empty
_postgres  	  /var/empty
_krbtgt  	  /var/empty
_kadmin_admin  	  /var/empty
_kadmin_changepw  	  /var/empty
_devicemgr  	  /var/empty
_webauthserver  	  /var/empty
_netbios  	  /var/empty
_warmd  	  /var/empty
_dovenull  	  /var/empty
_netstatistics  	  /var/empty
_avbdeviced  	  /var/empty
_krb_krbtgt  	  /var/empty
_krb_kadmin  	  /var/empty
_krb_changepw  	  /var/empty
_krb_kerberos  	  /var/empty
_krb_anonymous  	  /var/empty
_assetcache  	  /var/empty
_coremediaiod  	  /var/empty
_launchservicesd  	  /var/empty
_iconservices  	  /var/empty
_distnote  	  /var/empty
_nsurlsessiond  	  /var/db/nsurlsessiond
_nsurlstoraged  	  /var/db/nsurlstoraged
_displaypolicyd  	  /var/empty
_astris  	  /var/db/astris
_krbfast  	  /var/empty
_gamecontrollerd  	  /var/empty
_mbsetupuser  	  /var/setup
_ondemand  	  /var/db/ondemand
_xserverdocs  	  /var/empty
_wwwproxy  	  /var/empty
_mobileasset  	  /var/ma
_findmydevice  	  /var/db/findmydevice
_datadetectors  	  /var/db/datadetectors
_captiveagent  	  /var/empty
_ctkd  	  /var/empty
_applepay  	  /var/db/applepay
_hidd  	  /var/db/hidd
_cmiodalassistants  	  /var/db/cmiodalassistants
_analyticsd  	  /var/db/analyticsd
_fpsd  	  /var/db/fpsd
_timed  	  /var/db/timed
_nearbyd  	  /var/db/nearbyd
_reportmemoryexception  	  /var/db/reportmemoryexception
_driverkit  	  /var/empty
The end
```
