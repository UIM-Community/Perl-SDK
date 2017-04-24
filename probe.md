# Probe

Register a new probe to Nimbus.

```perl
my $sess;

if($sess = nimSession(NULL, NIMPORT_ANY)) {
    my $port = nimsPort($sess);
    my $id = substr($0,rindex($0,"/")+1);
    $id = "$id (Nimbus::Session)";
    my $rc = nimRegisterProbe($id,$port);
    if($rc == 0) {
        # Ok... Add callback 
    }
    else {
        nimSessionFree($sess);
    }
}
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
