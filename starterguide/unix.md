# Starter Guide - UNIX

## 1. Download SDK_Perl  

Download SDK_Perl package from [Nimsoft Archive](https://support.nimsoft.com/Default.aspx?center=felles/loginSmall&tourl=felles/archive&name=archive)

Depending on your UNIX system download the right perl packages too.

And put these .zip files onto your archive (with Infrastructure Manager or Admin Console).

## 2. Install perl packages on the Nimsoft Hub

Install the Perl SDK package and the right Perl UNIX package on the Nimsoft Hub.

After installation, verify the nimsoft directory on the system. You should have two directories:
- perllib
- perl

Depending on the system it can be Perl64 and not Perl.

## 3. Create your first script ! 

Now create your first .pl script with a content like the following example : 

```perl
#replace this
use lib "/opt/nimsoft/perllib";
use lib "/opt/nimsoft/perl/lib";

# Set env variable NIM_ROOT
$ENV{'NIM_ROOT'} = '/opt/nimsoft';

# Use perl-core package(s)
use strict;
use warnings;
use Data::Dumper;

# use Nimbus package(s) (from lib at the top of the script)
use Nimbus::API;
use Nimbus::PDS;

# Authenticate your script to NimBus
nimLogin("administrator","password"); # Put your UIM Login/Password 

# Get the robotname from the (local) NimBus
my $robotname = nimGetVarStr(NIMV_ROBOTNAME);

# Make a request to the local agent
# Second argument is the port of the probe (48002 is equal to controller probe)
# Third argument is the callback we want to achieve on the probe
my ($RC, $PDS) = nimRequest($robotname, 48002, "get_info");
if($RC == NIME_OK) {
    # Transform the PDS response into a readable Perl HASH (ref)
    my $robotInfo = Nimbus::PDS->new($PDS)->asHash();
    # print Dumper($robotInfo)."\n";
    print "$robotInfo->{origin}\n";
    print "$robotInfo->{robot_device_id}\n";
}
else {
    print nimError2Txt($RC)."\n";
}
```

Find more examples [here](https://github.com/UIM-Community/Perl-SDK/tree/master/examples).
