Day 24 — Introduction to FreeRTOS and Multithreaded Programming

Today I started studying FreeRTOS and multithreaded programming on the STM32F103. I learned why an RTOS becomes useful when a program has several independent jobs such as reading sensors, handling UART communication, updating LEDs, and processing data at different times.

I studied the difference between a traditional superloop and an RTOS-based design. In a superloop, all application functions are executed one after another inside while(1). In FreeRTOS, the application is divided into separate tasks, where each task is responsible for a specific job.

I learned that the STM32F103 still has only one Cortex-M3 CPU core, so the tasks are not truly executing in parallel on multiple processors. Instead, FreeRTOS provides concurrency by rapidly switching the CPU between tasks using a scheduler.

I studied the main task states: Running, Ready, Blocked, and Suspended. A Running task currently owns the CPU, a Ready task can run but is waiting for CPU time, a Blocked task is waiting for a delay or event, and a Suspended task has been explicitly prevented from running.

I learned about the FreeRTOS scheduler, which selects which Ready task should execute based mainly on priority and scheduling rules. I also studied preemptive scheduling, where a higher-priority task can take the CPU from a lower-priority task when it becomes Ready. I learned that a high-priority task that never blocks can cause lower-priority tasks to suffer from starvation.

I studied context switching and connected it with the Cortex-M3 hardware learned earlier. When FreeRTOS switches from one task to another, the execution state of the current task must be preserved and the next task's state restored. This involves processor context such as registers, the Program Counter, Stack Pointer, Link Register, and processor status.

I learned that every task requires its own stack in SRAM because each task has its own local variables, function calls, saved registers, and execution state. FreeRTOS also maintains information about each task using a Task Control Block (TCB) containing scheduling information such as the task's state, priority, and stack information.

I also studied the RTOS tick and Cortex-M exceptions used by FreeRTOS. SysTick can provide periodic timing information, PendSV is commonly used for context switching, and SVC provides supervisor-call functionality. I also connected the earlier MSP and PSP concepts with RTOS task and exception execution.

I learned the difference between blocking an entire program and blocking only one RTOS task. When a task uses osDelay(), that task becomes Blocked and the scheduler can allow another task to use the CPU. This is much more efficient than wasting processor time in a busy-wait loop.

Finally, I created the basic architecture for multiple tasks, such as an LED task that toggles an LED periodically and a UART task that sends messages independently. The main concept I learned was: multiple tasks → FreeRTOS scheduler → context switching → one Cortex-M3 CPU, while each task maintains its own stack and execution context.
