# Authentication API

These API are used to authenticate a Perl Script to NimBUS. There are not required when the script is runned as a deamon or as a timed probe by the product (and it could leak to some problems for a timed probe for example).

## API

### nimLogin(szLogin, szPassword) -> szLoginID

Login to NimBUS with user name and password. The login is global and will affect all subsequently calls to
NimBUS. You must free the SID when done with it.

```perl
my ($nimLoginID) = nimLogin('administrator', 'password');
if(not defined $nimLoginID) {
    print STDERR "Failed to authenticate the script to NimBUS\n";
}
```

### nimLogout() -> RC

Log off the current user. All global user credentials will be removed

### nimChangeLogin(szLogin, szPassword) -> RC

Can be used to switch between two or more different logins

### nimGetCurrentSid() -> Integer

Returns a pointer to the current SID in use by the NimBUS API. **Do not modify his value**
