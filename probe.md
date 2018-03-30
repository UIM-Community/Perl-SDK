# Probe

Register a new probe to Nimbus.

```perl
my $sess;

if($sess = nimSession(NULL, NIMPORT_ANY)) {
    my $port = nimsPort($sess);
    my $rc = nimRegisterProbe("probe_name",$port);
    if($rc == NIME_OK) {
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

## API

### nimRegisterProbe(szName, iPort) -> rc

This function will register the active session with nimbus name (probename/port) at the controller. You can get
the portnumber for the active session by acessing nims->iPort.

### nimUnRegisterProbe(szName) -> rc

This function will unregister probename at the controller

### nimSession(szHost, iPort) -> nims

Create a NimBUS session for client or server. This convenience function will create a server session on “port” if
the host parameter is set to NULL. If a hostname is passed on then a create client session is attempted.

### nimNamedSession(szAddr); 

Create a session connected to the given NimBUS address. nimSessionRequest is used to issue requests to the
probe when the connection is up.

### nimSessionFree(nims);

This function will free resources allocated to this session and free itself.

### nimSessionAlarm(nims, szMessage, iPri, szSuppKey, szSubSys, szSource, szNimID);

Send a NimBUS Alarm message on the session. This function behaves exactly like the nimAlarm function,
except that a session is required prior to sending the alarm.

### nimSessionFreeList(nimsList); 

Free sessList.

### nimSessionAddStdCallback(nims); 

Add session standard callback functions. This function will add the standard callback functions for status, list,
stop and restart. The NIMINFO struct also contains name, version and company information that are returned by
the _status command.

### nimSessionAddCallback(sess,cb_name); 

Add command callback function on session. This function will register a user-defined callback to the session (or
session list) for the command 'cmd' provided by the caller. The callback function prototype is determined by the
format 'fmt' parameter. The format string is defined by pdsScanf(3), and enables the programmer to specify the
parameter order and type to the callback function. A user specific 'cbdata' assocated with the callback may be
added by the nimSessionAddCbData.

### nimSessionAddCallbackPds(sess,cb_name,arg_format,security_level);

Add callback with arguments

```perl
sub get_info {
    my ($hMsg) = @_;
    nimSendReply($hMsg);
}

nimSessionAddCallbackPds($sess,"get_info","",0);
```

### nimSessionDispatch(nimsList, iMilliSec, iBreakTimeOut); 

The session dispatcher is the engine of the probe. When you have prepared the session by setting up command
callbacks (nimSessionAddCallback) and the standard callbacks (nimSessionAddStdCallback) most of the probe
logic will be handled by the dispatcher with the exception of what is done on timeouts.

### nimSessionGetLastError();

### nimSessionConnect();

### nimSessionIsConnected(nims) -> rc

Check if a session is connected.

### nimSessionController() -> nims

Create a session connected to the default controller. This convenience function will create a session to the default
controller.

### nimSessionSpooler() -> nims

Create a session connected to the default spooler. This convenience function will create a session to the default
spooler. Use this function when you expect to load many messages onto the spooler.

### nimSessionHub(szHubAddr) -> nims

Create a session connected to the hub. This convenience function will create a session to the named hub. If
'hubaddress' is NULL, then the NIMV_HUBADDR is used.

### nimSessionNewList();

### nimSessionAddList();

### nimSessionRemoveList();

### nimSessionRequest();

### nimSessionSend();

### nimSessionPostMessage();
