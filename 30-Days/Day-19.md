Day 19 — UART/USART Serial Communication

Today I studied UART/USART serial communication and learned how the STM32F103 can communicate with external devices such as a computer, another microcontroller, or serial modules.

I learned that UART (Universal Asynchronous Receiver/Transmitter) sends data serially, one bit after another, using TX (Transmit) and RX (Receive) lines. STM32 uses USART peripherals, which can support both synchronous and asynchronous communication. For normal UART communication, the devices use TX, RX, and a common GND, with the TX of one device connected to the RX of the other.

I studied the baud rate and learned that both communicating devices must use compatible communication settings. I used a typical configuration of 115200 baud, 8 data bits, no parity, and 1 stop bit (8-N-1). I also learned how UART creates a frame containing a start bit, data bits, optional parity, and stop bit.

I configured USART1 in asynchronous mode using STM32CubeMX and studied how the USART peripheral connects to the physical TX and RX pins through the GPIO alternate-function system. I learned that the USART clock comes from the RCC/APB clock system and is divided internally to generate the required baud timing.

I used HAL_UART_Transmit() to send text from the STM32 to a computer and HAL_UART_Receive() to receive data. I also studied a simple echo program, where the STM32 receives a character and immediately sends it back. I used received characters such as '1' and '0' to control an LED from a serial terminal.

I then studied interrupt-based UART reception using HAL_UART_Receive_IT(). When data arrives, the USART can generate an interrupt through the NVIC, which eventually calls HAL_UART_RxCpltCallback(). This allows the CPU to continue executing other code instead of blocking while waiting for incoming data.

I also studied important USART registers, including SR (Status Register), DR (Data Register), BRR (Baud Rate Register), and CR1–CR3 (Control Registers). Important status flags included RXNE for received data being available, TXE for the transmit data register being ready, and TC for transmission completion.

Finally, I learned about receive buffers and why they are necessary when multiple bytes arrive faster than the application can process them. The complete communication path I studied was: application data → memory buffer → HAL → USART peripheral → serial frame → TX pin → external device, with the reverse process occurring for received data.

This also showed how UART can be used as a practical debugging and monitoring interface, which will later be useful for observing and communicating with multiple FreeRTOS tasks.
