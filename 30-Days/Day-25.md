Day 25 — FreeRTOS Tasks, Scheduling, and Context Switching

Today I studied FreeRTOS task management and scheduling in more detail and learned how multiple tasks share the single Cortex-M3 CPU.

I learned that a task is more than just a function. Each task has its own task function, stack, priority, state, saved execution context, and Task Control Block (TCB). The TCB stores information the scheduler needs, such as the task priority, current state, and stack information.

I studied task creation and task attributes, including the task name, stack size, and priority. I also learned about task handles, which provide a way to identify and control specific tasks using RTOS functions.

I learned why every task needs its own stack in SRAM. The stack stores local variables, function-call information, return addresses, and saved CPU context. I also studied stack overflow, which can occur if a task uses more stack memory than was allocated and can lead to memory corruption or system crashes.

I studied the FreeRTOS scheduling rule that the CPU normally executes the highest-priority task that is currently Ready. A higher-priority task does not run while it is Blocked, so lower-priority tasks can execute during that time.

I learned more about preemptive scheduling. If a higher-priority task becomes Ready while a lower-priority task is running, FreeRTOS can perform a context switch and immediately give the CPU to the higher-priority task.

I also studied time slicing, where multiple Ready tasks with the same priority can share CPU time. This is different from priority-based preemption because equal-priority tasks can take turns using the processor.

I learned about starvation, which can happen when a high-priority task remains Ready continuously and prevents lower-priority tasks from receiving CPU time. This showed why well-designed tasks should normally perform their work and then block or wait when they have nothing useful to do.

I compared osDelay() with periodic scheduling using osDelayUntil(). osDelay() waits for a relative amount of time after the current work finishes, which can introduce timing drift. osDelayUntil() is better for tasks that need to execute at regular periods because it follows an absolute timing schedule.

I also studied task state control using suspend and resume operations. A suspended task is removed from normal scheduling until it is explicitly resumed, while a Blocked task automatically becomes Ready when its delay or waiting condition finishes.

Finally, I connected task scheduling with the Cortex-M3 hardware. During a context switch, the execution state of one task is saved and another task's state is restored. FreeRTOS commonly uses PendSV for this process, allowing the CPU to change from one task stack and execution context to another.

The main concept I learned was that FreeRTOS continuously asks: which Ready task has the highest priority? The selected task receives the Cortex-M3 CPU, while blocked or suspended tasks do not consume normal CPU execution time.
