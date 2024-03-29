# virtual-memory
虚拟内存：
1、虚拟内存是操作系统提供的一种机制，将内存作为磁盘的缓存。
2、每个进程都生存在虚拟地址空间，虚拟地址va（virtual address）通过mmu（memory management unit，cpu上的专用硬件）翻译成pa（physical address）。
3、每个进程都有一个页表，指令访问内存时，将虚拟地址映射到页表上，判断此页是否在内存中，若不在内存中，触发缺页中断，中断处理程序将次磁盘中的页面置换到内存中，将一个内存页换到磁盘中，置换完成后，cpu重新访问内存，此时页面已在内存中，可以正常访问。

虚拟内存的优点
1、虚拟内存方便内存地址的管理，每个进程都有一致的地址空间，降低了复杂性。
2、降低链接器的设计难度，可以链接生成代码地址固定但是又独立于实际物理内存中的可执行文件。
3、简化加载，加载器加载时只需要将页表指向磁盘，当cpu访问到相应页面时，触发缺页中断自动置换页面进入内存。
4、虚拟内存方便内存共享，不同进程的地址空间可以指向同一块内存，通过页表映射到内存，页表中还保存进程对内存页的权限，如果违反条件，就会调用segment falut的异常处理程序。
5、简化内存分配，当调用malloc时，直接在虚拟内存中分配连续的内存地址，再通过页表映射到物理内存中，由于页表的存在，物理内存可以随机的分配在不同位置。
