# PDS C API

Create a PDS with the original FFI of C SDK API. (**Not recommanded because some bugs can occur**).

> **Note**: This API has been documented mostly with the help of C SDK.

## Examples 

```perl
use Nimbus::API;

my $PDS = pdsCreate();
pds_putPCH("name","value");
pdsDump($PDS);

my $count = pdsCount($PDS);
print "PDS size => $count\n";
pdsDelete($PDS);
```

## API

### pdsCreate() -> pdsHandle

This function is a convenience function on top of pdsCreateSize(), and will create a PDS with data size 1024
bytes.

```perl
my $PDS = pdsCreate();
```

### pdsDelete(pdsHandle) -> iRc

This function will free the data related to the provided PDS handle previously created by pdsCreate().

### pdsReset(pdsHandle)  -> iRc

This function will reinitialize the PDS object, to an empty buffer, and initial pointer settings. If you wish to reset
the get pointer please use the pdsRewind() function. This function will wipe out your data. The buffer is not
reallocated

### pdsRewind(pdsHandle) -> iRc

This function will reinitialize the get pointer within the PDS object. This function is used when you want to
perform multiple gets on the PDS.

### pdsDump(pdsHandle) -> void

This function will run through the PDS, element for element and print the name, type, size and some of the data
of the current PDS.

```perl
pdsDump($PDS); // will output the PDS in the terminal and in the nimLogger
```

### pdsCount(pdsHandle) -> iSize

This convenience function will return the number of PDS elements in the specified PDS object.

### pdsGetNext(PDS) -> (rc, szKey, szType, iSize, data)

This function will use the current 'get' position as the starting point for element extraction. Please use the
pdsRewind() function prior to the first pdsGetNext() call. Note that if no pdsGet() or any of the pdsGet
convenience functions (e.g. pdsGet_INT) have been used, then the get pointer is initiated to the start of the PDS
buffer

### pdsGet_INT(pdsHandle, szKey) -> iVal

Retrieve the integer value $iVal corresponding to key $szKey from the PDS $pds	

### pdsGet_PCH(pdsHandle, szKey) -> szVal

Retrieve the string value $szVal corresponding to key $szKey from the PDS $pds

### pdsGet_PDS(pdsHandle, szKey) -> pds2

Retrieve the PDS $pds2 corresponding to key $szKey from the PDS $pds. Should call pdsDelete on the returned PDS ($pds2) to avoid memory leak!	

### pdsSearch(pdsHandle, szKey)

Check the PDS $pds if it contains a key $key and retrieve the value, size and type of data	

### pdsRemove(pdsHandle, szKey)

Remove a key from PDS Object.

### pdsPut_PCH(pdsHandle, szKey, szValue)

Put a new string in the PDS Object.

```perl
my $PDS = pdsCreate();
pdsPut_PCH($PDS, "key", "value");
```

### pdsPut_INT(pdsHandle, szKey, iValue)

Put a new int in the PDS Object.

```perl
my $PDS = pdsCreate();
pdsPut_INT($PDS, "key", 10);
```

### pdsPut_F(pdsHandle, szKey, iFloat)

Put a new Float in the PDS Object.

```perl
my $PDS = pdsCreate();
pdsPut_F($PDS, "key", 0.5);
```

### pdsPut_PDS(pdsHandle, szKey, pds)

Put a new PDS Object.

```perl
my $PDS = pdsCreate();
my $DATA = pdsCreate();
pdsPut_PDS($PDS, "subPds", $DATA);
```

### pdsPutTable(tablePds, pds_constant, szTableName)

This function will generate indexed elements, from zero (0) and upwards. The table equivalent of the type is used
as the target PDS. For instance will a type of PDS_PCH give a table of type PDS_PPCH.
