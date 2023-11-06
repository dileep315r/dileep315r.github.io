1. Every Android application runs in its own process, with its own instance of the Dalvik virtual machine. Dalvik has been written so that a device can run multiple VMs efficiently. The Dalvik VM executes files in the Dalvik Executable (.dex) format which is optimized for minimal memory footprint. The VM is register-based, and runs classes compiled by a Java language compiler that have been transformed into the .dex format by the included "dx" tool.
2. The Dalvik VM relies on the Linux kernel for underlying functionality such as threading and low-level memory management.
3. When an application component starts and the application doesn't have any other components running, the Android system starts a new Linux process for the application with a single thread of execution. By default, all components of the same application run in the same process and thread, called the main thread.
4. If an application component starts and there is already a process for that application, because another component from the application already started, then the component starts within that process and uses the same thread of execution. However, you can arrange for different components in your application to run in separate processes, and you can create additional threads for any process.
5. The system does not create a separate thread for each instance of a component. All components that run in the same process are instantiated in the UI thread, and system calls to each component are dispatched from that thread. Consequently, methods that respond to system callbacks—such as onKeyDown() to report user actions, or a lifecycle callback method—always run in the UI thread of the process.
6. Bear in mind that the Android UI toolkit is not thread-safe. So, don't manipulate your UI from a worker thread. Do all manipulation to your user interface from the UI thread. There are two rules to Android's single-thread model:
  1. Don't block the UI thread.
  2. Don't access the Android UI toolkit from outside the UI thread.
3. 

#### References
   1. https://web.archive.org/web/20081217032436/http://code.google.com/android/what-is-android.html
   1. [Memory management](https://developer.android.com/topic/performance/memory-overview)
   2. https://developer.android.com/guide/components/processes-and-threads
   3. [Common mistakes to avoid to improve performance](https://developer.android.com/topic/performance/memory)
   4. https://developer.android.com/guide/components/processes-and-threads
   5. https://developer.android.com/guide/topics/processes/process-lifecycle
   6. 
