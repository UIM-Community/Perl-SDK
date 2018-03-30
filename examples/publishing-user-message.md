
# Building and Publishing a User-defined Message

## API Used on this example

- [Nimbus::PDS](https://github.com/UIM-Community/Perl-SDK/blob/master/pds.md)
- [NimPostMessage from utils](https://github.com/UIM-Community/Perl-SDK/blob/master/util.md#nimpostmessageszsubjectudatailevelszsup)

## Example
The Perl module Nimbus::PDS wraps the various PDS functions in the Nimsoft API function library.

The code example creates a PDS instance, adds some data to the PDS, then publishes the message onto the Nimsoft Bus with the subject "your_subject".

```perl
use Nimbus::PDS

# Post trend-data onto the Nimsoft Bus
my $pds = Nimbus::PDS->new();
$pds->string("directory", "/tmp");
$pds->number("count", 33);
$pds->post("your_subject");
```

The PDS Class use the nimPostMessage method (you can find the API in utils section). So you can write the post by the following code as well : 

```perl
nimPostMessage("your_subject", $pds->data);
```
