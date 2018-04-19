# Transform an hash Ref to a PDS Object

## Synopsis
In many situations he can be useful to transform the PDS into a Perl hash (with asHash() method) to make a set of actions. But after that maybe we want to re-publish the message in the NimBus queue.

So we will see how to retransform our HashRef Object into a valid PDS for the Nimsoft API ! 

## API Used on this example

- [Nimbus PDS](https://github.com/UIM-Community/Perl-SDK/blob/master/pds.md)

## Example

```perl
use Nimbus::API;
use Nimbus::PDS;
use Scalar::Util qw(looks_like_number); # Dont forget to implement looks_like_number routine

# Copy this routine on your code
sub pdsFromArray {
    my ($arrayRef) = @_;
    return if ref($arrayRef) ne "ARRAY";

    my $PDS = Nimbus::PDS->new;
    my $index = 0;
    foreach(@{ $arrayRef }) {
        if (ref($_) eq "HASH") {
            $PDS->put($index, pdsFromHash($_), PDS_PDS);
        }
        elsif (ref($_) eq "ARRAY") {
            $PDS->put($index, pdsFromArray($_), PDS_PDS);
        }
        else {
            $PDS->put($index, $_, looks_like_number($_) ? PDS_INT : PDS_PCH);
        }
        $index++;
    }
    return $PDS;
}

sub pdsFromHash {
    my ($hashRef) = @_;
    my $PDS = Nimbus::PDS->new;
    for my $key (keys %{ $hashRef }) {
        my $val = $hashRef->{$key};
        if (ref($val) eq "HASH") {
            $PDS->put($key, pdsFromHash($val), PDS_PDS);
        }
        elsif (ref($val) eq "ARRAY") {
            $PDS->put($key, pdsFromArray($val), PDS_PDS);
        }
        else {
            $PDS->put($key, $val, looks_like_number($val) ? PDS_INT : PDS_PCH);
        }
    }
    return $PDS;
}

my $PDS = pdsFromHash({
    message => "hello world"
});
$PDS->dump();

# Do the action you want here...
# nimSendReply($hMsg, NIME_OK, $PDS);
```

This version doesn't support float and native PDS Array types because of some SDK Perl limitation (some methods and PDS Types are missing).
