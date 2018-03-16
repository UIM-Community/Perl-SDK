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

#### ciOpenRemoteDevice(szType, szName, szHost) -> hCI
Open a handle to a remote device

#### ciOpenLocalDevice(szType, szName) -> hCI
Open a handle to a local device

#### ciClose(hCI) -> rc
Close a (CI) handle

#### ciRelationship(hCIParent, hCIChild) -> rc
Set a parent/child relantionship between to devices

#### ciAttributeString(hCI, szKey, szValue) -> rc
Set a string attribute in a handle 

#### ciAttributeNumber(hCI, szKey, iValue) -> rc
Set a numeric attribute in a handle 

#### ciBindQoS(hCI, hQos, szMetric) -> rc
Bind a QoS to a metric on a device

#### ciUnBindQoS(hQoS) -> rc
Remove the binding to a device in a QoS handle

#### ciGetCachePath() -> (rc, szPath)
Get the path to the component information cache on the local system

#### ciSessionAlarm() -> (rc, szId)
Send an alarm bound to a metric on a device using a session to the spooler

#### ciAlarm(...arguments) -> (rc, szId)

All available arguments are the following: 

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
