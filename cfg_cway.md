# CFG ( C Way )

If you want to make a lot of actions (like updating sections, creating new section and save the .cfg ) the classical Nimbus API is not enougth (It's just here to help people to read cfg files easily). 

## Examples (creating cfg)

```perl
sub createSection {
    my ($CFG,$sectionName) = @_;
    cfgKeyWrite($CFG,$sectionName,"key","value");
    cfgKeyDelete($CFG,$sectionName,"key");
}

my $CFG = cfgOpen("test.cfg", 0);
createSection($CFG,"/setup");
cfgKeyWrite($CFG,"/setup/","loglevel","5"); 
cfgSync($CFG);
cfgClose($CFG);
```

## API 

### cfgOpen(szLocation,bRead) -> CFGHandle

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

### cfgKeyDelete(CFGhandle,szSection,szKey) -> BOOLEAN

Delete a key in a specific section.

```perl
cfgKeyDelete($CFGHandler,"/setup","logsize");
```

### cfgKeyList(CFGhandle,szSection) -> ARRAY

Retrieving an array of keys from a section.

```perl
my ($ARR) = cfgKeyList($CFGHandler,"/setup");
foreach my $keyName ($ARR) {
     my $keyValue = cfgKeyRead($CFGHandler,"/setup",$keyName);
     print "$keyName => $keyValue \n";
}
```

### cfgKeyRead(CFGHandle,szSection,szKey) -> STRING

Read a key value from a section.

### cfgKeyWrite(CFGHandle,szSection,szKey,szValue) -> BOOLEAN

Write a new value for a section/key. 

```perl
cfgKeyWrite($CFGHandler,"/setup","loglevel","5");
```

> If the section does'nt exist it will be created.

### cfgListRead(CFGHandle,szSection) -> BOOLEAN

Reads the section that is specified and returns the list of values as an array. This is a `cfgValueList` method.

Take the following xml : 

```xml
<setup>
    loglevel = 5
    logsize = 10000
</setup>
```

And now you want to retrieve all keys value from setup (so we need 5 and 10000).

```perl
my ($valArr) = cfgListRead($CFGHandler,"/setup");
```

### cfgListWrite(CFGHandle,szSection,szKeyBody,listArr) -> BOOLEAN

Replace a section with the contents of the array list. Each entry in the array is treated as a value. The key names are generated based on the KeyBody prefix (for example, "key" generates "key0", "key1"…).

```perl
my @Equipments = ("T1","T2","T3");
cfgListWrite($CFGHandler,"/equipments","id_",@Equipments);
```

And now your cfg look like 

```xml
<equipments>
    id_0 = T1
    id_1 = T2
    id_2 = T3
</equipements>
```

### cfgSectionCopy(CFGHandle,szSectionFrom,szSectionTo) -> BOOLEAN

Copy section `from` to section `to` with a new name.

```perl
cfgSectionCopy($CFGHandler,"/setup","/setup_copy");
```

### cfgSectionDelete(CFGHandle,szSection) -> BOOLEAN 

Delete a section.

### cfgSectionList(CFGHandle,szSection) -> ARRAY

List all sections from a section 

```perl
my ($ARR) = cfgSectionList($CFGHandler,"/");
foreach my $sectionName ($ARR) {
    cfgSectionDelete($CFGHandler,"/$sectionName");
}
```

### cfgSectionRename(CFGHandle,szOldSectionName,szNewSectionName) -> BOOLEAN

Rename a section 

```perl
cfgSectionRename($CFGHandler,"/setup","/setup_new");
```

## Create a section 

Perl SDK have no method to create a section. So we have to create a key on our needed section (and delete this key right after).

```perl 
cfgKeyWrite($CFGHandler,"/needed_section","key","value");
cfgKeyDelete($CFGHandler,"/needed_section","key");
```

And now you have the section `needed_section` without any key!
