# Get hubs, robots informations

## Synopsis

In this example we want to retrieve the complete list of hubs and robots of the whole UIM infrastructure where the script will be connected.

## API used in this example

- [Nimrequest](https://github.com/UIM-Community/Perl-SDK/blob/master/request.md)
- [Nimbus PDS](https://github.com/UIM-Community/Perl-SDK/blob/master/pds.md)

## Example

```perl
use Nimbus::API;
use Nimbus::PDS;

# get hubslist from local hub
sub getHubs {
	my ($RC, $pdsRET) = nimNamedRequest("hub", "gethubs", Nimbus::PDS->new()->data);
    if ($RC != NIME_OK) {
        my $nimError = nimError2Txt($RC);
        die "Failed to execute `gethubs` on the current connected hub, Error ($RC): $nimError\n";
    }

	my @hubs = ();
	my $PPDS = Nimbus::PDS->new($pdsRET);
	for ( my $i = 0; my $HUBPDS = $PPDS->getTable("hublist", PDS_PDS, $i); $i++) {
		push(@hubs, $HUBPDS->asHash());
	}

	return \@hubs;
}

# Catch error with eval (same as a try/catch)
eval {
	my $hubArr = getHubs();
	my @robots = ();
	foreach my $hub (@{ $hubArr }) {
		my ($RC, $pdsRET) = nimNamedRequest("$hub->{addr}", "getrobots", Nimbus::PDS->new()->data);
		if ($RC != NIME_OK) {
			my $nimError = nimError2Txt($rc);
			print STDERR "Faild to execute `getrobots` on hub addr $hub->{addr}, Error ($RC): $nimError\n";
			next;
		}

		my $PPDS = Nimbus::PDS->new($pdsRET);
		for ( my $i = 0; my $ROBOTPDS = $PPDS->getTable("robotlist", PDS_PDS, $i); $i++) {
            push(@robots, $ROBOTPDS->asHash());
        }
	}

	my $totalRobotCount = scalar @robots;
	print STDOUT "Total robots count: $totalRobotCount\n";
    print Dumper(@robots)."\n";

	# Do what you want here
	# execute get_info to get more informations !
	# execute probelist on the robot ? etc...
};
print STDERR $@ if $@;
```
