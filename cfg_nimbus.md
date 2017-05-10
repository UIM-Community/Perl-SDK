# CFG (Nimbus::CFG)

The CFG object is a class wrapper around the functions that are targeted against configuration files. The relevant functions are listed in the CFG.pm module.

Nimbus::API::cfg*

When a new CFG object is constructed the constructor takes one required argument (the configuration filename), and one optional (a 'private' hash). It is normal to maintain the hash within the CFG object, but in some cases it can be useful to add the configuration data to a private hash.

## Example

```xml
<setup>
logfile = stdout
loglevel = 2
	<names> 
 		name_0 = luke 
 		name_1 = leia 
 		name_2 = r2d2
	</names>
</setup>
```

Now require this cfg in your perl code 

```perl 
use Nimbus::CFG;
my $cfg      = Nimbus::CFG->new("test.cfg");

my $logfile  = $cfg->{setup}->{logfile} || "output";
my $loglevel = $cfg->{setup}->{loglevel} || 5; 
print "$logfile - $loglevel \n";
```

## API 

### new(fileLocation) -> cfgHandle

Create a new cfg.

### debug(boolean) -> VOID

Set debug to 1 or 0.

---
### dump(cfgHandle) -> VOID

Dump the cfg content 

```perl
$cfg->dump($cfg);
```

---
### getKeys(section) -> ARRAY

Get all keys from a section. 

```perl
foreach my $key ( $cfg->getKeys( $cfg->{"setup"} ) ) {
    print "$key\n"; # print logfile and loglevel
}
```

---
### getSections(section) -> ARRAY

Get all section from a section 

```perl
foreach my $section ( $cfg->getSections( $cfg->{"setup"} ) ) {
    print "$section\n"; # print name
}
```

---
### getValues(section) -> ARRAY


Get all keys values from a section 

```perl
foreach my $val ( $cfg->getValues( $cfg->{"setup"} ) ) {
    print "$val\n"; # print stdout and 2
}
```

---
### open(cfgHandle) -> VOID

Open a new cfg (same as using new). Can be useful when you use a private converter.

---
### setConverter(&src,&dst) -> VOID

The setConverter method takes a reference to a function as a parameter. This function is called whenever a new section is parsed. The default converter substitutes every hash(#) in a section name with a slash(/). This can be useful when using the slash (/) character as part of the section/key name, such as a filename or equivalent.

Create a new .cfg file like this (namned my.cfg). 
```xml
<filesystems>
    <#dev#dsk#c0t3d0s4>
        name = /usr
            high = 99
            low  = 70
    </#dev#dsk#c0t3d0s4>
</filesystems
```

**Script using the standard/builtin converter** 

```perl
use Nimbus::CFG;
my $cfg = Nimbus::CFG->new("my.cfg");
my $fs1 = $cfg->{filesystems}->{'/dev/dsk/c0t3d0s4'};

print "filesystem1: $fs1->{name}, high:$fs1->{high} \n";
==> will print 'filesystem1: /usr, high:99'
```

**Script using a private converter** 

```perl
use Nimbus::CFG;

sub myconv {
    my $s = shift;
    $$s =~ s/\#/\>/g;   # convert from hash(#) to GT(>)
}

my $cfg = Nimbus::CFG->new();
$cfg->setConverter(\&myconv);

$cfg->open("my.cfg");
my $fs1 = $cfg->{filesystems}->{'>dev>dsk>c0t3d0s4'};

print "filesystem1: $fs1->{name}, high:$fs1->{high} \n";
==> will print 'filesystem1: /usr, high:99'.
```

