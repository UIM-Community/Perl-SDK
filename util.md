# Util API

### nimInit(flag)

### nimEnd(flag)

#### nimEncryptString(string)

Encrypt string.

#### nimDecryptString(string)

Decrypt encrypted string (with nimEncryptString).

#### nimError2Txt(code)

Return return code as text 

```perl
my $rc = nimRequest(...);
print nimError2Txt($rc);
```

#### nimLogin(login,password);

#### nimLogout();

Logout the current login.

#### nimChangeLogin(login,password);

Change the current login for a another one.

#### nimGetCurrentSid()

Get the current process Sid.

#### nimSuppToStr(bHold,iNumber,iSeconds,szSuppKey)

Create suppression definition string.

```perl
my $szSup = nimSuppToStr(0,0,0,"FileSystem|$name");
$szSup = nimSuppToStr(1,0,60,"");
```

#### nimGetNameToIp(szName)

```perl
my($rc,$szIp,$iPort) =  nimGetNameToIp ($szName);
```

#### nimGetIpToName(szIp,szPort);

```perl
my($rc,$szName) =  nimGetIpToName ($szIp,$iPort);
```

## Get variables

| Constants | Type | Description |
| --- | --- | --- |
| NIMV_CONTIP | string | Controller IP |
| NIMV_CONTPORT | int | Controller Port |
| NIMV_SPOOLIP | string | Spooler IP |
| NIMV_SPOOLPORT | int | Spooler Port |
| NIMV_HUBIP | string | HUB IP |
| NIMV_HUBPORT | int | HUB Port | 
| NIMV_DEF_HUBPORT | int | N.A |
| NIMV_HUBADDR | string | Hub nimbus addresse | 
| NIMV_HUBDOMAIN | string | Hub domain |
| NIMV_DEF_CONTPORT | int | N.A |
| NIMV_DEF_SPOOLPORT | int | N.A |
| NIMV_ROBOTIP | string | Robot IP |
| NIMV_HUBNAME | string | Hub name |
| NIMV_PROBEID | int | Probe id | 

#### nimGetVarStr(symbol) 

```perl
my ($rc,$domain) = nimGetVarStr(NIMV_HUBDOMAIN);
if($rc == NIME_OK) {
    print "$domain\n";
}
```

#### nimGetVarInt(symbol)

```perl
my ($rc,$ip) = nimGetVarStr(NIMV_ROBOTIP);
if($rc == NIME_OK) {
    print "$ip\n";
}
```

#### nimSetVarInt(symbol) 

Set new int variable.

#### nimSetVarStr(symbol) 

Set new string variable.
