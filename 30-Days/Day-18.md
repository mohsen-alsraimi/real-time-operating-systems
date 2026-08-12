## Day 18 — PWM Programming with STM32 Timers

Today I studied **PWM (Pulse Width Modulation)** and learned how STM32 timers can generate digital waveforms automatically without requiring the CPU to continuously switch a GPIO pin HIGH and LOW.

I learned the main properties of a PWM signal: **frequency, period, and duty cycle**. The frequency determines how many PWM cycles occur each second, while the duty cycle determines the percentage of each period that the signal remains active. Changing the duty cycle can be used to control things such as **LED brightness and motor power**.

I learned how the timer components from Day 17 are used for PWM. The **PSC (Prescaler)** divides the timer clock, **CNT (Counter)** performs the counting, and **ARR (Auto-Reload Register)** determines the PWM period. I also introduced the **CCR (Capture/Compare Register)**, which determines the compare point and therefore controls the PWM duty cycle.

I studied the main PWM relationships:

$$
f_{PWM} = \frac{f_{timer}}{(PSC + 1)(ARR + 1)}
$$

and approximately:

$$
Duty\ Cycle = \frac{CCR}{ARR + 1} \times 100\%
$$

I configured a timer channel for **PWM Generation** using STM32CubeMX and learned that the timer output reaches the physical GPIO through the pin's **alternate-function hardware**. I used `HAL_TIM_PWM_Start()` to start PWM generation and `__HAL_TIM_SET_COMPARE()` to modify the duty cycle while the timer was running.

I also studied timer channels such as **CH1–CH4** and their corresponding **CCR1–CCR4** registers. I learned about other important PWM-related registers, including **CCMR**, which configures the capture/compare operating mode, and **CCER**, which controls channel output enabling and polarity.

Using the debugger, I learned how to inspect **PSC, ARR, CNT, CCR, CCMR, CCER, and CR1** and connect the CubeMX/HAL configuration to the actual timer hardware.

The main concept I learned was that the **CPU only configures and updates the timer**, while the timer hardware independently counts, compares CNT with CCR, and generates the PWM waveform on the physical pin. This allows precise and efficient waveform generation while the CPU remains available for other operations.
