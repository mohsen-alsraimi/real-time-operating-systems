## Day 20 — ADC: Analog-to-Digital Conversion

Today I studied the **ADC (Analog-to-Digital Converter)** of the STM32F103 and learned how the microcontroller can measure analog voltages and convert them into digital values that the CPU can process.

I learned the difference between **analog and digital signals**. Digital signals normally represent discrete HIGH and LOW states, while analog signals can continuously vary across a voltage range. Sensors for temperature, light, pressure, sound, and other physical quantities often produce analog voltages, so the ADC provides the connection between these real-world signals and software.

The STM32F103 uses a **12-bit ADC**, which provides $2^{12} = 4096$ possible values, represented from **0 to 4095**. I learned that the ADC measures the input relative to its reference voltage. Assuming a 3.3 V reference, approximately 0 V corresponds to 0, 1.65 V corresponds to about 2048, and 3.3 V corresponds to about 4095.

I learned how to convert the raw ADC result back into an estimated voltage using:

$$
V_{in} = \frac{ADC_{value}}{4095} \times V_{REF}
$$

I also studied **sampling and quantization**. Sampling means measuring the analog voltage at particular moments, while quantization converts each sampled voltage into one of the available digital levels. I learned about the ADC's internal **sample-and-hold** process and why sampling time is important, especially when the analog source has higher impedance.

I configured **ADC1 and an ADC channel** using STM32CubeMX and learned that the associated GPIO pin must be configured in **analog mode**. I studied ADC calibration and used `HAL_ADC_Start()`, `HAL_ADC_PollForConversion()`, and `HAL_ADC_GetValue()` to perform a conversion and retrieve its result.

I used a **potentiometer** as a variable analog input and observed how changing its voltage changes the ADC reading between approximately 0 and 4095. I also converted the ADC reading into millivolts and studied how several measurements can be averaged to reduce random fluctuations and noise.

I combined the ADC with peripherals studied previously. ADC measurements can be transmitted to a computer through **UART**, used as thresholds to control GPIO outputs, or mapped to a timer's **PWM duty cycle**, allowing a potentiometer to control LED brightness.

I also studied important ADC registers including **SR, CR1, CR2, SMPR1/SMPR2, SQR1–SQR3, and DR**. The **DR (Data Register)** contains the conversion result, the status register reports events such as **EOC (End of Conversion)**, the sampling registers configure sampling time, and the sequence registers determine which ADC channels are converted and in what order.

Finally, I compared **polling and interrupt-based ADC operation**. With polling, the CPU waits for the conversion to complete, while interrupt mode allows the ADC to notify the CPU when the result is ready.

The main system I learned was: **analog signal → analog GPIO pin → ADC channel → sampling → conversion → ADC data register → CPU/SRAM → application**, after which the measurement can be processed, transmitted through UART, or used to control other peripherals such as PWM.
