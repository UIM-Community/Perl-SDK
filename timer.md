# nimTimer 

These functions give you access to high-resolution timers. 
nimTimerDiff* will return the time since started, unless nimTimerStop() has been called, in which case it will return the time difference between start and stop.

```perl
my ($time) = nimTimerCreate(); 
nimTimerStart($time);

my ($diffMs) = nimTimerDiff($time); 
print "$diffMs\n" # print difference between time and now in milliseconds

my ($diffSecond) = nimTimerDiffSec($time);
print "$diffSecond\n" # print difference between time and now in seconds.

nimTimerStop($time);
nimTimerFree($time);
```

## API

#### nimTimerCreate() -> Time 

Create a new time. Return a timer object.

#### nimTimerStart(timer)

Start a timer (not started automatically). 

#### nimTimerStop(timer) 

Stop a timer

#### nimTimerFree(timer)

Destroy memory allocation for the timer.

#### nimTimerDiff(timer) -> iMS

Return the difference between the timer start date and now in milliseconds.

#### nimTimerDiffSec(timer) -> iSec

Return the difference between the timer start date and now in seconds.
