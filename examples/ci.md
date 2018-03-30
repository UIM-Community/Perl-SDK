# Nimsoft CI

This example has been take from CA UIM Communities (thanks to carl).
https://communities.ca.com/thread/241721931


```perl
#!perl/bin/perl
use lib "perllib/";
use Nimbus::API;
$ENV{'NIM_ROOT'} = '/opt/nimsoft';
nimInit(0);

#
# NIS2 - Local device example
#
# This example shows how to create a CI representing
# a directory on the local system, and a metric representing
# the available space on that directory. A device that represents
# the local computer system where this probe is running is
# implicitly created by the ciOpenLocalDevice function.
#
# The name of the directory this probe is monitoring
my $dirName = "/var";

# The CI type is the dotted decimal type path (see the
# CM_CONFIGURATION_ITEM_DEFINITION table in the DB for a list of defined types).
my $dirCiType = "1.11"; # System.Directory

# The metric type is the kind of metric to collect for the configuration item
# (see CM_CONFIGURATION_ITEM_METRIC_DEFINITION for defined metric types).
my $dirMetric = "3"; # Directory Space in KB

# The (simulated) measurement value
my $dirSpace = 100; # Measurement - 100 KB remaining

# This creates a CI representing the "/var" directory on the local system.
my $hCI = ciOpenLocalDevice($dirCiType, $dirName);

# Send an alarm for the CI and metric ID
my ($rc,$szId) = ciAlarm($hCI, $dirMetric, 3, "$dirName space is low");

# Define a QoS metric for directory space
my $qosName = "QOS_DIRECTORY_SPACE";
my $qosGroup = "QOS_MACHINE";
my $qosDescr = "Directory Space";
my $qosUnit = "Kilobytes";
my $qosUnitAbbr = "KB";
my $qosInterval = 300;
my $qosSource = ""; # Nimsoft SDK will use the local host address
my $rc = nimQoSSendDefinition($qosName, $qosGroup, $qosDescr, $qosUnit, $qosUnitAbbr);
my $hQoS = nimQoSCreate($qosName, $qosSource, $qosInterval);

# Bind the CI to QoS (establish their relationship)
my $rc = ciBindQoS($hCI, $hQoS, $dirMetric);

# Send the QoS data point
my $rc = nimQoSSendValue($hQoS, $dirName, $dirSpace);

# Clean up
my $rc = ciUnBindQoS($hQoS);
my $rc = nimQoSFree($hQoS);
my $rc = ciClose($hCI);

nimEnd(0);
```
