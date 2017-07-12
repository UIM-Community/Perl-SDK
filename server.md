# Server session (Nimbus API)

The Session object is a class wrapper around the Nimbus::API module, and raises the abstraction layer from the low-level Nimsoft API. Reference the Session.pm module for the functions included.

You can create a server (TCP/IP), that accepts commands over the ports registered by the $nim->*server* method. The command is dispatched by the command dispatcher to the function with the same name as the command. A command without a matching function causes an abort situation.

Another feature of this class is the ability to connect to a Nimsoft hub. The functions $nim->*attach* and $nim->*subscribe* both connect to the hub and receive postings over the hubpost function.

## API

#### new(id,sessions)

The new method takes a **string** session ID as a required parameter, and session name as an optional parameter.

```perl
my $optional_sessions = nimSessionNewList();
my $sess = Nimbus::Session->new("id-server",$optional_sessions);
```

#### addCallback(cb,format,level)

Adds a callback to the server session. This allows functions to be triggered from other probes or utilities.
```perl
function test {
     my ($hMsg) = @_; 
     print 'test callback triggered \n';
     nimSendReply($hMsg,NIME_OK);
}
$sess->addCallback("test");
```

The perl support `string` and `integer`. Integer are declared with **%d** symbol.

```
string_param, integer_param%d
```

#### attach(queue,hubip,hubport)

The attach method causes the session to attach to a queue defined on the hub. As opposed to the subscribe method, messages are queued when the process is detached (for example, not running, or running but detached).

#### subscribe(subjects,hubip,hubport)

The subscribe method causes the session to set up a subscribe channel at the hub. This type of channel is not secure in the sense of deliverability. Messages are only directed down the channel when the session is listening.

#### detach(id)

The detach method disconnects the subscribe channel that is referenced by the $id parameter. The first channel is used if no parameter is supplied.

#### dispatch(timeout_ms,breakOnEvent)

This function loops while waiting for messages from the Hub. A timeout function is run if it has been set. Reconnects to the Hub in the event this connection drops.

```perl
$sess->dispatch(15000); # 15 seconds timeout!
``` 

#### server(port,timeoutCB,restartCB)

Starts a server session, which waits for incoming messages on the Nimsoft Bus. Callbacks which have been registered are published on the bus, making the interface available.

```perl
sub timeout {
     print 'timeout, defined in dispatch or 5 seconds by default\n';
}

sub restart {
     print 'restart\n';
}

if ($sess->server (NIMPORT_ANY,\&timeout,\&restart) == NIME_OK) {
    $sess->dispatch();
}
``` 

#### setInfo(version,company)

Fills in the information about the probe which is gathered when the _status callback is run.

```perl
$sess->setInfo("v1.0","CA Services");
```

#### setPostCallback(cbName)

Sets the function to run when a message is received from the Hub. Default function is hubpost, but this allows you to specify another function name.

```perl
sub hubpost_custom {

}

$sess->setPostCallback('hubpost_custom');
```

This can be very useful if you want to build multiple functions to handle hubpost request based on different conditions.

#### setRetryInterval(interval_seconds)

Sets how often to attempt a reconnect if connection to the Hub drops.
