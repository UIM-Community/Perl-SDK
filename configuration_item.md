# Configuration Item (CI)

A configuration item (CI )is an entity associated with a device. For example, a disk on a computer or an application running on a system

A CI must have a path (also known as "type"), which is a dotted-decimal path such as "1.1". The path / type is taken from a list available from CiManager.

A CI also has an optional name, which is a free-form string and can be something like "C:" (for a disk name) or "eth0" (for a network device name.) This device name is used to determine the uniqueness of a given CI. A CI unique identifier consists of the device being monitored, the path, and the name. When a remote system is involved, the device unique identifier incorporates the remote system IP address and the local (robot) system device identifier.
