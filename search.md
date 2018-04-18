# Search API

## Example 

Return a list of Nimsoft probe addresses where he finded the "nas" probe.

```perl
my $PDS = Nimbus::PDS->new();
$PDS->string("probename", "nas");
my ($RC, $pdsRET) = nimFindAsPds($PDS->data, NIMF_PROBE);
pdsDump($pdsRET) if $RC == NIME_OK;
```

If you want to recover the first addr, take a look at the following code
```perl
my $nasAddr = Nimbus::PDS->new($pdsRET)->getTable("addr", PDS_PCH);
```

There is an issue around how PDS handle some Array type (so it could be difficult to get multiple addr depending on the used API).

## Constants

All filter fields (with the exception of timeout) are regular expressions. Timeout specifies the timeout for each query the function executes.

### Filters

| Filter(s) string |
| --- |
| domain |
| hubip |
| hubname |
| hubversion |
| robotip |
| robotname |
| robotversion |
| osmajor |
| osminor |
| osuser1 |
| osuser2 |
| probename | 
| pkg_name |
| pkg_version |
| group |
| active |
| timeout |

### Flags

| Flags | Description |
| --- | --- |
| NIMF_HUB | returns a list of Hub addresses |
| NIMF_ROBOT | returns a list of Robot addresses |
| NIMF_PROBE | returns a list of Probe addresses |

## API

The find functions take a PDS with filters for different search criteria and a flag specifying the type of search as input.

#### nimFindAsPds(pdsFilter,iFlags)
> Return rc,data

This is a wrapper around nimFindAsFunc(). pdsPutTable() is used to fill pdsOut

#### nimFindAsTable(pdsFilter,iFlags)
> Return rc,data

This is a wrapper around nimFindAsFunc(). cslLineInsert() is used to fill pppchOut
