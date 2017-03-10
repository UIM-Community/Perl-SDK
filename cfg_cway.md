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

### cfgOpen(cfgLocation,readOnly) -> CFGHandle
##### Arguments type
| cfgLocation | readOnly |
| --- | --- |
| STRING | BOOLEAN |

Open the cfg file. First argument is the cfg location and the second one allow to only allow to read the cfg file.

```perl
my $CFGHandler = cfgOpen('test.cfg',0);
```

### cfgClose(CFGhandle) -> BOOLEAN

Close the cfg. Take as argument the cfg handle.

```perl
cfgClose($CFGHandler);
```

### cfgSync(CFGhandle) -> BOOLEAN

Write the cfg to the disk (but leave the file open). 

```perl
cfgSync($CFGHandler);
```

> Warning : It's **Sync** and not **Synch** 

### cfgKeyDelete(CFGhandle,section,key) -> BOOLEAN

##### Arguments type
| section | key |
| --- | --- |
| STRING | STRING |

Delete a key in a specific section.

```perl
cfgKeyDelete($CFGHandler,"/setup","logsize");
```

### cfgKeyList(CFGhandle,section) -> ARRAY

##### Arguments type
| section | 
| --- | 
| STRING |

Retrieving an array of keys from a section.

```perl
my ($ARR) = cfgKeyList($CFGHandler,"/setup");
foreach my $keyName ($ARR) {
     my $keyValue = cfgKeyRead($CFGHandler,"/setup",$keyName);
     print "$keyName => $keyValue \n";
}
```

### cfgKeyRead(CFGHandle,section,key) -> STRING

##### Arguments type
| section | key |
| --- | --- |
| STRING | STRING |

Read a key value from a section.

### cfgKeyWrite(CFGHandle,section,key,value) -> BOOLEAN

##### Arguments type
| section | key | value |
| --- | --- | --- | 
| STRING | STRING | STRING |

Write a new value for a section/key. 

```perl
cfgKeyWrite($CFGHandler,"/setup","loglevel","5");
```

### cfgListRead() -> BOOLEAN
### cfgListWrite() -> BOOLEAN

### cfgSectionCopy(CFGHandle,sectionFrom,sectionTo) -> BOOLEAN

##### Arguments type
| sectionFrom | sectionTo |
| --- | --- |
| STRING | STRING |

Copy section `from` to section `to` with a new name.

```perl
cfgSectionCopy($CFGHandler,"/setup","/setup_copy");
```
