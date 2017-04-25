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

Create a new session.

### nimNamedSession(); 

Create a new named session.

### nimSessionFree(session); 

### nimSessionRequest(); 

### nimSessionSend(); 

### nimSessionPostMessage(); 

### nimSessionAlarm(); 

### nimSessionNewList(); 

### nimSessionAddList(); 

### nimSessionRemoveList(); 

### nimSessionFreeList(sessList); 

Free sessList.

### nimSessionAddStdCallback(sess); 

Add a standart callback (like timeout,restart etc..).

### nimSessionAddCallback(sess,cb_name); 

Add command callback function on session. This function will register a user-defined callback to the session (or
session list) for the command 'cb_name' provided by the caller. 

### nimSessionAddCallbackPds(sess,cb_name,arg_format,security_level);

Add callback with arguments

```perl
sub get_info {
    my ($hMsg) = @_;
    nimSendReply($hMsg);
}

nimSessionAddCallbackPds($sess,"get_info","",0);
```

### nimSessionDispatch(timeout); 

### nimSessionGetLastError(); 

### nimSessionConnect(); 

### nimSessionIsConnected(); 

### nimSessionController(); 

### nimSessionSpooler(); 

### nimSessionHub(); 
