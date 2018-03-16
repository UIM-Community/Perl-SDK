# Sending QoS Data

The probe should only initialize itself during startup by sending the definition. However, it must report the collected data every time it runs. This instructs the data_engine to insert the collected sample value into the database. 
The following code packs the QoS message into a function:

> Dont forgot to send a new QoS Definitions for **QOS_TEST**

```perl
my $samplevalue = 100;
my $source = nimGetVarStr(NIMV_ROBOTNAME);
my $target = "startup-time";
my $interval = 300;	# Seconds
if (my $qos = nimQoSCreate("QOS_TEST",$source,$interval,-1)) {
    if ($samplevalue < 0) {
        nimQoSSendNull ($qos,$target);
    }
    else {
        nimQoSSendValue($qos,$target,$samplevalue);
    }
    nimQoSFree($qos);
}
```

The following code illustrates how you may wrap your data collection code with stopwatch functionality. This is useful when doing response time measurements:

```perl
my $source = nimGetVarStr(NIMV_ROBOTNAME);
my $target = "startup-time";
my $interval = 300;	# Seconds
if (my $qos = nimQoSCreate("QOS_TEST",$source,$interval,-1)) {
    nimQoSStart($qos);
 
    # Do your work here...
 
    nimQoSStop($qos);
    nimQoSSendTimer($qos,$target);
    nimQoSFree($qos);
}
```
