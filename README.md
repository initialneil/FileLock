By Neil Z. SHAO:
- fix `__init__.py`
- install:
```
pip install git+https://github.com/initialneil/FileLock.git
```

- example 1:
```
lock_fn = ...

# lock or skip
lock_fn = lock_fn + '.lock' if os.name == 'nt' else lock_fn
locker = FileLock(lock_fn, timeout=0.2)
lock_file = locker.lock_file if os.name == 'nt' else locker.lockfile

try:
    print(f'[Main] try lock {lock_file} ... ', end='')
    locker.acquire()
    print("success")
except:
    print("failed")
    # continue or return
    return

# do stuff...

locker.release()
```

- example 2:
```
lock_fn = ...

# lock or skip
lock_fn = lock_fn + '.lock' if os.name == 'nt' else lock_fn
try:
    with FileLock(lock_fn, timeout=0.2):
        print("Lock success")
        # do stuff...
    
except:
    print("Lock failed")
    # continue or return
    return
```

-----
========
FileLock
========

    A file locking mechanism that has context-manager support so 
    you can use it in a with statement. This should be relatively cross
    compatible as it doesn't rely on msvcrt or fcntl for the locking.
    

    Originally posted at http://www.evanfosmark.com/2009/01/cross-platform-file-locking-support-in-python/
