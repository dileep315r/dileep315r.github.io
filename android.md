1. Every Android application runs in its own process, with its own instance of the Dalvik virtual machine. Dalvik has been written so that a device can run multiple VMs efficiently. The Dalvik VM executes files in the Dalvik Executable (.dex) format which is optimized for minimal memory footprint. The VM is register-based, and runs classes compiled by a Java language compiler that have been transformed into the .dex format by the included "dx" tool.
2. The Dalvik VM relies on the Linux kernel for underlying functionality such as threading and low-level memory management.

#### References
   1. https://web.archive.org/web/20081217032436/http://code.google.com/android/what-is-android.html
   1. [Memory management](https://developer.android.com/topic/performance/memory-overview)
   2. 
