# nimsoft-perlsdk-doc
CA UIM - Nimsoft - Perl SDK Documentation

The goal of this github is to provide a complete and young documentation with better explaination & examples.

Original documentation [Here](http://docs.nimsoft.com/prodhelp/en_US/Monitor/SDK/PerlSDK/index.htm?toc.htm?2186383.html)
Some examples & references taken from C SDK Documentation.

> Work in progress ( ~ 50% done ). 

## Starter guide

- [SDK_Perl on Windows](starterguide/windows.md)
- SDK_Perl on UNIX

## Overview 

- Return code [Here](return_code.md)
- Configuration Item (CI) [Here](configuration_item.md)

## API 

- nimRequest & nimNamedRequest - [Here](request.md)
- [**Nimbus**] Session(s) - [Here](server.md)
- Probe & Session(s) (Advanced) - [Here](probe.md)
- [**Nimbus**] CFG - [Here](cfg_nimbus.md)
- CFG - [Here](cfg_cway.md)
- [**Nimbus**] PDS - [Here](pds.md)
- PDS - [Here](pds_cway.md)
- CI
- QOS
- nimFind - [Here](search.md)
- nimLog - [Here](nimLog.md)
- nimAlarm - [Here](nimAlarm.md)
- others methods - [Here](util.md)

## Example(s)

- [How to handle and parse nimRequest and nimNamedRequest PDS](examples/handlepds.md);
- [Building and Publishing a User-defined Message](examples/publishing-user-message.md)
- [Build a server solution](examples/build-server.md)
- Build a server solution (Advanced)
- [Sending an Alarm message](examples/sending-alarm.md)
- [Sending an Alarm message (Advanced)](examples/sending-alarm_advanced.md)

## Community link(s)

[Perl probe kickstarter - Part 1 - Develop a custom Perl probe](https://communities.ca.com/docs/DOC-231172625)

[Perl probe kickstarter - Part 2 - Package and distribute](https://communities.ca.com/docs/DOC-231172657)

[Perl probe kickstarter - Part 3 - Code, debug and deploy](https://communities.ca.com/docs/DOC-231172784)

[Compiling & Installing Perl Modules on Linux](https://communities.ca.com/docs/DOC-231169163)

[SDK Perl Releases Notes](http://docs.nimsoft.com/prodhelp/en_US/Monitor/SDK/PerlSDK/ReleaseNotes/Perl%20SDK-2013%205.05.pdf)

## Community Framework(s)

- Perluim [Here](https://github.com/fraxken/perluim)
- Perluim5 (Alpha stage) [Here](https://github.com/UIM-Community/perluim5)
