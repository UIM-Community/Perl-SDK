# Util API

### nimInit(iFlag)

Initialize the NimBUS API. On windows that includes the WinSock initializing. This should be the first
NimBUS call in any application.

### nimEnd(iFlag)

Release all initialized NimBUS data. This should be the last NimBUS call in any application.

> nimInit and nimEnd are automatically triggered by Perl SDK.

### nimPostMessage(szSubject,uData,iLevel,szSup)

Post a message with a given subject to NimBUS. This is the generic method that is the basis for both nimAlarm
and nimQoS messages.

- szSubject is the post channel.
- udata     is a PDS record with user-data.
- iLevel    is the post priority (see Level constants).
- szSup     is the suppression definition.

```perl
my $PDS = Nimbus::PDS->new;
$PDS->put('level',5,PDS_INT);
$PDS->put('message','hello world!',PDS_PCH);
nimPostMessage('alarm2',$PDS->{pds});
```

> **Warning** This method only allow to post the field "**udata**".

### nimSendReply(hMsg,rc,pds)

Reply to message! 

```perl
sub cb_execute {
    my ($hMsg) = @_;
    my $PDS = Nimbus::PDS->new(); 
    $PDS->put("status","ok",PDS_PCH);
    nimSendReply($hMsg,NIME_OK,$PDS);
}
```

### gettimeofday()

Returns the time in seconds and in micro-seconds if in a scalar context, or it returns an array with 2 values (seconds, useconds).

```perl
my @start = gettimeofday();
# do stuff...
my @end   = gettimeofday();
my $diff  = tv_interval(@start,@end);
```

### nimEncryptString(szKey, szString) -> String

Will encrypt the input string using the Twofish algorithm and the encryption key. The function returns a base64
encoded and encrypted string. The result must be freed after use.

### nimDecryptString(szKey, szCrypted) -> String

The input string must be encrypted by nimEncryptString and the key must be the same. The result must be freed
after use.

### nimError2Txt(NIM_CODE) -> String

Translate the integer return code value into a human readable message!

```perl
my $rc = nimRequest(...);
print nimError2Txt($rc);
```

### nimLogin(szLogin,szPassword); -> nimLogin

Login to NimBUS with user name and password. The login is global and will affect all subsequently calls to
NimBUS. You must free the SID when done with it.

```perl
my ($nimLogin) = nimLogin('administrator','password');
```

### nimLogout(); -> RC

Log off the current user. All global user credentials will be removed

### nimChangeLogin(szLogin,szPassword); -> RC

Can be used to switch between two or more different logins

### nimGetCurrentSid() -> Integer

Returns a pointer to the current SID in use by the NimBUS API. **Do not modify this value**

### nimSuppToStr(bHold,iNumber,iSeconds,szSuppKey) -> String

Create suppression definition string.

```perl
my $szSup = nimSuppToStr(0,0,0,"FileSystem|$name");
$szSup = nimSuppToStr(1,0,60,"");
```
Set new string variable.
