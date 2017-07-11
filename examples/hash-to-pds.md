# Transform an hash Ref to a PDS Object

In many situations he can be useful to transform the PDS into a Perl hash to make a set of actions. But after that maybe we want to re-publish 
our PDS somewhere (on a callback response or in a queue).

So we have to retransform our Hash Object to a PDS.

```perl
use Scalar::Util qw(looks_like_number); # Dont forget to implement looks_like_number routine

sub pdsFromHash {
    my ($hashRef) = @_;
    my $PDS = Nimbus::PDS->new;
    for my $key (keys %{ $hashRef }) {
        my $val = $hashRef->{$key};
        if(ref($val) eq "HASH") {
            $PDS->put($key,pdsFromHash($val),PDS_PDS);
        }
        else {
            $PDS->put($key,$val,looks_like_number($val) ? PDS_INT : PDS_PCH);
        }
    }
    return $PDS;
}

my $PDS = pdsFromHash({
    message => "hello world"
});

nimSendReply($hMsg,NIME_OK,$PDS);
```

This version dont support "float" Type. However now you can transform your hash into a PDS easily.
