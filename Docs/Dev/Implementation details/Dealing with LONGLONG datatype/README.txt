# LONGLONG Data type

## Why is LONGLONG Data type required?

Traditionally one used Long data type (32-bit) to represent the size of a file (the size of a BLOB in this case). However, using an unsigned 32-bit integer only gives access to files the size of 4,294,967,295 bytes (i.e. ~4.3GB). Nowadays it's fairly common that files upwards of 4.3GB exist. A 64-bit integer however can represent ~1.8x10^19 bytes of data (18 exabytes). This is far more data than a file will realistically be in the next milenium.

Thus in our data type we should use 64-bit integers to represent the size of a BLOB in our format.


## Implementation details in 32-bit and 64-bit

### 32-Bit systems

In 32-bit systems, `IntPtr` is defined as a 32 bit integer. Thus an own 64-bit data type needs to be created.

Resources:
~~~~~~~~~~
http://www.geoffchappell.com/studies/windows/win32/kernel32/api/index.htm
https://source.winehq.org/WineAPI/
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kernel32.dll functions:

LONGLONG RtlLargeIntegerAdd(LONGLONG a, LONGLONG b)			See: https://source.winehq.org/WineAPI/RtlLargeIntegerAdd.html
LONGLONG RtlLargeIntegerArithmeticShift(LONGLONG a, INT count)		See: https://source.winehq.org/WineAPI/RtlLargeIntegerArithmeticShift.html
LONGLONG RtlLargeIntegerNegate(LONGLONG a)				See: https://source.winehq.org/WineAPI/RtlLargeIntegerNegate.html
LONGLONG RtlLargeIntegerShiftLeft(LONGLONG a, INT count)		See: https://source.winehq.org/WineAPI/RtlLargeIntegerShiftLeft.html
LONGLONG RtlLargeIntegerShiftRight(LONGLONG a, INT count)		See: https://source.winehq.org/WineAPI/RtlLargeIntegerShiftRight.html
LONGLONG RtlLargeIntegerSubtract(long a, long b)			See: https://source.winehq.org/WineAPI/RtlLargeIntegerSubtract.html


To declare use string instead of LONGLONG. Strings will be fixed at 4 chars long (4 bytes + 1 byte (null termination)). _Assumption here that passing 5 bytes to a 4 byte datatype won't matter, not necessarily correct. Might need to allocate in memory and pass value of pointer._

Declare Function RtlLargeIntegerAdd Lib "kernel"(a as string, b as string) as string




### 64-bit systems

`IntPtr` data type can be used to handle long values