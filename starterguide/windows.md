# Windows - Starter guide

## 1. Download SDK_Perl 

Download SDK_Perl package from [Nimsoft Archive](https://support.nimsoft.com/Default.aspx?center=felles/loginSmall&tourl=felles/archive&name=archive)

And put the .zip file onto your archive (with Infrastructure Manager or Admin Console).

<p align="center"><img src="http://i.imgur.com/LkAaMHg.png"></p>

## 2. Install SDK_Perl on your hubs.

Install the package SDK_Perl where you want ( on a hub ).

After installation, check locally on the system if the directory **Nimsoft/perllib** has been created successfully.

<p align="center"><img src="http://i.imgur.com/k73jbIN.png"></p>

## 3. Install Perl 5.14

Install Perl 5.14 (5.14.2 or 5.14.3) on the system. You can find all Strawberry release [here](http://strawberryperl.com/releases.html) 

<p align="center"><img src="http://i.imgur.com/KHsQ3zw.png"></p>

## 3. Create your first script ! 

Now create your first .pl script with a content like the following example : 

> **Replace the lib path with your Nimsoft perllib directory**

```perl
#replace this
use lib "E:/Nimsoft/perllib";

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
