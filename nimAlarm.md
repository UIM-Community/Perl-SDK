# nimAlarm

This method allow to generate very simple alarm.

## Examples

```perl
my ($RC,$AlarmID) = nimAlarm(5,"Hello world!","1.1.1")
if($RC == NIME_OK) {
    print "$AlarmID\n"
}
```

## API

### nimAlarm(criticity,alarmMessage,subsystem_id,supkey,alarmSource)

| argument | type | default value |
| --- | --- | --- |
| criticity | INT | undef | 
| alarmMessage | STRING | undef | 
| subsystem_id | STRING | "1.1" | 
| supkey | STRING | "none" | 
| alarmSource | STRING | "localhost" | 

> If you put a subsystem_id (think to create this one in the NAS probe).
