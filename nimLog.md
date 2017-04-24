# nimLog 

nimLog is all method from Perl SDK API that allow to create and manage a log file for your probe.

## Examples 

```perl
my $LOGFILE = "probe.log"; 
nimLogSet($LOGFILE,"",5);
nimLog(3,"Hello world!");
nimLogClose()
```

## API 

### nimLogSet(file,prefix,level)

### nimLogClose()

### nimLog(level,message)

### nimLogSetLevel(level) 

### nimLogTruncate(size)

### nimLogTruncateSize()

### nimLogTruncateTime()

### nimLogPds

### nimLogClose()
