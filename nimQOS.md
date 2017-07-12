# The Quality of Service functions 

## API

### nimQoSCreate (szQoSName,szSource,samplerate,samplemax) -> QoSHandle
Creates and initializes a QoS object and returns a handle to this object.

### nimQoSCreateAsynch()

### nimQoSSendValue($hQoS, $szSource, $iValue)
Send a QoS value.

### nimQoSSendNull($Handle, $sztarget) ->int
Send a QoS message with a NULL sample. Used to indicate that the target was unavailable for monitoring. 

### nimQoSSendDefinition($szName, $szGroup, $szDesc, $szUnit, $szAbbr [,$iFlags])
New version of the deprecated nimQoSDefinition function; sends a QoS definition to the Nimsoft bus. This definition must be in place before sending QoS messages for the given named QoS. Should only be sent on startup to avoid excessive work for the data_engine probe.

### nimQoSSendValueStdev($hQoS,$szTarget,$fValue,$fStdev)

### nimQoSPostMessage($handle, $sztarget, $fsamplevalue, $fsample_stdev) -> int
Replaces the deprecated nimQoSMessage. Sends a raw QoS message.

### nimQoSStart($hQos)
Sets the start time in the given QoS object.

### nimQoSStop($hQos)
Sets the stop timer in the given QoS object and calculates the time used since nimQoSStart was run.

### nimQoSSendTimer($hQoS, $szSource)
Sends a QoS message with the time (in milliseconds). The time is the interval between when nimQoSStart was called and nimQoSStop was called. If nimQoSStop has not been called the time between when nimQoSStart was called and the current time is used.

### nimQoSSetSampletime()

### nimQoSGetTimer() -> iTimer
Return QoS timer.

### nimQoSGetHostname() -> szHost
Return QoS hostname.

### nimQoSGetSource()

### nimQoSSourceIsSet
