# PDS C API

Create a PDS with the original FFI of C SDK API. (**Not recommanded because some bugs can occur**).

> **Note**: This API has been documented mostly with the help of C SDK.

## Examples 

```perl
my $PDS = pdsCreate();
pds_putPCH("name","value");
pdsDump($PDS);
my $count = pdsCount($PDS);
print "PDS size => $count\n";
pdsDelete($PDS);
```

## API

### pdsCreate()

This function is a convenience function on top of pdsCreateSize(), and will create a PDS with data size 1024
bytes.

### pdsDelete(pdsHandle)

This function will free the data related to the provided PDS handle previously created by pdsCreate().

### pdsReset(pdsHandle) 

This function will reinitialize the PDS object, to an empty buffer, and initial pointer settings. If you wish to reset
the get pointer please use the pdsRewind() function. This function will wipe out your data. The buffer is not
reallocated

### pdsRewind(pdsHandle)

This function will reinitialize the get pointer within the PDS object. This function is used when you want to
perform multiple gets on the PDS.

### pdsDump(pdsHandle)

This function will run through the PDS, element for element and print the name, type, size and some of the data
of the current PDS.

### pdsCount(pdsHandle)

This convenience function will return the number of PDS elements in the specified PDS object.

### pdsGetNext(PDS)

This function will use the current 'get' position as the starting point for element extraction. Please use the
pdsRewind() function prior to the first pdsGetNext() call. Note that if no pdsGet() or any of the pdsGet
convenience functions (e.g. pdsGet_INT) have been used, then the get pointer is initiated to the start of the PDS
buffer

### pdsSearch(pds,szKey)

Check the PDS $pds if it contains a key $key and retrieve the value, size and type of data	

### pdsRemove(pdsHandle,szKey)

Remove a key from PDS Object.

### pdsPut_PCH(pdsHandle,szKey,szValue)

Put a new string in the PDS Object.

### pdsPut_INT(pdsHandle,szKey,iValue)

Put a new int in the PDS Object.

### pdsPut_PDS(pdsHandle,szKey,pds)

Put a new PDS Object.

### pdsPut_F(pdsHandle,szKey,iFloat)

Put a new Float in the PDS Object.

### pdsPutTable(tablePds,pds_constant,szTableName)

This function will generate indexed elements, from zero (0) and upwards. The table equivalent of the type is used
as the target PDS. For instance will a type of PDS_PCH give a table of type PDS_PPCH.
