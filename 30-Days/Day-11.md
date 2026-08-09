Day 11 — Interrupts, Exceptions, EXTI, and NVIC

Today I studied the interrupt and exception system of the STM32F103 and learned how the processor can immediately respond to hardware 
events without continuously checking them. I learned the difference between polling, where the CPU repeatedly checks whether an event 
has occurred, and interrupts, where hardware requests the CPU's attention only when an event happens.

I studied the NVIC (Nested Vectored Interrupt Controller) inside the Cortex-M3. The NVIC manages interrupts from peripherals such as 
GPIO, timers, USART, and ADC. It controls whether interrupts are enabled, their pending and active states, their priorities, and interrupt 
nesting. I also learned that a higher-priority interrupt can interrupt a lower-priority handler when the priority configuration allows it.

I learned about ISR (Interrupt Service Routine), which is the function executed when an interrupt occurs, and the vector table, which 
contains the information needed to locate the appropriate exception handlers. For external GPIO events, the STM32 uses the EXTI 
(External Interrupt/Event Controller). EXTI can detect signal changes such as a rising edge (LOW → HIGH) or falling edge (HIGH → LOW) and generate an interrupt request.

I also studied what happens inside the Cortex-M3 when an exception is accepted. The processor automatically saves a basic context 
containing R0–R3, R12, LR, PC, and xPSR onto the stack. The CPU then enters Handler Mode and executes the appropriate handler. After 
the handler finishes, the processor restores the required state and continues the interrupted program.

Finally, I learned about Cortex-M exceptions such as SysTick, PendSV, and SVCall. SysTick can generate periodic timing interrupts, 
while PendSV is commonly used by real-time operating systems for context switching. This connected interrupts directly to future FreeRTOS
and multithreading work, because switching between tasks requires saving one task's processor context and restoring another.

The complete interrupt path I learned was: hardware event → peripheral/EXTI → NVIC → Cortex-M3 → context saving → ISR → exception return
→ previous program continues.
