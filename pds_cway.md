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
bytes

### pdsDelete(pds)

This function will free the data related to the provided PDS handle previously created by pdsCreate().

### pdsReset(pds) 

This function will reinitialize the PDS object, to an empty buffer, and initial pointer settings. If you wish to reset
the get pointer please use the pdsRewind() function. This function will wipe out your data. The buffer is not
reallocated

### pdsRewind(pds)

This function will reinitialize the get pointer within the PDS object. This function is used when you want to
perform multiple gets on the PDS.

### pdsDump(pds)

This function will run through the PDS, element for element and print the name, type, size and some of the data
of the current PDS.

### pdsCount(pds)

This convenience function will return the number of PDS elements in the specified PDS object.

### pdsGetNext()

### pdsRemove(pds,key)

Remove a key from PDS Object.

### pdsPut_PCH(key,strval)

Put a new string in the PDS Object.

### pdsPut_INT(key,intval)

Put a new int in the PDS Object.

### pdsPut_PDS(key,pds)

Put a new PDS Object.

### pdsPut_F(key,float)

Put a new Float in the PDS Object.

### pdsPutTable(tablePds,type,table_name)
