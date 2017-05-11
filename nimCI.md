# The Configuration Item functions

A Configuration Item (CI) is an entity with a set of properties associated 
with it. As an example a disk can be described by manufacturer, volume name, 
device, size etc. Data on Configuration Items is stored in the NIS database. 

A Configuration Item Metric is a monitoring point in a CI. A CI can have 
several Metrics associated with it. As an example a set of CPU metrics could 
contain the Wait, System, Idle and Used metrics.  A metric is roughly 
equivalent to a QoS object in this regard. 

A monitored computer system will typically have one or more devices that are 
being montored. Each of these devices will have one or more Configuration 
Items, which again have one or more Metrics associated with them. Alarms and
QoS messages are bound to the CI and the Metric for the specific monitoring 
point the message is generated for.

## API

#### ciOpenRemoteDevice()
#### ciOpenLocalDevice()
#### ciClose()
#### ciRelationship()
#### ciAttributeString()
#### ciAttributeNumber()
#### ciBindQoS()
#### ciUnBindQoS()
#### ciGetCachePath()
#### ciSessionAlarm()
#### ciAlarm()

- hCI is the CI handle from ciOpen[Remote|Local]Device
- szMetric is the name of the metric
- iLevel is the alarm level (see Level constants).
- szMsg  is the alarm message.
- token  is the alarm token to look up for internationalization.
- pdsVal is a PDS with the alarm values for internationalization (default:none)
- szSub  is the subsystem identifier eg. 1.2.3 (default: 1.1).
- szSup  is the suppression definition (default: none).
- szSrc  is the alarm source (default: localhost).
- szCustom1 is a user defined field (default: none).
- szCustom2 is a user defined field (default: none).
- szCustom3 is a user defined field (default: none).
- szCustom4 is a user defined field (default: none).
- szCustom5 is a user defined field (default: none).
