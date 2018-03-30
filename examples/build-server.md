# Building a Server Solution

You may, by simple means, make your Perl script behave as a "Network-aware application." It can be upgraded from just a monitoring probe, generating alarms in certain situations, to a full-blown server responding to requests over the network. The Nimbus::Session module is a class module wrapping many features from the C-like interfaces found in Nimbus::API. The session object decreases the number of API functions needed to a minimum.

Steps in creating your Perl server:

- Insert references to Nimbus::API and Nimbus::Session
- Construct a new session object using Nimbus::Session->new
- Initiate a server using Nimbus::Session->server
- Register callback functions using Nimbus::Session->addCallback
- Invoke the message dispatcher using Nimbus::Session->dispatch.

## API Used on this example

- [Nimbus Session](https://github.com/UIM-Community/Perl-SDK/blob/master/server.md)

## Example 

```perl
use Nimbus::API;
use Nimbus::Session;

# CALLBACK Declarations
sub your_function {
    my ($hMsg, $str_param, $int_param) = @_;

    print "your_function: I received a string=$str_param, and a number=$int_param\n";
    nimSendReply ($hMsg);
}

sub timeout {
    # Do something, normally you would put your monitoring code
    # here, checking the elapsed time.
}

sub restart {
    # Reload configuration, etc...
}

# MAIN ENTRY
my $sess = Nimbus::Session->new("perl-example-server");
$sess->setInfo ("1.0", "Owner information goes here");
 
if ($sess->server (NIMPORT_ANY,\&timeout,\&restart)==0) {
    $sess->addCallback ("your_function", "string_param, integer_param%d" );
    $sess->dispatch();
}
```

Note you can configure the timeout callback time (milliseconds) in the dispatch method.

```perl
$sess->dispatch(1000);
```
