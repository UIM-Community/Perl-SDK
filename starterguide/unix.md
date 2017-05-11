# Starter Guide - UNIX

## 1. Download SDK_Perl  

Download SDK_Perl package from [Nimsoft Archive](https://support.nimsoft.com/Default.aspx?center=felles/loginSmall&tourl=felles/archive&name=archive)

Depending on your UNIX system download the right perl packages too.

And put these .zip files onto your archive (with Infrastructure Manager or Admin Console).

## 2. Install perl packages on hub(s)

Install all packages on the desired hub (or hubs). 

After installation, check your nimsoft directory and verify if you have perllib and perl64 directories. If they are on the system this is good.

## 3. Env variables

Now in the Nimsoft directory you have two directory named `perllib`. Check your robot environment variables to find PERL5LIB variable.

## 4. Lib paths

Update the lib paths on your main perl script.

```perl
use lib "/opt/nimsoft/perllib";
use lib "/opt/nimsoft/perl/lib";
```
