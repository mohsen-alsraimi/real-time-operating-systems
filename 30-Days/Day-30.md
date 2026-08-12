Day 30 — Debugging, Fault Handling, Optimization, and Complete STM32 + FreeRTOS System

Today I studied how to debug, analyze, and optimize an STM32 FreeRTOS application, and connected everything learned during the previous days into one complete understanding of how the STM32 system operates from power-on to multithreaded execution.

I learned how STM32CubeIDE, ST-LINK, and SWD allow communication with the Cortex-M3 debugging hardware. Using the debugger, I can pause execution, set breakpoints, step through instructions and C code, inspect variables, watch expressions, examine CPU registers, inspect memory, and follow the call stack. This makes it possible to determine what the microcontroller is actually doing instead of relying only on LED or UART output.

I studied how debugging changes when using FreeRTOS. Instead of examining only the current function, I must consider the states of multiple tasks. A task can be Running, Ready, Blocked, or Suspended, and a task that appears not to be working may simply be blocked while waiting for a queue, semaphore, event, notification, or timeout. I learned to debug the complete data path rather than immediately assuming that the final peripheral is the problem.

I also studied HardFaults and Cortex-M fault handling. Invalid memory accesses, corrupted pointers, stack problems, and other processor faults can cause the system to enter a fault handler. Registers such as CFSR, HFSR, and BFAR, together with the Program Counter, Link Register, Stack Pointer, and call stack, can help determine what caused the failure.

Another important topic was task stack and RTOS heap management. Every FreeRTOS task requires its own stack, while tasks, queues, semaphores, mutexes, timers, and other kernel objects consume SRAM. I learned about stack overflow detection, stack high-water marks, allocation failures, and the difference between static and dynamic RTOS memory allocation. Instead of simply increasing every stack size, memory usage should be measured and adjusted according to the actual requirements of each task.

I reviewed important multithreading problems including race conditions, deadlocks, starvation, and priority inversion. I learned that volatile does not provide thread safety, mutexes are needed when appropriate for shared resources, consistent mutex acquisition order can help prevent deadlocks, and high-priority tasks must eventually block or wait so that lower-priority tasks are not starved.

I also learned that optimization in embedded systems is not only about making code execute faster. It includes CPU usage, SRAM usage, Flash usage, latency, power consumption, timing, and system reliability. Event-driven tasks should normally block instead of continuously polling, unnecessary context switching should be avoided, and hardware peripherals such as timers and DMA should perform operations that they can handle more efficiently than software.

Finally, I studied the complete STM32 startup sequence. After power and reset, the Cortex-M3 uses the vector table to obtain the initial Main Stack Pointer and the address of Reset_Handler. Startup code prepares the C environment by initializing .data and .bss, after which execution reaches main(). The HAL, clock system, GPIO, UART, ADC, DMA, timers, and other peripherals are initialized before the FreeRTOS kernel objects and tasks are created and the scheduler is started.

I connected this startup process with FreeRTOS execution. Each task has its own stack, priority, state, and Task Control Block. The scheduler chooses the highest-priority Ready task, while tasks become Blocked when waiting for delays or events. SysTick supports RTOS timing, while PendSV is used for context switching on Cortex-M. During a context switch, the execution context of one task is preserved and another task's context is restored so that each task can later continue from where it stopped.

I also connected hardware interrupts to multithreading. A hardware event such as a button press can travel through GPIO → EXTI → NVIC → Cortex-M exception handling → ISR → RTOS synchronization mechanism → task state change → scheduler → context switch → task execution. This demonstrated how physical hardware events can directly influence which software task the processor executes.

The main concept I learned on the final day was how all layers of the STM32 system work together. Flash stores the program, SRAM holds runtime data and task stacks, peripherals interact with the physical world, interrupts notify the Cortex-M3 about hardware events, DMA can transfer data without continuous CPU involvement, FreeRTOS organizes concurrent tasks, and the scheduler determines which Ready task receives CPU time.

After completing the 30-day study, I now understand STM32 programming as a complete system rather than only a collection of HAL functions. The complete path can be viewed as:

Power → Reset → Vector Table → Stack Pointer → Reset Handler → C Runtime Initialization → main() → HAL and Clock Configuration → Peripheral Initialization → FreeRTOS Initialization → Task and RTOS Object Creation → Scheduler → Tasks → Interrupts/Events → Context Switching → Application Behavior.

This final day connected the STM32F103 hardware, Cortex-M3 architecture, memory, peripherals, interrupts, DMA, debugging, FreeRTOS scheduling, synchronization, multithreading, and application software into one complete embedded-system model.
