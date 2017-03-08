# CFG ( C Way )

If you want to make a lot of actions (like updating sections, creating new section and save the .cfg ) the classical Nimbus API is not enougth (It's just here to help people to read cfg files easily). 

## Examples (creating cfg)

```perl
sub createSection {
    my ($CFG,$SECTION) = @_;
    cfgKeyWrite($CFG,$SECTION,"key","value");
    cfgKeyDelete($CFG,$SECTION,"key");
}

my $CFG = cfgOpen("test.cfg");
createSection($CFG,"/setup");
cfgKeyWrite($CFG,"/setup/","loglevel","5"); 
cfgSync($CFG);
cfgClose($CFG);
```

## API 

### cfgOpen(filePath,readOnly)
