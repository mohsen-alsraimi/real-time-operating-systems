Day 26 — Race Conditions, Mutexes, Semaphores, and Critical Sections

Today I studied one of the most important problems in multithreaded programming: what happens when multiple tasks access the same data or hardware resource.

I learned about shared resources, such as global variables, UART, SPI, I²C, and memory buffers. When two tasks access the same resource without proper synchronization, a race condition can occur. I studied how an operation such as counter++ may actually involve separate load, modify, and store instructions, allowing a context switch to occur in the middle and produce an incorrect result.

I learned that using volatile does not make shared data thread-safe. volatile only tells the compiler that a variable may change unexpectedly; it does not make multi-step operations atomic or prevent race conditions.

I studied critical sections, which protect very short pieces of code that must not be interrupted by conflicting execution. I learned that critical sections should be kept as short as possible because they can temporarily restrict scheduling or interrupt handling.

I then studied mutexes, which provide mutual exclusion for shared resources. Only one task can own a mutex at a time. If another task tries to acquire the same mutex, it can become Blocked until the resource is released. I learned how mutexes can safely protect shared peripherals such as UART, SPI, and I²C so that multiple tasks do not interfere with each other's transactions.

I also studied binary and counting semaphores. Binary semaphores are useful for event signaling, such as notifying a task that a button interrupt or DMA transfer has occurred. Counting semaphores can represent multiple pending events or multiple available resources.

I learned the important difference between a mutex and a semaphore. A mutex is mainly used to protect ownership of a shared resource, while a semaphore is mainly used for synchronization and event signaling.

I studied priority inversion, where a high-priority task can become blocked waiting for a resource owned by a low-priority task while a medium-priority task prevents the low-priority task from running. I learned how mutexes can use priority inheritance to temporarily increase the low-priority task's priority so it can finish and release the resource.

I also learned about deadlock, where two tasks wait indefinitely for resources owned by each other. I studied how consistent lock ordering, timeouts, simpler resource designs, and shorter lock durations can help avoid deadlocks.

Finally, I connected synchronization with hardware interrupts. Instead of performing large amounts of work inside an ISR, the interrupt can signal a task using a semaphore or similar RTOS mechanism. The task then wakes and performs the longer processing. This is known as deferred interrupt processing.

The main concept I learned was that safe multithreading requires coordination. Mutexes protect shared resources, semaphores synchronize events, and critical sections protect very short atomic operations, while incorrect synchronization can lead to race conditions, starvation, priority inversion, or deadlock.
