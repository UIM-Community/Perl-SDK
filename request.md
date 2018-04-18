# Request 

Perl SDK request are made to do callback on Nimsoft probes.

**Find an example on how to handle request response** [Here](https://github.com/UIM-Community/Perl-SDK/blob/master/examples/handlepds.md)

## nimRequest(szHostname, iProbePort, szCallback, pdsData)

Send a request over the Nimsoft Bus to a server. This function does not traverse hub tunnels, because it attempts a direct connection to the given IP/port. A firewalled environment causes difficulties.

```perl
my ($RC, $pdsRET) = nimRequest("robotName", 48000, "get_info", Nimbus::PDS->new()->data);
```

### Probes with fixed port

| probe name | port |
| --- | --- |
| controller | 48000 |
| spooler | 48001 | 
| hub | 48002 | 

### Retrieve robot name

If you want to retrieve the current (local) uim agent, use the nimGet API.

```perl
my ($RC, $Robotname) = nimGetVarStr(NIMV_ROBOTNAME);
if ($RC != NIME_OK) {
    my $nimError = nimError2Txt($RC);
    die "Unable to get the current UIM Robot name, Error ($RC): $nimError\n"
}
```

## nimNamedRequest(szAddr, szCallback, pdsData)

Send a named request over the Nimsoft Bus to a server. This function works through Hub Tunnels, because the routing of messages is up to the Hub.

```perl
my ($RC,$RES) = nimRequest(
    "/DOMAIN/HUB-NAME/ROBOT-NAME/controller",
    "get_info",
    Nimbus::PDS->new()->data
);
```

> **Note** If you create your PDS with Nimbus::PDS you have to put $PDS->data in the callback request to take in account the PDS correctly.
