# The Quality of Service functions 

## API

### nimQoSCreate (szQoSName, szTarget, iSampleRate, iSampleMax) -> QoSHandle
Creates and initializes a QoS object and returns a handle to this object.

| Type | Argument name | Description |
| --- | --- | --- | 
| String | szQoSName | The name of the QoS. |
| String | szTarget | The QoS target. |
| Integer | iSampleRate | The rate of the sample interval. |
| Integer | iSampleMax | the maximum value (if any). For example: disksize.

```perl
# Use sampleMax -1 to specifiy "no limit"
my ($QoS) = nimQoSCreate("QOS_NAME", "targetDeviceName", 30, -1);
```

> **Warnings** Think to send a QoSDefinition before creating any QoS

### nimQoSFree(QoSHandle)
Release the resources that are allocated in the handle.

```perl
nimQoSFree($QoS);
```

### nimQoSSendValue($hQoS, $sztarget, $iValue) -> rc
Send a QoS value.

### nimQoSSendValueStdev($hQoS, $szTarget, $fValue, $fStdev) -> rc

### nimQoSSendNull($Handle, $sztarget) -> rc
Send a QoS message with a NULL sample. Used to indicate that the target was unavailable for monitoring. 

### nimQoSSendDefinition($szName, $szGroup, $szDesc, $szUnit, $szAbbr [,$iFlags]) -> rc
New version of the deprecated nimQoSDefinition function; sends a QoS definition to the Nimsoft bus. This definition must be in place before sending QoS messages for the given named QoS. Should only be sent on startup to avoid excessive work for the data_engine probe.

A normal definition example: 
```perl
nimQoSSendDefinition(
  'QOS_TEST',
  'QOS_GROUP',
  'QoS Description',
  's',
  'Seconds',
  NIMQOS_DEF_NONE
);
```

A boolean definition:
```perl
nimQoSSendDefinition(
  'QOS_BOOL',
  'QOS_GROUP',
  'QoS Description',
  'State',
  '',
  NIMQOS_DEF_BOOLEAN
);
```

Some valid units (there is many in the database) : 

| Unit name | abbreviation |
| --- | --- | 
| Bytes | B |
| us | us |
| State | N.A |
| Mega Bytes | MB |
| Giga Bytes | GB |
| Seconds | s |
| Milliseconds | ms |
| Bytes/Second | B/s |
| Kilobytes/Second | KB/s |
| Megabytes/Second | MB/s |
| Percent | % |

### nimQoSPostMessage($handle, $sztarget, $fsamplevalue, $fsample_stdev) -> rc
Replaces the deprecated nimQoSMessage. Sends a raw QoS message.

### nimQoSStart($hQos)
Sets the start time in the given QoS object.

### nimQoSStop($hQos)
Sets the stop timer in the given QoS object and calculates the time used since nimQoSStart was run.

### nimQoSSendTimer($hQoS, $szSource)
Sends a QoS message with the time (in milliseconds). The time is the interval between when nimQoSStart was called and nimQoSStop was called. If nimQoSStop has not been called the time between when nimQoSStart was called and the current time is used.

### nimQoSSetSampletime()
Set a new (timestamp) sample time to the QoS.

### nimQoSGetTimer() -> iTimer
Return QoS timer.

### nimQoSGetHostname() -> szHost
Return QoS hostname.

### nimQoSGetSource()

### nimQoSCreateAsynch()

### nimQoSSourceIsSet
