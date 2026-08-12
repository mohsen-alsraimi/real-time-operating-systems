Day 16 — External Interrupt Programming

Today I studied how to use external interrupts on the STM32F103 and applied the interrupt concepts from the previous hardware lessons in
a real program.

I learned the difference between polling and interrupt-based programming. With polling, the CPU repeatedly checks the state of a GPIO pin
inside the main loop. With interrupts, the hardware notifies the CPU only when an event occurs, allowing the processor to perform other work
in the meantime.

I configured a GPIO pin as an EXTI input and learned how the EXTI (External Interrupt/Event Controller) detects rising and falling edges on
external signals. I also studied how the NVIC receives the interrupt request, manages its priority, and allows the Cortex-M3 to execute the
correct interrupt handler.

I learned how the interrupt software path works through functions such as EXTI0_IRQHandler(), HAL_GPIO_EXTI_IRQHandler(), and
HAL_GPIO_EXTI_Callback(). I used the callback to react to a button press and control an LED.

I also studied what happens inside the processor when an interrupt is accepted. The Cortex-M3 automatically saves a basic execution context,
including R0–R3, R12, LR, PC, and xPSR, onto the stack, enters Handler Mode, executes the ISR, and then restores the previous execution
state when the handler finishes.

I learned that interrupt routines should be kept short. Instead of performing large operations inside the ISR, a better design is often to
set a volatile flag and let the main program handle the larger task. I also learned about button bouncing, which can cause multiple
interrupts from a single physical press, and the need for software or hardware debouncing.

Using the debugger, I inspected the interrupt execution flow and studied EXTI registers such as IMR, RTSR, FTSR, and PR. The complete
path I learned was: button → GPIO → EXTI → NVIC → Cortex-M3 → ISR → callback → exception return → previous program continues.
