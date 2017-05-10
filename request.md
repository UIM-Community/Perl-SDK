# Request 

Perl SDK request are made to do callback on Nimsoft probes.

**Find an example on how to handle request response** [Here](https://github.com/UIM-Community/Perl-SDK/blob/master/examples/handlepds.md)

## nimRequest(hostname,probePort,callback,pdsData)

Send a request over the Nimsoft Bus to a server. This function does not traverse hub tunnels, because it attempts a direct connection to the given IP/port. A firewalled environment causes difficulties.

```perl
my $PDS = pdsCreate();
my ($RC,$RES) = nimRequest("serverName",48000,"get_info",$PDS);
pdsDelete($PDS);
```

#### Probes with fixed port

| probe name | port |
| --- | --- |
| controller | 48000 |
| spooler | 48001 | 
| hub | 48002 | 

## nimNamedRequest(nimAddr,callback,pdsData)

Send a named request over the Nimsoft Bus to a server. This function works through Hub Tunnels, because the routing of messages is up to the Hub.

```perl
my $PDS = pdsCreate();
my ($RC,$RES) = nimRequest("/DOMAIN/HUB-NAME/ROBOT-NAME/controller","get_info",$PDS);
pdsDelete($PDS);
```
