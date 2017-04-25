# Building and Publishing a User-defined Message

The Perl module Nimbus::PDS wraps the various PDS functions in the Nimsoft API function library.

**Example**
The example creates a PDS instance, adds some data to the PDS, then publishes the message onto the Nimsoft Bus with the subject "your_subject".

```perl
use Nimbus::PDS
##########################################################
# Post trend-data onto the Nimsoft Bus
#
my $pds = Nimbus::PDS->new();
my $dir	= "/tmp";
my $count = 33;
 
$pds->string("directory",$dir);
$pds->number("count",$count);
$pds->post("your_subject");
```
