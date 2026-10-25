# Milestones

We will build the prototype using a TJA1051T/3 CAN Bus module (Adafruit 5708) and an STM32 NUCLEO-F303K8 board with an STM32F303K8 microcontroller (ARM Cortex-M4). After completing these milestones, we will design a custom board with an STM32G4-series microcontroller and a TCAN1044AV-Q1 transceiver.

1. **M0 — LED blinking and debugger**  
   We will configure the LED to blink using a timer, without `HAL_Delay`. We will consider this milestone complete when we can stop the program at a breakpoint and inspect the GPIO register.

2. **M1 — Logging**  
   We will redirect `printf` to UART (on the Nucleo board, we can use the ST-LINK virtual COM port) and create a logging module with `ERROR`, `INFO`, and `DEBUG` levels. We will consider this milestone complete when we can see logs containing the firmware version in a terminal.

3. **M2 — CAN loopback mode**  
   We will run the CAN controller in loopback mode, without a transceiver. We will calculate the bit-timing parameters for 500 kbit/s using the APB clock — prescaler, segments, and a sample point of about 87.5% — and compare them with a calculator. We will also configure the filters. We will consider this milestone complete when a transmitted frame is received in the RX interrupt.

4. **M3 — CAN on the bench**  
   We will connect the transceiver with 120 Ω termination and a second node (another STM32 board or an inexpensive USB-CAN adapter). We will measure CAN-H and CAN-L with an oscilloscope and save the capture in `docs/measurements/`. We will consider this milestone complete when the two nodes exchange frames without errors; we will also check the TEC and REC counters.

5. **M4 — Listening in a vehicle**  
   We will use silent (listen-only) mode exclusively and will not transmit anything. We will consider this milestone complete when we determine whether there is traffic on the connector and log the received frames to a file. If we detect no traffic, we will account for the fact that, in many vehicles, the connector is behind a gateway that responds only to requests.

6. **M5 — First OBD request**  
   We will send a Mode 01 request on ID `0x7DF` and receive a response from `0x7E8`. We will implement PID conversion formulas in a separate, tested module. We will consider this milestone complete when we can read engine RPM and coolant temperature.

7. **M6 — ISO-TP (ISO 15765-2)**  
   We will handle multi-frame responses with Flow Control frames, such as a VIN response (Mode 09, PID `0x02`). We will implement a state machine with unit tests and timeout handling. We will consider this milestone complete when we can read the full VIN.

8. **M7 — Native USB CDC**  
   We will expose the device as a virtual COM port and add a circular buffer. We will not block in interrupt handlers. We will consider this milestone complete when data is transmitted over native USB and UART remains available for logging.

9. **M8 — PC communication protocol**  
   We will choose a simple text/CSV format or slcan (Lawicel) to provide compatibility with SocketCAN and SavvyCAN. We will document the decision in an ADR.

10. **M9 — PC application**  
    We will create a Python script using `pyserial` to display engine RPM in a live plot.

11. **M10 — FreeRTOS (optional)**  
    If we decide to use FreeRTOS, we will split CAN, USB, and OBD handling into separate tasks and replace global variables with queues. We will do this only after the non-RTOS version is working, so we can compare the two approaches.
