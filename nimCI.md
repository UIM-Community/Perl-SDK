# The Configuration Item functions

A Configuration Item (CI) is an entity with a set of properties associated 
with it. As an example a disk can be described by manufacturer, volume name, 
device, size etc. Data on Configuration Items is stored in the NIS database. 

A Configuration Item Metric is a monitoring point in a CI. A CI can have 
several Metrics associated with it. As an example a set of CPU metrics could 
contain the Wait, System, Idle and Used metrics.  A metric is roughly 
equivalent to a QoS object in this regard. 

A monitored computer system will typically have one or more devices that are 
being montored. Each of these devices will have one or more Configuration 
Items, which again have one or more Metrics associated with them. Alarms and
QoS messages are bound to the CI and the Metric for the specific monitoring 
point the message is generated for.

> **Warnings**: CI Methods only work if your script is correctly logged to NimBus !

## API

#### ciOpenRemoteDevice(szCIType, szName, szIp) -> hCI
Open a handle to a remote device.

```perl
# ci_type 2.1 = Network.device
my ($hCI) = ciOpenRemoteDevice('2.1', 'device_name', 'device_ip');
if(!defined($hCI)) {
    print STDERR "Failed to open new CI on remoteDevice 'device_name'\n";
}
```

#### ciOpenLocalDevice(szCIType, szName) -> hCI
Open a handle to a local device. (On the same system as the Nimsoft agent).

```perl
# ci_type 1.1 = System.Disk
my ($hCI) = ciOpenLocalDevice('1.1', 'D:');
if(!defined($hCI)) {
    print STDERR "Failed to open new CI on localDevice 'D:'\n";
}
```

**Base categories of ciType are :**

| ci_id | name |
| --- | --- |
| 1 | System |
| 2 | Network |
| 3 | Application |
| 4 | Database |
| 9 | Private |

All new ci_type created have to be set under the category nine. This category will be conserved when the product will be upgraded for example.

#### ciClose(hCI) -> rc
Close a (CI) handle

```perl
my ($hCI) = ciOpenLocalDevice('1.1', 'D:');
ciClose($hCI);
```

#### ciRelationship(hCIParent, hCIChild) -> rc
Set a parent/child relantionship between to devices

#### ciAttributeString(hCI, szKey, szValue) -> rc
Set a string attribute in a handle 

#### ciAttributeNumber(hCI, szKey, iValue) -> rc
Set a numeric attribute in a handle 

#### ciBindQoS(hCI, hQos, szMetric) -> rc
Bind a QoS to a metric on a device

```perl
my ($hCI) = ciOpenRemoteDevice('2.1', 'device_name', 'device_ip');
my $QoS = nimQoSCreate("QOS_NAME", "device_name", 30, -1);
ciBindQoS($hCI, $QoS, "2.1:1");
# Play here with QoS
# Send alarm... They will be linked as metric of the QoS
ciUnBindQoS($QoS);
ciClose($hCI);
```

#### ciUnBindQoS(hQoS) -> rc
Remove the binding to a device in a QoS handle

#### ciGetCachePath() -> (rc, szNisCachePath)
Get the path to the component information cache on the local system

```perl
my ($RC, $nisCachePath) = ciGetCachePath();
print "$nisCachePath\n" if $RC == NIME_OK;
# will output something like: /opt/nimsoft/niscache
```

#### ciSessionAlarm(nims, ...arguments) -> (rc, szId)
Send an alarm bound to a metric on a device using a session to the spooler

Nims argument is the Nimbus session.

```perl
my $sess = Nimbus::Session->new("id-server",$optional_sessions);
if ($sess->server (NIMPORT_ANY,\&timeout,\&restart) == NIME_OK) {
    # NimBus session is only available when $sess->server is triggered and when it returned NIME_OK
    my $nims = $sess->{SERVER_SESS};
    $sess->dispatch();
}
```

> Arguments are the same as ciAlarm (except nims).

#### ciAlarm(...arguments) -> (rc, szId)

All available arguments are the following: 

| Argument name | Description |
| --- | --- |
| hCI | the CI handle from ciOpen[Remote|Local]Device |
| szMetric | the name of the metric |
| iLevel | the alarm level (severity) - see constants |
| szMsg | the alarm message |
| token | token to loop up for internationalization |
| pdsVal | PDS with the alarm values for internationalization (default:none) |
| szSub | the subsystem identifier eg. 1.2.3 (default: 1.1). |
| szSup | the suppression (supp_key) definition (default: none). |
| szSrc | the alarm source (default: localhost) |
| szCustom1 | a user defined field (default: none) |
| szCustom2 | a user defined field (default: none) |
| szCustom3 | a user defined field (default: none) |
| szCustom4 | a user defined field (default: none) |
| szCustom5 | a user defined field (default: none) |
