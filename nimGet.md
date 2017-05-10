# nimGet API

nimGet methods are created to retrieve or transform information retrieved from local robot/hub.

## Constants 

| Constants | Type | Description |
| --- | --- | --- |
| NIMV_CONTIP | string | Controller IP |
| NIMV_CONTPORT | int | Controller Port |
| NIMV_SPOOLIP | string | Spooler IP |
| NIMV_SPOOLPORT | int | Spooler Port |
| NIMV_HUBIP | string | HUB IP |
| NIMV_HUBPORT | int | HUB Port | 
| NIMV_DEF_HUBPORT | int | N.A |
| NIMV_HUBADDR | string | Hub nimbus addresse | 
| NIMV_HUBDOMAIN | string | Hub domain |
| NIMV_DEF_CONTPORT | int | N.A |
| NIMV_DEF_SPOOLPORT | int | N.A |
| NIMV_ROBOTIP | string | Robot IP |
| NIMV_HUBNAME | string | Hub name |
| NIMV_PROBEID | int | Probe id | 

## API 

#### nimGetNameToIp(szName)

Look up a NimBUS address to find the IP address and port number to connect to, used together with
nimSessionConnect or nimSession. Use nimNamedSession instead.

```perl
my($rc,$szIp,$iPort) =  nimGetNameToIp ($szName);
```

#### nimGetIpToName(szIp,szPort);

Transform nimbus ip and port into a nimbus addr.

```perl
my($rc,$szName) =  nimGetIpToName ($szIp,$iPort);
```


#### nimGetVarStr(symbol) 

Get the requested API value. Typically used for fetching the current hub, spooler or controller IP.

```perl
my ($rc,$domain) = nimGetVarStr(NIMV_HUBDOMAIN);
if($rc == NIME_OK) {
    print "$domain\n";
}
```

#### nimGetVarInt(symbol)

Return the requested API value. E.g. what = NIMV_SPOOLPORT returns the local spooler port

```perl
my ($rc,$ip) = nimGetVarStr(NIMV_ROBOTIP);
if($rc == NIME_OK) {
    print "$ip\n";
}
```

#### nimSetVarInt(symbol) 

Set the named API variable. Typically used to change the default spooler port.

#### nimSetVarStr(symbol) 

Set a new API value. Typically used to change default spooler IP.
