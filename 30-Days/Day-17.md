## Day 17 — Hardware Timers and Timer Interrupts

Today I studied the **hardware timers of the STM32F103** and learned how they can generate precise timing events without requiring the CPU to manually count time.

I learned that a timer is driven by a clock and uses three important values: **PSC (Prescaler), CNT (Counter), and ARR (Auto-Reload Register)**. The prescaler divides the timer input clock, the counter increments according to the divided clock, and the auto-reload value determines when the timer period ends and restarts.

I studied the main timer formulas:

$$
f_{counter} = \frac{f_{timer}}{PSC + 1}
$$

and

$$
T = \frac{(PSC + 1)(ARR + 1)}{f_{timer}}
$$

Using these formulas, I learned how to calculate timer periods such as 1 second, 500 ms, and 100 ms. I also learned an important STM32 detail: when an APB prescaler is greater than 1, the timer clock can be twice the APB peripheral clock.

I configured **TIM2** using STM32CubeMX, enabled its interrupt in the NVIC, and started it using `HAL_TIM_Base_Start_IT()`. When the timer reaches the configured period, it generates an update event and interrupt. The interrupt passes through `TIM2_IRQHandler()` and `HAL_TIM_IRQHandler()` before reaching `HAL_TIM_PeriodElapsedCallback()`.

I used the timer callback to toggle an LED periodically without using `HAL_Delay()`. This demonstrated that the timer hardware can continue counting independently while the CPU performs other operations.

I also studied important timer registers such as **PSC, CNT, ARR, CR1, DIER, and SR**. Using the debugger, I could inspect the counter changing and observe the configured prescaler, period, interrupt-enable bits, and timer status flags.

The main concept I learned was the complete timer path: **clock → RCC/APB → timer clock → prescaler → counter → auto-reload → update event → interrupt → NVIC → Cortex-M3 → timer callback**. This showed how hardware timers provide accurate, non-blocking timing and prepare the system for more advanced real-time and FreeRTOS applications.
