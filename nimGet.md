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

#### nimGetVarStr(symbol) 

```perl
my ($rc,$domain) = nimGetVarStr(NIMV_HUBDOMAIN);
if($rc == NIME_OK) {
    print "$domain\n";
}
```

#### nimGetVarInt(symbol)

```perl
my ($rc,$ip) = nimGetVarStr(NIMV_ROBOTIP);
if($rc == NIME_OK) {
    print "$ip\n";
}
```

#### nimSetVarInt(symbol) 

Set new int variable.

#### nimSetVarStr(symbol) 
