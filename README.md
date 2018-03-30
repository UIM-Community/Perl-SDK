# nimsoft-perlsdk-doc
CA UIM - Nimsoft - Perl SDK Documentation

The main goal of this git is to provide a perl SDK documentation with a better visibility on all API and community works. It give a new way for the community to contribute if any problems are spotted too.

- [Original documentation](http://docs.nimsoft.com/prodhelp/en_US/Monitor/SDK/PerlSDK/index.htm?toc.htm?2186383.html)
- Some examples & references are taken from C SDK Documentation.

For a better experience find the web version [Here](https://uim-community.github.io/Perl-SDK/)

> Work in progress ( ~ **85% done** ). 

## Setup - starter guide

- [SDK_Perl on Windows](starterguide/windows.md)
- [SDK_Perl on UNIX](starterguide/unix.md)

## Overview and vocabulary

- Return code constants & explaination [Here](return_code.md)
- Configuration Item (CI) [Here](configuration_item.md)
- Full constants list [Here](constants.md)

The Perl SDK modules wrap the Nimsoft Message Bus API functions, easing the development of probes that are written in Perl.

- API.pm is the foundation Perl object, providing your interface into the Nimsoft Controller. Three other Perl objects are abstractions for making particular tasks more convenient:

   - CFG.pm - for manipulating probe configuration files
   - PDS.pm - for working with machine-independent data manipulation routines (PDS means Portable Data Stream)
   - Session.pm - for using the functions available once a Nimsoft session is established.
   
## Convensions used when prototyping the functions
  - **sz** - prefix for string
  - **i**  - prefix for integer (number)
  - **b**  - prefix for boolean (true(1)/false(0))

**rc** is the Return Code (integer)

## API 

- nimRequest & nimNamedRequest - [Here](request.md)
- [**Nimbus**] Session(s) - [Here](server.md)
- [**Nimbus**] CFG - [Here](cfg_nimbus.md)
- [**Nimbus**] PDS - [Here](pds.md)
- Probe & Session(s) (**Advanced**) - [Here](probe.md)
- CFG - [Here](cfg_cway.md)
- PDS - [Here](pds_cway.md)
- CI - [Here](nimCI.md)
- QOS - [Here](nimQOS.md) [**Contribution Welcome**]
- nimTimer - [Here](timer.md)
- nimGet - [Here](nimGet.md)
- nimFind - [Here](search.md)
- nimLog - [Here](nimLog.md)
- nimAlarm - [Here](nimAlarm.md)
- others methods - [Here](util.md)

## Example(s)

- [How to handle and parse nimRequest and nimNamedRequest PDS](examples/handlepds.md);
- [Building and Publishing a User-defined Message](examples/publishing-user-message.md)
- [Build a server solution](examples/build-server.md)
- [Subscribing to bus messages](examples/subscribing_bus.md)
- [Sending an Alarm message](examples/sending-alarm.md)
- [Sending an Alarm message (Advanced)](examples/sending-alarm_advanced.md)
- [Sending Qos Data](examples/qos.md)
- [Create & Send an Alarm (or) QoS linked to a CI](examples/ci.md)
- [Transform Hash into a PDS](examples/hash-to-pds.md)

## Troubleshooting 

#### Symptom: Scripts halt with an error message similar to:
```
Can't locate Nimbus/API.pm in @INC (@INC contains: /usr/local/lib/perl5/sun4-solaris/5.00404 /usr/local/lib/perl5 /usr/local/lib/perl5/site_perl/sun4-solaris /usr/local/lib/perl5/site_perl .) at subex.pl line 1.
BEGIN failed--compilation aborted at subex.pl line 1.
``` 

Possible causes:
1. The perllib directory structure is not reachable for Perl
   - Add PERL5LIB to your environment  (for example PERL5LIB = /opt/nimsoft/perllib)
   - Add use lib ("/opt/nimsoft/perllib") to your script header (before use Nimbus::API)
2. Perl Extensions for Nimsoft are binary incompatible with the distribution
   - Get a compatible Perl distribution (or contact Nimsoft support).

#### Symptom: You are unable to locate the perllib directory on the file system.

Possible causes:
1. The Nimsoft runtime libraries for Perl have not been installed
   - Install the runtime libraries
2. They do not reside under the root installation directory for Nimsoft
   - WIN32: c:\program files\Nimsoft\perllib
   - UNIX:    /opt/nimsoft/perllib.
   
## Know defects

- nimRequest and nimNamedRequest timeout doesn't work on both UNIX and Windows system.
- Callbacks arguments are returned as 'NULL' or '0' on UNIX systems.
- Nimbus::PDS::asHash() doesn't work well for Array values.
- nimTimerFree() doesn't work well.

## Community link(s)

[Perl probe kickstarter - Part 1 - Develop a custom Perl probe](https://communities.ca.com/docs/DOC-231172625)

[Perl probe kickstarter - Part 2 - Package and distribute](https://communities.ca.com/docs/DOC-231172657)

[Perl probe kickstarter - Part 3 - Code, debug and deploy](https://communities.ca.com/docs/DOC-231172784)

[Compiling & Installing Perl Modules on Linux](https://communities.ca.com/docs/DOC-231169163)

[SDK Perl Releases Notes](http://docs.nimsoft.com/prodhelp/en_US/Monitor/SDK/PerlSDK/ReleaseNotes/Perl%20SDK-2013%205.05.pdf)

[Configuration Items And Metrics](https://communities.ca.com/thread/241721931)

## Community Framework(s)

- Perluim [Here](https://github.com/fraxken/perluim)
- Perluim5 (Alpha stage) [Here](https://github.com/UIM-Community/perluim5)
