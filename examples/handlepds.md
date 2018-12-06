# How to handle and parse nimRequest and nimNamedRequest PDS.

When your request return a success code you have to handle the returned object (a PDS). Sometimes it's a little bit hard to understand what we have
to do exactly with this when we start this Perl SDK or with Nimsoft.

Go througth differents examples : 

## API Used on this example

- [NimRequest](https://github.com/UIM-Community/Perl-SDK/blob/master/request.md)
- [Nimbus PDS](https://github.com/UIM-Community/Perl-SDK/blob/master/pds.md)

## Get the PDS and transform it to hash

```perl
my $PDS = Nimbus::PDS->new;
my ($RC, $Response) = nimNamedRequest("controller", "get_info", $PDS->data);

if($RC == NIME_OK) {
    my $PDS = Nimbus::PDS->new($Response);
    my $HashRef = $PDS->asHash();
    print "$PDS->get('robotname')\n";
    print "$HashRef->{robotname}\n";
}
```

> Note : asHash() method return a hash reference. So you have to write `->` to access data.

You can continue to work directly with PDS or transform your PDS Object to an Hash.

## When you have to handle a table in a PDS

```perl
my $PDS = Nimbus::PDS->new;
my ($RC, $Response) = nimNamedRequest("hub", "getrobots", $PDS->data);

if($RC == NIME_OK) {
    my $PPDS = Nimbus::PDS->new($Response);
    for( my $count = 0; my $RobotPDS = $PPDS->getTable("robotlist", PDS_PDS, $count); $count++) {
        my $robot_name = $RobotPDS->get("name");
        # or $robotHashRef = $RobotPDS->asHash(); 
        # $robotHashRef->{name};
    }
}
```
