# Sending an Alarm Message (advanced)

## Synopsis 

Nimsoft Perl API for sending alarms are not useful enought when you have to send an alarm with fields like `origin` or `usertag2`. On this scenera we have to build our owns methods and send a final PDS to the spooler probe with the callback `post_raw`.

## API used in this example

- [Nimbus PDS](https://github.com/UIM-Community/Perl-SDK/blob/master/pds.md)

## Example

```perl

#
# DESC: Generate a random string between multiple length integers
#
sub rndStr { 
    return join'', @_[ map{ rand @_ } 1 .. shift ] 
}

#
# DESC: Generate a valid random nimid
#
sub nimId {
    my $A = rndStr(10,'A'..'Z',0..9);
    my $B = rndStr(5,0..9);
    return "$A-$B";
}

#
# DESC: Generate alarm PDS
#
sub generateAlarm {
    my ($subject,$hashRef) = @_;

    my $PDS = Nimbus::PDS->new(); 
    my $nimid = nimId();

    $PDS->string("nimid",$nimid);
    $PDS->number("nimts",time());
    $PDS->number("tz_offset",0);
    $PDS->string("subject","$subject");
    $PDS->string("md5sum","");
    $PDS->string("user_tag_1",$hashRef->{usertag1} || "");
    $PDS->string("user_tag_2",$hashRef->{usertag2} || "");
    $PDS->string("source",$hashRef->{source} || $hashRef->{robot} || "");
    $PDS->string("robot",$hashRef->{robot} || "");
    $PDS->string("prid",$hashRef->{probe} || "");
    $PDS->number("pri",$hashRef->{severity} || 0);
    $PDS->string("dev_id",$hashRef->{dev_id} || "");
    $PDS->string("met_id",$hashRef->{met_id} || "");
    if ($hashRef->{supp_key}) { $PDS->string("supp_key",$hashRef->{supp_key}) };
    $PDS->string("suppression",$hashRef->{suppression} || "");
    $PDS->string("origin",$hashRef->{origin} || "");
    $PDS->string("domain",$hashRef->{domain} || "");

    my $AlarmPDS = Nimbus::PDS->new(); 
    $AlarmPDS->number("level",$hashRef->{severity} || 0);
    $AlarmPDS->string("message",$hashRef->{message});
    $AlarmPDS->string("subsys",$hashRef->{subsystem} || "1.1.");
    if(defined $hashRef->{token}) {
        $AlarmPDS->string("token",$hashRef->{token});
    }

    $PDS->put("udata",$AlarmPDS,PDS_PDS);

    return ($PDS,$nimid);
}    
```

In this code we have three functions. ( `rndStr`, `nimId` and `generateAlarm` ). 
The **two firsts are for here for generating a unique nimId** for our alarm (customize if needed).

And generateAlarm is here to return the complete PDS for our alarm. After that we have just to send this PDS to our callback ! 

```perl
use Nimbus::API;
use Nimbus::PDS;

my ($PDS, $nimId) = generateAlarm('alarm',{
    severity => NIML_CRITICAL,
    message => "hello world",
    origin => "yahou",
    usertag2 => "test",
    domain => "domain"
});

my ($RC, $Response) = nimRequest("robotname", 48001, "post_raw", $PDS->data);
if($RC == NIME_OK) {
    print "Alarm with id => $nimId successfully created\n";
}
else {
    my $nimError = nimError2Txt($RC);
    print "Failed to trigger new alarm with id => $nimID, Error ($RC): $nimError\n";
}
```
