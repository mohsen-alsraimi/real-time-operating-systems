Day 10 — GPIO Hardware Architecture

Today I studied the GPIO (General-Purpose Input/Output) hardware architecture of the STM32F103 and learned how the microcontroller 
communicates with external components through its physical pins. GPIO pins are organized into ports such as GPIOA, GPIOB, and GPIOC, 
with individual pins identified as PA0, PA1, PB0, PC13, and so on.

I learned that a GPIO pin can operate as either an input or output. In input mode, the STM32 reads electrical signals from external 
devices such as buttons and sensors. In output mode, the STM32 generates digital HIGH or LOW signals to control components such as LEDs. 
A floating input can produce unpredictable values, so pull-up and pull-down resistors are used to keep the input at a defined logic level 
when no external signal is driving it.

I studied the two important output configurations: push-pull and open-drain. Push-pull can actively drive a pin both HIGH and LOW and is 
commonly used for normal digital outputs. Open-drain can actively pull the line LOW but releases it for the HIGH state, usually requiring 
a pull-up resistor. This configuration is important for shared communication buses such as I²C.

I also learned how GPIO is controlled through memory-mapped hardware registers. In the STM32F1, CRL and CRH configure the operating
modes of the pins, IDR provides the input states, ODR controls output data, and BSRR allows individual output bits to be set or reset 
efficiently. Before using a GPIO port, its required peripheral clock must also be enabled through the RCC.

Another important concept was alternate functions. A physical GPIO pin can be connected internally to peripherals such as USART, 
SPI, or timers instead of being used as an ordinary digital input/output. This allows dedicated hardware peripherals to directly 
generate or receive signals through physical pins.

Finally, I connected GPIO with the previous topics and understood the complete path from software to physical hardware: 
C code → Cortex-M3 CPU → internal bus → memory-mapped GPIO register → GPIO output circuitry → physical pin → external device. 
This showed how software instructions running inside the processor can directly control electrical signals in the real world.
