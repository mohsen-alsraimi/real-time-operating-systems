Day 28 — Task Notifications, Event Flags, Software Timers, and Event-Driven Design

Today I studied event-driven programming in FreeRTOS and learned how tasks can remain blocked until an event actually requires their attention, instead of repeatedly polling hardware or shared variables.

I learned about task notifications, which provide a lightweight way for one task or an interrupt to directly signal a specific task. Notifications can be used as simple signals, counters, or bit values, making them useful for events such as DMA completion, UART reception, or sensor-ready signals.

I also studied event flags, where individual bits represent different system events. For example, one bit can represent a button event, another an ADC-ready event, and another a UART event. A task can wait for any of several events or wait until all required events have occurred.

I learned how event flags can be used for synchronization between tasks. For example, a control task can remain blocked until several initialization tasks set their corresponding READY bits, allowing the system to begin operation only after all required components are initialized.

I then studied FreeRTOS software timers and learned the difference between software timers and STM32 hardware timers. Hardware timers such as TIM2 provide precise hardware timing, PWM, capture, and interrupts, while software timers are managed by the RTOS and are better suited for application-level timing such as communication timeouts, inactivity detection, delayed actions, and periodic status operations.

I learned the difference between one-shot and periodic software timers. A one-shot timer executes once after a configured delay, while a periodic timer automatically repeats. I also learned that software timer callbacks run through the FreeRTOS timer service mechanism and should remain short so they do not delay other timer callbacks.

I studied how timers can signal tasks instead of performing large operations directly inside their callbacks. A timer callback can set an event flag, send a message, or notify a worker task, while the task performs the larger processing.

I also connected software timers with button debouncing. A button interrupt can start or restart a short one-shot timer, and after the bouncing period finishes, a task can verify the stable GPIO state before processing the button press.

Finally, I learned how to choose between different FreeRTOS mechanisms: mutexes protect shared resources, queues transfer data, semaphores synchronize events, task notifications provide lightweight one-to-one signaling, event flags represent multiple event conditions, and software timers schedule delayed or periodic software actions.

The main concept I learned was that a well-designed RTOS system should be event-driven: tasks normally remain Blocked when they have nothing to do, become Ready when an event, message, notification, or timeout occurs, perform their work, and then block again. This allows the CPU and scheduler to operate much more efficiently than continuously polling every possible event.
