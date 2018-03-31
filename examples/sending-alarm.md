# Sending an Alarm Message

Sending a Nimsoft Alarm message can assist in the integration of existing scripts with event management, or when you choose to use Perl as the programming language for system administrative tasks (for example, monitoring and batch jobs).

## Synopsis
```perl
use Nimbus::API;
my($retcode,$msgid) = =nimAlarm ($severity[,$msgtext [,$subsysid [,$supid[,$source]]]);
```
where:

- Severity and msgtext are required parameters, while the others are optional. The severity parameter may be one of the severity level constants or its corresponding number. 
- The subsysid may be a registered subsystem identification number stored in the Nimsoft Alarm Service (nas), or it may be any string.
- The supid may be used to group/tag one or several events into a state. The state may be used to notify the operator about a situation, yet remove the event from the console whenever the situation is back to normal again.
- The source may be used to impersonate any equipment so it appears as a managed element.

## API used in this example

- [NimAlarm](https://github.com/UIM-Community/Perl-SDK/blob/master/nimAlarm.md)

## Examples 

A simple example showing how to send an alarm.

```perl
use Nimbus::API;
nimAlarm(NIML_CRITICAL, "This is a critical message from perl");
```

This next example is a bit more complicated showing how to integrate a simple file counting module with Nimsoft, that should give an alarm when the number of files in the /tmp directory exceeds 3, and clears it if the number of files is 3 or less.

```perl
use Nimbus::API;
use Monitor;	# Reference to module containing FileCount
use strict;
 
my $dir = "/tmp";
####################################################################
# The subsystem-id is maintained by the Alarm Server, you may however,
# also set it to any textstring like "DirMonitor". Here we use the id.
# Hint: launch the NAS configurator and find the string tied to the id by
# looking under the subsystem tab.

my $sid = "1.1.5";
####################################################################
# The suppression tag enables the Alarm Server to keep a severity state on
# the message so it is possible to escalate the severity and/or to clear it.

my $suptag = nimSuppToStr(0,0,0,"fileMonitor/$dir");
my $count  = FileCount($dir);
 
if ($count > 3) {
  nimAlarm(NIML_CRITICAL,"Directory $dir has too many files ($count)",$sid,$suptag);
}
else {
  nimAlarm(NIML_CLEAR,"Directory $dir is checked and ok",$sid,$suptag);
}
```
