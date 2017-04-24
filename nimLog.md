# nimLog 

nimLog is all method from Perl SDK API that allow to create and manage a log file for your probe.

## Examples 

```perl
my $LOGFILE = "probe.log"; 
nimLogSet($LOGFILE,"prefix - ",5);
nimLogTruncateSize(512 * 1024);
nimLog(3,"Hello world!"); 
nimLogSetLevel(2);
nimLog(3,"Hello world!"); # Skipped
nimLogClose()
```

## API 

### nimLogSet(file,prefix,level)

Create log utility. (Like a class constructor).

### nimLogClose()

Close a log handle.

### nimLog(level,message)

Log a message in the current nimLog handler (defined with nimLogSet);

### nimLogSetLevel(level) 

Set a new log-level

### nimLogTruncate()

Launch a new truncate of the file (can be defined with `nimLogTruncateSize` **OR** `nimLogTruncateTime` method).

```perl
nimLogTruncateSize(512 * 1024);
sleep(10);
nimLogTruncate(); # Run 512 KB truncate!
```

### nimLogTruncateSize(size)

Truncate logsize (in KB). So it's base * 1024. (For example 512KB is 512*1024).

```perl
nimLogTruncateSize(512 * 1024);
```

> Warn: Truncate only support one method (time or size) at the same time.

### nimLogTruncateTime(time)

Truncate the logfile based on time. Time is in `seconds`.

```perl
nimLogTruncateTime(60 * 10); # 10 minutes.
```

> Warn: Truncate only support one method (time or size) at the same time.

### nimLogPds(pds,print_name,loglevel,detail)

Dump a PDS object to the log.

### nimLogClose()

Close the log.
