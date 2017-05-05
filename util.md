# Util API

#### nimInit(flag)

#### nimEnd(flag)

#### nimPostMessage()

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
Set new string variable.
