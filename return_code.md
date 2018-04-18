# Return code

| Constant variable | Value (int) | Description |
| --- | --- | --- |
| NIME_OK | 0 | All is ok ! |
| NIME_ERROR | 1 | A error occured while execution the action |
| NIME_COMERR | 2 | A communication error occured | 
| NIME_INVAL | 3 | N.A | 
| NIME_NOENT | 4 | Most of the time, that mean the callback does'nt exist ! |
| NIME_ISENT | 5 | N.A |
| NIME_ACCESS | 6 | nimLogin is not correct | 
| NIME_AGAIN | 7 | N.A |
| NIME_NOMEM | 8 | N.A |
| NIME_NOSPC | 9 | N.A |
| NIME_EPIPE | 10 | N.A |
| NIME_NOCMD | 11 | N.A | 
| NIME_LOGIN | 12 | N.A | 
| NIME_SIDEXP | 13 | N.A | 
| NIME_ILLMAC | 14 | N.A | 
| NIME_ILLSID | 15 | N.A | 
| NIME_SIDSESS | 16 | N.A | 
| NIME_EXPIRED | 17 | N.A |
| NIME_NOLIC | 18 | N.A |
| NIME_INVLIC | 19 | N.A |
| NIME_ILLIC | 20 | N.A |
| NIME_INVOP | 21 | N.A |
| NIME_USER | 100 | N.A | 

Nimsoft API only return the integer code. If you want a complete description, use the `nimError2Txt` method to get the linked string description.

```perl
my $nimError = nimError2Txt($RC);
print "Error ($RC): $nimError\n";
```

## How to use ?

In your perl code you can check these return code with the linked Nimbus constant ! 

```perl
if(NIME_OK == 0) {
   # TRUE
}
```

If you made a nimRequest (or nimNamedRequest) the best practice it's to use the constant variable and not the int value directly. For example : 

```perl
# GOOD
if($RC == NIME_OK) {

}
```

```perl
# BAD
if($RC == 0) {

}
```

## Note 

If you try to execute your script directly on the system and you get a NIME_ACCESS error. This is because you have to log your script to the hub.

Add this to your code : 

```perl
my ($nimCS) = nimLogin('login', 'password');
if(not defined $nimCS) {
    print STDERR "NimBUS Authentication failed!\n";
}
```
