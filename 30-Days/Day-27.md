Day 27 — FreeRTOS Queues and Inter-Task Communication

Today I studied FreeRTOS queues and learned how tasks can safely exchange data without directly sharing the same variables.

I learned that queues are used for message passing between tasks. Instead of one task writing to a global variable while another task reads it, the producer task can place data into a queue and the consumer task can receive that data later.

I studied the FIFO (First In, First Out) behavior of queues. The first message placed into the queue is normally the first message received. I also learned the producer-consumer pattern, where one task generates data and another task waits for and processes it.

I learned that a task can block on an empty queue using osMessageQueueGet(). While blocked, the task does not waste CPU time. When another task places a message into the queue, the blocked task becomes Ready and can be scheduled again. Similarly, a producer can block or fail when trying to send to a full queue depending on the configured timeout.

I studied how queues are created using osMessageQueueNew() and how their configuration includes the queue length and message size. I learned that queue memory is stored in SRAM, so queue size must be selected carefully because the STM32 has limited memory.

I used osMessageQueuePut() to send data and osMessageQueueGet() to receive it. I also learned that queues normally copy the message data into their own storage, which allows the producer and consumer to work with separate copies of the data.

I studied how queues can transfer not only simple integers but also structures containing several related values, such as an ADC reading, voltage, timestamp, or sensor measurement. This allows a complete and consistent data sample to be transferred between tasks.

I learned the difference between the main FreeRTOS synchronization mechanisms studied so far. A mutex protects a shared resource, a semaphore signals an event, a critical section protects a very short sensitive operation, and a queue transfers actual data between tasks.

I also studied queue-based system architecture. Instead of allowing several tasks to directly access UART, the tasks can send messages to a queue while a dedicated UART task becomes the only task that controls the UART peripheral. This reduces resource conflicts and makes the program easier to organize.

Finally, I connected queues with the scheduler. When a task waits on an empty queue, it becomes Blocked. When data arrives, it becomes Ready, and if its priority is high enough, FreeRTOS may perform a context switch and run it immediately.

The main concept I learned was that queues provide a clean and safe way to build data-processing pipelines, such as Sensor Task → Queue → Processing Task → Queue → UART Task, while FreeRTOS handles task blocking, synchronization, and scheduling automatically.
