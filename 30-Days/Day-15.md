Day 15 — GPIO Programming

Today I practiced controlling the STM32F103 GPIO using both the HAL library and direct register access. I learned how the GPIO theory from
the previous hardware days is applied in a real STM32CubeIDE project.

I configured a GPIO pin as an output and used it to control an LED. I learned how CubeMX generates the GPIO initialization code and how
MX_GPIO_Init() enables the GPIO peripheral clock through the RCC and configures the pin mode, output type, speed, and initial state.

I used HAL functions such as HAL_GPIO_WritePin(), HAL_GPIO_TogglePin(), and HAL_GPIO_ReadPin() to control output pins and read input pins.
I also learned that some LEDs are active-low, meaning a LOW output can turn the LED on while a HIGH output turns it off.

I configured a GPIO pin as an input and studied how a push button can be read using polling. I also reviewed the use of pull-up and
pull-down resistors to prevent floating input values and learned about mechanical button bouncing and why debouncing may be required.

I then studied the GPIO hardware registers directly. In STM32F1, CRL and CRH configure the pins, IDR contains input states, ODR contains
output data, and BSRR allows individual output bits to be set or reset efficiently. I practiced using bit masks and bitwise operations
such as shifting, OR, AND, and XOR to manipulate individual GPIO bits.

Using the STM32CubeIDE debugger, I connected the software with the hardware by inspecting GPIO registers while the program was running.
This helped me understand the complete path from
C code → HAL or register operation → internal bus → GPIO register → GPIO hardware → physical pin → LED or button.

The main result of Day 15 was understanding that HAL provides a convenient abstraction, but the actual control of the GPIO still happens
through memory-mapped hardware registers inside the STM32.
