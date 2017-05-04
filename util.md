# Util API

### nimInit(flag)

### nimEnd(flag)

### nimEncryptString(string)

Encrypt string.

### nimDecryptString(string)

Decrypt encrypted string (with nimEncryptString).

### nimError2Txt(code)

Return return code as text 

```perl
my $rc = nimRequest(...);
print nimError2Txt($rc);
```

### nimLogin(login,password);

### nimLogout();

### nimChangeLogin(login,password);

### nimGetCurrentSid()

### nimSuppToStr(bHold,iNumber,iSeconds,szSuppKey)

### nimGetNameToIp(szName)

### nimGetIpToName(szIp,szPort);
