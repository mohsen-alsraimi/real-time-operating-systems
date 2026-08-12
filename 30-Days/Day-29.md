Day 29 — Complete Multithreaded STM32 FreeRTOS System

Today I studied how to combine the individual STM32 and FreeRTOS concepts learned during the previous days into a complete multithreaded embedded-system architecture. Instead of treating tasks, queues, interrupts, peripherals, and synchronization mechanisms separately, I learned how they work together as one system.

I learned how to divide an embedded application into multiple tasks according to responsibility. A Sensor Task can acquire ADC measurements, a Processing Task can process those measurements, a UART Task can handle communication with the computer, and a Control Task can handle buttons and system events. This keeps each task focused on a specific job.

I studied how to build a data-processing pipeline using queues. Sensor data can flow through the system as Sensor → ADC → Sensor Task → Queue → Processing Task → Queue → UART Task → UART → PC. This architecture allows tasks to exchange complete messages without depending heavily on shared global variables.

I learned how task blocking makes this architecture efficient. The Processing Task can remain Blocked while waiting for sensor data, and the UART Task can remain Blocked while waiting for messages. When data becomes available, FreeRTOS changes the appropriate task from Blocked to Ready and the scheduler decides when it should execute.

I also connected hardware interrupts with FreeRTOS tasks. A button can generate a GPIO/EXTI interrupt, which is handled through the NVIC and Cortex-M3 exception system. Instead of performing large operations inside the ISR, the interrupt can signal a semaphore or event that wakes the Control Task. This implements deferred interrupt processing, keeping ISRs short while moving application logic into normal task context.

I studied how task priorities should be selected according to timing and latency requirements rather than simply how important a task appears. A processing or control task may require higher priority, while UART logging can usually operate at a lower priority.

I connected the scheduler with the underlying Cortex-M3 hardware. SysTick provides timing used by the RTOS, PendSV is used for context switching, and SVC participates in kernel-related operations. During a context switch, the execution context of the current task is saved and another task's context and stack are restored.

I also studied how DMA can improve the architecture. Instead of the CPU manually moving every ADC sample, the ADC can work with DMA to transfer samples directly into SRAM. When the transfer finishes, an interrupt can notify the Processing Task, allowing the CPU to perform other work while the hardware handles data movement.

I learned the importance of peripheral ownership. Instead of allowing many tasks to access UART directly and requiring a mutex, a dedicated UART Task can own the peripheral while other tasks send messages to it through a queue. This reduces resource conflicts and simplifies synchronization.

I also studied the memory cost of an RTOS application. SRAM is required for task stacks, Task Control Blocks, queues, semaphores, event flags, software timers, buffers, global variables, and RTOS kernel data. Therefore, creating unnecessary tasks, excessively large stacks, or oversized queues can waste the limited SRAM available on the STM32.

Finally, I studied several problems that must be considered when designing and debugging a multithreaded system, including queue overflow, stack overflow, race conditions, deadlocks, starvation, incorrect priorities, and insufficient processing throughput. Debugging an RTOS system requires understanding not only individual lines of C code but also task states, resource ownership, communication paths, timing, and synchronization.

The main concept I learned was how the complete system fits together: STM32 peripherals perform hardware operations, interrupts report hardware events, RTOS synchronization mechanisms wake the appropriate tasks, queues transfer data between tasks, and the scheduler determines which Ready task receives the Cortex-M3 CPU. This creates an organized, event-driven multithreaded embedded system rather than placing all application logic inside one while(1) loop.
