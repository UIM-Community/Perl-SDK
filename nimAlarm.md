# nimAlarm

This method allow to generate very simple alarm.

## Examples

```perl
my ($RC,$AlarmID) = nimAlarm(NIML_CRITICAL,"Hello world!","1.1.1")
if($RC == NIME_OK) {
    print "$AlarmID\n"
}
```

## Severity 

| Constant name | value (INT) | 
| NIML_CLEAR | 0 |
| NIML_INFO | 1 |
| NIML_WARNING | 2 |
| NIML_MINOR | 3 |
| NIML_MAJOR | 4 | 
| NIML_CRITICAL | 5 |

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
