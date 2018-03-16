# Sending an Alarm Message (advanced)

The classical way to send an alarm is not enougth when you need to set fields like 'origin', 'usertag2' or anything else like met_id,dev_id etc..
So in this case we have to post a new alarm to the spooler probe by our self.

Let code a sample function to generate our alarm PDS :

```perl
sub rndStr { 
    return join'', @_[ map{ rand @_ } 1 .. shift ] 
}

sub nimId {
    my $A = rndStr(10,'A'..'Z',0..9);
    my $B = rndStr(5,0..9);
    return "$A-$B";
}

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
# Require Nimbus lib
# Require required Nimbus API

my ($PDS,$nimId) = generateAlarm('alarm',{
    severity => NIML_CRITICAL,
    message => "hello world",
    origin => "yahou",
    usertag2 => "test",
    domain => "domain"
});

my ($RC,$Response) = nimRequest("robotname",48001,"post_raw",$PDS);
if($RC == NIME_OK) {
    print "Alarm with id => $nimId successfully created\n";
}
else {
    print "Failed to create alarm id => $nimID, rc => $RC\n";
}
```
