# nimAlarm

This method allow to post simple Alarm on the Nimbus.

## Examples

```perl
my ($RC,$AlarmID) = nimAlarm(NIML_CRITICAL,"Hello world!","1.1.1")
if($RC == NIME_OK) {
    print "$AlarmID\n"
}
```

## Severity constants

| Constant name | value (INT) | 
| --- | --- |
| NIML_CLEAR | 0 |
| NIML_INFO | 1 |
| NIML_WARNING | 2 |
| NIML_MINOR | 3 |
| NIML_MAJOR | 4 | 
| NIML_CRITICAL | 5 |

## API

### nimAlarm(iCriticity,szMessage,szSubsys,szSupp_key,szSource)

| argument | type | default value |
| --- | --- | --- |
| criticity | INT | undef | 
| alarmMessage | STRING | undef | 
| subsystem_id | STRING | "1.1" | 
| supkey | STRING | "none" | 
| alarmSource | STRING | "localhost" | 

> If you put your own subsystem id, dont forgot to create it on the Nas probe!
