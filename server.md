# Server session (Nimbus API)

The Session object is a class wrapper around the Nimbus::API module, and raises the abstraction layer from the low-level Nimsoft API. Reference the Session.pm module for the functions included.

You can create a server (TCP/IP), that accepts commands over the ports registered by the $nim->*server* method. The command is dispatched by the command dispatcher to the function with the same name as the command. A command without a matching function causes an abort situation.

Another feature of this class is the ability to connect to a Nimsoft hub. The functions $nim->*attach* and $nim->*subscribe* both connect to the hub and receive postings over the hubpost function.

## API

#### new(szId, szName?) -> szSessionId

The new method takes a **string** session ID as a required parameter, and session name as an optional parameter.

| Argument name | Description |
| --- | --- |
| szId | session ID |
| szName | optional session name |

```perl
my $sess = Nimbus::Session->new("id-server");
```

#### addCallback(szCallbackName, szCallbackArguments, iSecurityLevel) -> rc

Adds a callback to the server session. This allows functions to be triggered from other probes or utilities.

| Argument name | Description |
| --- | --- |
| szCallbackName | Name of the function to be called when callback is triggered. |
| szCallbackArguments | 	Parameters to the function and their data types. |
| iSecurityLevel | 	0=open, 1=read, 2=write, 3=admin |

```perl
function test {
     my ($hMsg) = @_; 
     print 'test callback triggered \n';
     nimSendReply($hMsg, NIME_OK);
}
$sess->addCallback("test");
```

Perl SDK session callbacks support `string` and `integer`. Integer are declared with **%d** symbol. For example to declare two arguments let take the following example:
```
string_param, integer_param%d
```

It will produce the following code:

```perl
function test {
     my ($hMsg, $str_param, $integer_param) = @_; 
     print 'test callback triggered, $str_param, $integer_param \n';
     nimSendReply($hMsg);
}
$sess->addCallback("test", "string_param, integer_param%d");
```

Default values are `NULL` for String type and `0` for integer.

#### attach(szQueue, szHubIp, iHubPort?) -> rc

The attach method causes the session to attach to a queue defined on the hub. As opposed to the subscribe method, messages are queued when the process is detached (for example, not running, or running but detached).

#### detach(iId)

The detach method disconnects the subscribe channel that is referenced by the $id parameter. The first channel is used if no parameter is supplied.

#### subscribe(szSubject, szHubIp, iHubPort?) -> rc

The subscribe method causes the session to set up a subscribe channel at the hub. This type of channel is not secure in the sense of deliverability. Messages are only directed down the channel when the session is listening.

#### dispatch(iTimeoutMs, iBreakOnEvent) -> sessRC

This function loops while waiting for messages from the Hub. A timeout function is run if it has been set. Reconnects to the Hub in the event this connection drops.

```perl
$sess->dispatch(15000); # 15 seconds timeout!
``` 

Return a Session error code (NIMSW_TIMEOUT, NIMSW_ERROR, NIMSW_RESTART or NIMSW_EXIT) or -1 on a fatal error.

#### server(iPort, fTimeOut, fRestart) -> rc

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

#### setPostCallback(szCallbackName) -> rc

Sets the function to run when a message is received from the Hub. Default function is hubpost, but this allows you to specify another function name.

```perl
sub hubpost_custom {

}

$sess->setPostCallback('hubpost_custom');
```

This can be very useful if you want to build multiple functions to handle hubpost request based on different conditions.

#### setRetryInterval(iIntervalSecond) -> rc

Sets how often to attempt a reconnect if connection to the Hub drops.
