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
use strict;
use warnings;
use lib "E:/Nimsoft/perllib"; #replace this

nimLogin("administrator","password") # Put your UIM Login/Password 

my $robotname = nimGetVarStr(NIMV_ROBOTNAME);
my ($RC,$PDS) = nimRequest($robotname,48002,"get_info");
if($RC == NIME_OK) {
    my $Info = Nimbus::PDS->new($PDS)->asHash();
    print "$Info->{origin}\n";
    print "$Info->{robot_device_id}\n";
}
```

This little script retrieve information from hub probe (on the robot where the script is executed) by executing get_info callback.
