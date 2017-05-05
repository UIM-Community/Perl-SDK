# Subscribing to Bus Messages

Any message published onto the Nimsoft Bus may be subscribed to by a program or script. The Nimbus::API provides the generic functions for subscribing to a message.  The simplest way is to use the Nimbus::Session module. This module implements a method called Nimbus::Session->subscribe.

```perl
use Nimbus::API;
use Nimbus::Session;
use strict;
 
# Callback whenever a message is ready for delivery, the udata
# and full messages are PDS containing the full (complete) message
# including headers, and the udata is the user-data area of the message.
sub hubpost {
    my ($hMsg,$udata,$full) = @_;
    nimLog (1,"(hubpost)");
    my $subject = pdsGet_PCH($full,"subject");
    print "The user-data posted under subject: $subject\n";
    pdsDump($udata);
    nimSendReply($hMsg);
}

# Other CALLBACK Declarations
sub your_function {
    my ($hMsg,$str_param,$int_param) = @_;
    print "your_function: I received a string=$str_param, and a number=$int_param\n";
    nimSendReply ($hMsg);
}

sub timeout {
# Do something useful
}

sub restart {
# Reload configuration, etc...
}

sub ctrlc {
    exit;
}

# Main entry
$SIG{INT} = \&ctrlc;
 
nimLogSet ("stdout","test",1,0);
nimLog (0,"Starting..");
 
my $sess = Nimbus::Session->new("perl-example-server");
$sess->setInfo ("1.0", "Owner information goes here");
 
if ($sess->subscribe ("MY_SUBJECT")) {
    nimLog(0,"unable to subscribe at Hub");
}
if ($sess->server (NIMPORT_ANY,\&timeout,\&restart)==0) {
    $sess->addCallback ("your_function", "string_param, integer_param%d" );
    $sess->dispatch ();
}
nimLog (0,"Exiting...");
```
