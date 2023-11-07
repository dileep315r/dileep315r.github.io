1. Every Android application runs in its own process, with its own instance of the Dalvik virtual machine. Dalvik has been written so that a device can run multiple VMs efficiently. The Dalvik VM executes files in the Dalvik Executable (.dex) format which is optimized for minimal memory footprint. The VM is register-based, and runs classes compiled by a Java language compiler that have been transformed into the .dex format by the included "dx" tool.
2. The Dalvik VM relies on the Linux kernel for underlying functionality such as threading and low-level memory management.
3. When an application component starts and the application doesn't have any other components running, the Android system starts a new Linux process for the application with a single thread of execution. By default, all components of the same application run in the same process and thread, called the main thread.
4. If an application component starts and there is already a process for that application, because another component from the application already started, then the component starts within that process and uses the same thread of execution. However, you can arrange for different components in your application to run in separate processes, and you can create additional threads for any process.
5. The system does not create a separate thread for each instance of a component. All components that run in the same process are instantiated in the UI thread, and system calls to each component are dispatched from that thread. Consequently, methods that respond to system callbacks—such as onKeyDown() to report user actions, or a lifecycle callback method—always run in the UI thread of the process.
6. Bear in mind that the Android UI toolkit is not thread-safe. So, don't manipulate your UI from a worker thread. Do all manipulation to your user interface from the UI thread. There are two rules to Android's single-thread model:
  1. Don't block the UI thread.
  2. Don't access the Android UI toolkit from outside the UI thread.
7. This is primarily true for methods that can be called remotely, such as methods in a bound service. When a call on a method implemented in an IBinder originates in the same process in which the IBinder is running, the method is executed in the caller's thread. However, when the call originates in another process, the method executes in a thread chosen from a pool of threads that the system maintains in the same process as the IBinder. It's not executed in the UI thread of the process.
8. Android offers a mechanism for IPC using RPCs, in which a method is called by an activity or other application component but executed remotely in another process, with any result returned back to the caller. This entails decomposing a method call and its data to a level the operating system can understand, transmitting it from the local process and address space to the remote process and address space, and then reassembling and reenacting the call there.
9. A task is a collection of activities that users interact with when trying to do something in your app. These activities are arranged in a stack called the back stack in the order in which each activity is opened.
10. Because the activities in the back stack are never rearranged, if your app lets users start a particular activity from more than one activity, a new instance of that activity is created and pushed onto the stack, rather than bringing any previous instance of the activity to the top. As such, one activity in your app might be instantiated multiple times, even from different tasks
11. On Android, storage isn’t used for swap space like it is on other Linux implementations since frequent writing can cause wear on this memory, and shorten the life of the storage medium.
12. With a testable app architecture, the code follows a structure that allows you to easily test different parts of it in isolation. Testable architectures have other advantages, such as better readability, maintainability, scalability, and reusability.
13. Common decoupling techniques include the following:
    1. Split an app into layers such as Presentation, Domain, and Data. You can also split an app into modules, one per feature.
    2. Avoid adding logic to entities that have large dependencies, such as activities and fragments.      3. Use these classes as entry points to the framework and move UI and business logic elsewhere, such as to a Composable, ViewModel, or domain layer.
    4. Avoid direct framework dependencies in classes containing business logic. For example, don't use Android Contexts in ViewModels.
    5. Make dependencies easy to replace. For example, use interfaces instead of concrete implementations. Use Dependency injection even if you don't use a DI framework.

#### References
   1. https://web.archive.org/web/20081217032436/http://code.google.com/android/what-is-android.html
   1. [Memory management](https://developer.android.com/topic/performance/memory-overview)
   2. https://developer.android.com/guide/components/processes-and-threads
   3. [Common mistakes to avoid to improve performance](https://developer.android.com/topic/performance/memory)
   4. https://developer.android.com/guide/components/processes-and-threads
   5. https://developer.android.com/guide/topics/processes/process-lifecycle
   6. https://developer.android.com/guide/components/services
   7. https://developer.android.com/guide/components/activities/tasks-and-back-stack
   8. https://developer.android.com/training/testing/fundamentals
   9. 
