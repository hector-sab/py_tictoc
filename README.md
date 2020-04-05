# ttictoc
Time execution of blocks of code.

## TocToc
The easiest way to time something is with `tic` and `toc`

```python
from ttictoc import tic,toc
tic() # Start timing
# some code
elapsed = toc() # Gets the elapsed time until this moment
print('Elapsed time:',elapsed)
```

You can execute multiple tocs and will be linked to the `tic` time.
Also, each time `tic` is executed the time holded by `tic` will be
updated.
```python
import time
from ttictoc import tic,toc
tic() # Start timing
time.sleep(1)
tic() # Reset the starting time
time.sleep(1)
print(toc()) # Prints ~1 seconds
time.sleep(1)
print(toc()) # Prints ~2 seconds
```

## Timer Class
The Timer class can be used to have a single and multiple timers.
Examples seen with tic,toc are also valid with Timer start,stop
```python
import time
from ttictoc import Timer

# General timer
t = Timer()
t.start() # Starts the general timer
time.sleep(1)
elapsed = t.stop()
print('Elapsed time:',elapsed)

# Multiple timers
t.start('t0')
for i in range(2):
  tname = 't'+str(i+1)
  t.start(tname)
  time.sleep(1)
  elapsed = t.stop(tname)
  print('[INSIDE LOOP][{}] Elapsed time: {}'.format(tname,elapsed))
t.stop('t0')

print('[OUTSIDE LOOP][{}] Elapsed time: {}'.format('t0',t.elapsed['t0']))
print('[OUTSIDE LOOP][{}] Elapsed time: {}'.format('t1',t.elapsed['t1']))
print('[OUTSIDE LOOP][{}] Elapsed time: {}'.format('t2',t.elapsed['t2']))
```

## Context manager
You can also use it as context manager
```python
import time
from ttictoc import Timer

# Default
with Timer():
  time.sleep(1)

# With out verbose
with Timer(verbose=False) as T:
  time.sleep(1)
print('Elapsed time:',T.elapsed)

# With default verbose message
with Timer(verbose_msg=f'[User msg][{time.time()}] Elapsed time: {{}}'):
  time.sleep(1)
```

## Specify timing method
By default, `Timer` (and `tic`,`toc`) use `timeit.default_timer`. However, the timing function can be selected as follow.
```python
import time
from ttictoc import Timer
t = Timer(func_time=time.clock)
t.start()
time.sleep(5)
elapsed = t.stop()
print('Elapsed time:',elapsed)
```
