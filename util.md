# Util API

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
