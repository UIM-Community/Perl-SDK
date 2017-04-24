# Probe

Register a new probe to Nimbus.

```perl
my $sess;

if($sess = nimSession(NULL, NIMPORT_ANY)) {
    my $port = nimsPort($sess);
    my $rc = nimRegisterProbe("probe_name",$port);
    if($rc == 0) {
        # Ok... Add callback 
    }
    else {
        nimSessionFree($sess);
    }
}
```

And if you want to unregister probe 

```perl
unRegisterProbe("probe_name");
```

# Sessions 

## API

### nimSession(any,port);

### nimNamedSession(); 

### nimSessionFree(session); 

### nimSessionRequest(); 

### nimSessionSend(); 

### nimSessionPostMessage(); 

### nimSessionAlarm(); 

### nimSessionNewList(); 

### nimSessionAddList(); 

### nimSessionRemoveList(); 

### nimSessionFreeList(); 

### nimSessionAddStdCallback(); 

### nimSessionAddCallback(); 

### nimSessionAddCallbackPds(); 

### nimSessionDispatch(timeout); 

### nimSessionGetLastError(); 

### nimSessionConnect(); 

### nimSessionIsConnected(); 

### nimSessionController(); 

### nimSessionSpooler(); 

### nimSessionHub(); 
