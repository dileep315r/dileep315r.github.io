#### Virtualization
1. A hypervisor is software that creates and runs virtual machines (VMs).
2. The physical hardware, when used as a hypervisor, is called the host, while the many VMs that use its resources are guests
3. The hypervisor gives each virtual machine the resources that have been allocated and manages the scheduling of VM resources against the physical resources
4. Hyper-V host administrator can select hypervisor scheduler types that are best suited for the guest virtual machines (VMs) and configure the VMs to take advantage of the scheduling logic
5. Hardware virtualization. See [link](https://security.stackexchange.com/questions/175789/does-the-main-os-run-virtualised-under-the-ring-1-hypervisor) to know how the hardware virtualization works.
   1. Hardware provides a way to intercept privileged instructions to the hypervisor. Hypervisor safely emulates the privileged instruction.
   2. When a privileged instruction is to be executed in a guest, it is automatically trapped and the guest exits in a process called vmexit, and the hypervisor is allowed to determine whether or not the instruction should be allowed, and can safely emulate it if it so wishes. After it has made its decision, it gives control back to the guest using vmenter, and the guest continues along like nothing happened until it runs into another privileged instruction that forces it to give control back to the hypervisor.
 #### Docker
 1. Process space and resources seggregated in an OS.
 2. Just some libraries on top and the processes would run.
 3. Lightweight container.
 
 