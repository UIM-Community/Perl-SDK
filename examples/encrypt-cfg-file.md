# Encrypt a field of a Nimsoft CFG File !

## Synopsis
You have a probe where you want to encrypt one or many "password" fields to not leave them visible for UIM Administrators. For this example we want to retrieve our database password (decrypted if he is crypted and if not... encrypt it).

## API Used on this example

- To open and read keys: [Nimbus CFG](https://github.com/UIM-Community/Perl-SDK/blob/master/cfg_nimbus.md)
- To write the cfg on the disk: [CFG C API](https://github.com/UIM-Community/Perl-SDK/blob/master/cfg_cway.md)

> For this example we use both API. But everything can be done by only using the C Binding CFG API ! 

## Configuration

myprobe.cfg
```xml
<setup>
    loglevel = 5
</setup>
<database>
   database = ca_uim
   host = 127.0.0.1
   port = 33006
   user = sa
   password = myPassword
</database>
```

## Code

```perl
use Nimbus::API;
use Nimbus::CFG;

# Your credential key
my $CRED_KEY = "CRED_KEY";

# Open CFG
my $CFG = Nimbus::CFG->new("myprobe.cfg");

# Get the CFG field /database/password
my $DB_Password = $CFG->{database}->{password}

# Crypt CFG Credential keys!
if(substr($DB_Password, length($DB_Password) - 2, 2) ne "==") {
  my $CFGNapi = cfgOpen("myprobe.cfg", 0);
  # Encrypt the password
  my $cValue = nimEncryptString($CRED_KEY, $DB_Password);
  # Write it on the CFG memory handler
  cfgKeyWrite($CFGNapi, "/database/", "password", $cValue); 
  # Write it to the disk
  cfgSync($CFGNapi);
  cfgClose($CFGNapi);
}
else {
  # Password is crypted... Translate it with the key
  $DB_Password = nimDecryptString($CRED_KEY, $DB_Password);
}

```
