# Util API

#### nimInit(flag)

Initialize the NimBUS API. On windows that includes the WinSock initializing. This should be the first
NimBUS call in any application.

#### nimEnd(flag)

Release all initialized NimBUS data. This should be the last NimBUS call in any application.

#### nimPostMessage()

Post a message with a given subject to NimBUS. This is the generic method that is the basis for both nimAlarm
and nimQoS messages.

#### nimSendReply(hMsg,rc,pds)

Reply to message! 

```perl
sub cb_execute {
    my ($hMsg) = @_;
    my $PDS = Nimbus::PDS->new(); 
    $PDS->put("status","ok",PDS_PCH);
    nimSendReply($hMsg,NIME_OK,$PDS);
}
```

#### nimEncryptString(string)

Will encrypt the input string using the Twofish algorithm and the encryption key. The function returns a base64
encoded and encrypted string. The result must be freed after use.

#### nimDecryptString(string)

The input string must be encrypted by nimEncryptString and the key must be the same. The result must be freed
after use.

#### nimError2Txt(code)

Return return code as text 

```perl
my $rc = nimRequest(...);
print nimError2Txt($rc);
```

#### nimLogin(login,password);

Login to NimBUS with user name and password. The login is global and will affect all subsequently calls to
NimBUS. You must free the SID when done with it.

#### nimLogout();

Log off the current user. All global user credentials will be removed

#### nimChangeLogin(login,password);

Can be used to switch between two or more different logins

#### nimGetCurrentSid()

Returns a pointer to the current SID in use by the NimBUS API. NB! Do not modify this value

#### nimSuppToStr(bHold,iNumber,iSeconds,szSuppKey)

Create suppression definition string.

```perl
my $szSup = nimSuppToStr(0,0,0,"FileSystem|$name");
$szSup = nimSuppToStr(1,0,60,"");
```
Set new string variable.
