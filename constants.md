# Perl SDK Constants

## Alarms 

| Constant name | value (INT) | 
| --- | --- |
| NIML_CLEAR | 0 |
| NIML_INFO | 1 |
| NIML_WARNING | 2 |
| NIML_MINOR | 3 |
| NIML_MAJOR | 4 | 
| NIML_CRITICAL | 5 |

### QoS flags

| Flags |
| --- | 
| NIMQOS_DEF_NONE | 
| NIMQOS_DEF_BOOLEAN | 
| NIMQOS_DEF_HASMAX |
| NIMQOS_DEF_ASYNCH |
| NIMQOS_DEF_REDEFINE |

### Logs flags

| Flags |
| --- |
| NIM_LOGF_NOTRUNC |
| NIM_LOGF_RESETATSTART |

## Flags (nimFind API)

| Flags | Description |
| --- | --- |
| NIMF_HUB | returns a list of Hub addresses |
| NIMF_ROBOT | returns a list of Robot addresses |
| NIMF_PROBE | returns a list of Probe addresses |
