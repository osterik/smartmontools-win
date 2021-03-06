Smartmontools for Windows written by Orsiris "Ozy" de Jong
Doc Rev 1.4 (C) 2012-2013           http://www.netpower.fr
----------------------------------------------------------


For command line usage see below

Smartmontools For Windows is an alternate package for smartmontools by Bruce Allen and Christian Franke, and has been created to quickly install smartmontools as service, support mail or local alerts, and preconfigure smart monitor options.
Installation can be run silently with command line parameters for massive deployments, or graphically for standard users.

Configuration files are automatically generated (but you can still enjoy manual editing of course).
A service called "SmartD" is created and launched at system startups. This service will enumerate hard disks smartmontools can monitor and send an email and/or show a local message in case of errors.
A file called smart.log is created on error, including all smart information, and sent by mail. A error action log is created under erroraction.log.

Optionally, an initial smart.log file is kept on the disk, in the case you want to keep initial smart infos for warranty issues.

This software and the software it installs are under GPL licence. No responsibility will be taken for any problems or malfunctions that may occur while using this software.

But feel free to send a mail to ozy [at] netpower.fr for limited support on my free time.
Also, if you like this work or use it in your business, feel free to sponsor my project on my site, 99% of benefits will probably go into the coffee machine :)

This installer uses the following software

- smartmontools by Bruce Allen & Christian Franke, http://smartmontools.sourceforge.net
- sendemail by Brandon Zehm, http://caspian.dotconf.net
- Inno Setup by Jordan Russel, http://www.jrsoftware.org
- Gzip by Free Software Foundation, Inc. Copyright (C) 1992, 1993 Jean-loup Gailly, http://gnuwin32.sourceforge.net/
- Base64 by Matthias G�rtner, http://www.rtner.de/software/base64.htm

Command line parameters
-----------------------

smartmontools-win-6.2-1.exe [--short=S/../.././08] [--long=L/../../5/12] [--hddlist="/dev/pd0;/dev/csmi0,1"] [--checkhealth=(yes|no)] [--checkataerrors=(yes|no)] [--checkfailureusae=(yes|no)] [--reportselftesterrors=(yes|no] [--reportcurrentpendingsect=(yes|no)] [--reportofflinependingsect=(yes|no)] [--trackchangeusageprefail=(yes|no)] [--ignoretemperature=(yes|no)] [--powermode=(never|sleep|standby|idle)] [--maxskips=7] [-f source@mail.tld -t destination@mail.tld -s smtp.server.tld [-u smtpuser] [-p smtppassword] [--tls=no]] [--localmessages=(yes|no)] [--warningmessage="Your custom alert message"] [--compresslogs=(yes|no)] [--keepfirstlog=(yes|no)] [--sendtestmessage=(yes|no)] [/silent]

--short=S/../.././13 Regular expression that determines when to run short selftest, set to everyday ay 08AM if not defined (see below or smartd.conf manual for details)
--long=L/../../5/12 Regular expression that determines when to run long selftest, set to friday at 13AM if not defined (see below or smartd.conf manual for details)
--hddlist="/dev/pd0;/dev/pd1;/dev/sdc" Device list separated by semicolons. If not defined, hdds will be autodetected.
Example: --hddlist="/dev/csmi0,0;/dev/csmi0,1" for an Intel RAID of two disks (intel raid autodetection does not always work, this does)
--checkhealth=(yes|no) is activated by default, Check SMART health
--checkataerrors=(yes|no) is activated by default, Report increases in ATA errors
--checkfailureusage=(yes|no) is activated by default, Check for failures in usage attribs
--reportselftesterrors=(yes|no) is activated by default, Report increases in selftest errors
--reportcurrentpendingsect=(yes|no) is activated by default, Report nonzero Current Pending Sect
--reportofflinependingsect=(yes|no) is activated by default
--trackchangeusageprefail=(yes|no) is activated by default, Track changes in usage + prefail attribs
--ignoretemperature=(yes|no) is activated by default, Ignore temperatures changes
--powermode=(never|sleep|standby|idle) Determines in which minimal powermode is required for selftests to be run. Is set to sleep if not defined
--maxskips=N Maximum number of tests to skip because of the powermode before a test is forced. Is set to 7 by default

-f Email address your alert mail will come from
-t destination email address for your alert
-s your smtp server
-u your smtp server username (not mandatory)
-p your smtp server password (not mandatory)
--tls (no|auto|yes) Use of TLS s�curity, is no if not defined
--localmessages=(no|yes) Display local warning messages on errors, is set to no if not defined
--warningmessage="Your custom warning message", if not set, the default warning message will be used
--compresslogs=(yes|no) is activated if not defined
--keepfirstlog=(yes|no) is activated if not defined
--sendtestmessage=(yes|no)  is activated if not defined
/silent or /verysilent are silent switches. Please be aware these are the only switches using a slash, as they are Inno Setup internal logic switches.

See examples below

Selftest regular expressions
----------------------------

Regular expressions would look like T/MM/DD/d/HH where
T = type of test (S=short, L=long)
MM = Month (January = 01, December = 12)
DD = Day of month (01...31)
d = Day of week (Monday = 1, Sunday = 7)
HH = Hour in 24H format

You can replace any date/time related value by points, which are wildcards. The following regular expression would schedule a long test every tuesday and friday at 02AM:

L/../../[2,5]/02

Examples
--------

A basic installation script:

smartmontools-win-6.2-1.exe -f sourcemail@example.tld -t destination@example.tld -s smtp.of.your.isp.com /silent

This line would silently install smartmontools mail alerts, autodetection of hdds, using all monitor parameters, and schedule a short selftest every day at 08AM and a long selftest every friday at 12AM.

An other example would be that would use tls for mails, authentificate on your ISP's SMTP server, never ignore temperature changes, show local warning messages and have a short selftest every day at 09AM and a long selftest every tuesday and sunday at 02PM for the drives /dev/pd0 and /dev/csmi0,1 would look like

smartmontools-win-6.2-1.exe -f sourcemail@example.tld -t destination@example.tld -s smtp.of.your.isp.com -u username@smtp.server.tld -p pA55W0RD --tls=yes --ignoretemperature=no --hddlist=/dev/pd0;/dev/csmi0,1 --short=S/../.././09 --long=L/../../[2,7]/02 --localmessages=yes /silent


--------------------------------------------------------------

