# ARDUINO SERIAL FUNCTIONS

## Structured Function Manual

Every function uses the same structure: Topic • Purpose / Explain • Syntax • Return value • Example code

For Arduino IDE learners and embedded firmware developers. The final section contains one commented ESP32 demonstration sketch.

Compatibility note: exact methods and overloads depend on the selected board package. ESP32-specific functions are marked clearly.

## 1. Setup and configuration

## 1.1 Serial.begin()

**Topic:** Initialize communication  
**Purpose / Explain:** Starts serial communication at the selected baud rate. On ESP32, extra overloads can configure UART format and pins.  
**Syntax:** `Serial.begin(baud);`  
**Return value:** `void` — no value.  

### Example code

```c
void setup() {
Serial.begin(115200);    // Start Serial at 115200 baud
Serial.println("Ready"); // Print startup message
}
void loop() {}
```

**Note:** Match the Serial Monitor baud rate.

## 1.2 Serial.end()

**Topic:** Stop communication  
**Purpose / Explain:** Stops the serial interface where supported by the core.  
**Syntax:** `Serial.end();`  
**Return value:** `void` — no value.  

### Example code

```c
Serial.println("Stopping...");
Serial.flush(); // Finish outgoing data
Serial.end();   // Stop Serial
```

**Note:** Reset/reinitialize the board/interface to resume.

## 1.3 Serial.setTimeout()

**Topic:** Configure timeout  
**Purpose / Explain:** Sets the timeout used by Stream reads and parsing functions; it is not a global program timeout.  
**Syntax:** `Serial.setTimeout(milliseconds);`  
**Return value:** `void` — no value.  

### Example code

```c
Serial.setTimeout(750);         // Use a 750 ms Stream timeout
long value = Serial.parseInt(); // May wait for input
```

## 1.4 Serial.getTimeout()

**Topic:** Read timeout setting  
**Purpose / Explain:** Returns the current timeout used by applicable Stream methods.  
**Syntax:** `unsigned long ms = Serial.getTimeout();`  
**Return value:** `unsigned long` — milliseconds.  

### Example code
```c
unsigned long ms = Serial.getTimeout();
Serial.print("Timeout:");
Serial.println(ms);
```

**Note:** The common default is 1000 ms, but check the selected core.

**Reference:** Arduino Stream reference [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/stream/)

## 2. Output and transmission

## 2.1 Serial.print()

**Topic:** Readable output  
**Purpose / Explain:** Prints text or values without adding a newline.  
**Syntax:** `Serial.print(value); / Serial.print(value, base);`  
**Return value:** `size_t` — number of bytes written on common implementations.  

### Example code
```c
int voltage = 27;
Serial.print("Voltage = "); // Print label
Serial.print(voltage);      // Print 27
Serial.print(" V");         // Continue same line
Serial.println();           // Then move to next line
```

**Note:** Integer bases include DEC, HEX, BIN, and OCT.  
**Reference:** Serial.print() [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/serial/print/)

## 2.2 Serial.println()

**Topic:** Readable output with line ending  
**Purpose / Explain:** Prints a value and appends a line ending.  
**Syntax:** `Serial.println(value);`  
**Return value:** `size_t` — number of bytes written on common implementations.  

### Example code
```c
Serial.println("System Ready");
Serial.println(123);            // Output is on two separate lines
```

**Reference:** Serial.println() [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/serial/println/)

## 2.3 Serial.write()

**Topic:** Raw byte transmission  
**Purpose / Explain:** Sends raw bytes without converting numeric values to readable decimal text.  
**Syntax:** `Serial.write(byte);` `Serial.write(buffer, length);`  
**Return value:** `size_t` — number of bytes written.  

### Example code
```c
Serial.print(65); // Sends text '65'
Serial.write(65); // Sends one byte 0x41, ASCII 'A'
```

**Reference:** Serial.write() [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/serial/write/)

## 2.4 Serial.printf() [ESP32]

**Topic:** Formatted output  
**Purpose / Explain:** Uses printf-style format specifiers. This is an ESP32 Arduino-core extension, not portable to every board.  
**Syntax:** `Serial.printf("format", arguments...);`  
**Return value:** Usually `size_t;` verify the installed core.  

### Example code
```c
int voltage = 27;
float current = 2.5f;
Serial.printf("Voltage=%d V, Current=%.2f A\n", voltage, current);  //Output: Voltage=27 V, Current=2.50 A
```

**Note:** Common specifiers: %d integer, %s string, %x hex, %.2f float to 2 decimals.

## 2.5 Serial.availableForWrite()

**Topic:** TX buffer status  
**Purpose / Explain:** Checks how many bytes can be written without waiting, where supported.  
**Syntax:** `int freeBytes = Serial.availableForWrite();`  
**Return value:** `int` — available transmit-buffer space in bytes.  

### Example code
```c
int freeBytes = Serial.availableForWrite();
if (freeBytes > 0) {
Serial.write('A');    // Write if space is available
}
```

## 2.6 Serial.flush()

**Topic:** Wait for transmission  
**Purpose / Explain:** Waits for outgoing serial data to finish transmitting under standard Arduino semantics.  
**Syntax:** `Serial.flush();`  
**Return value:** `void` — no value.  

### Example code
```c
Serial.println("Saving...");
Serial.flush(); // Wait for queued output to transmit
```

**Note:** Do not assume this clears RX data. ESP32 has additional documented overloads.  
**Reference for ESP32 extensions:** ESP32 Serial API [URL 🔗](https://docs.espressif.com/projects/arduino-esp32/en/latest/api/serial.html)

## 3. Receive buffer

## 3.1 Serial.available()

**Topic:** Receive buffer status  
**Purpose / Explain:** Counts bytes waiting to be read; it does not consume them.  
**Syntax:** `int count = Serial.available();`  
**Return value:** `int` — number of bytes available.  

### Example code
```c
if (Serial.available() > 0) { // Any bytes waiting?
int b = Serial.read(); // Read one byte
Serial.println(b); // Print numeric byte value
}
```

**Note:** If ABC are buffered, the count may be 3; after reading one byte, it may be 2.  
**Reference:** Serial.available() [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/serial/available/)

## 3.2 Serial.read()

**Topic:** Read one byte  
**Purpose / Explain:** Consumes one byte from the receive buffer.  
**Syntax:** `int data = Serial.read();`  
**Return value:** `int` — 0 to 255, or -1 if no byte is available.  

### Example code
```c
if (Serial.available() > 0) {
int data = Serial.read();
Serial.print("Received: ");
Serial.println(data);
}
```

## 3.3 Serial.peek()

**Topic:** Inspect next byte  
**Purpose / Explain:** Returns the next byte without removing it from the receive buffer.  
**Syntax:** `int data = Serial.peek();`  
**Return value:** `int` — 0 to 255, or -1 if no byte is available.  

### Example code
```c
if (Serial.available() > 0) {
int next = Serial.peek(); // Inspect only
Serial.println(next);
// Byte remains in the buffer
}
```

## 4. Read buffers and strings

## 4.1 Serial.readBytes()

**Topic:** Read a block of bytes  
**Purpose / Explain:** Reads up to the requested length; can wait for data or timeout and may return fewer bytes than requested.  
**Syntax:** `size_t n = Serial.readBytes(buffer, length);`  
**Return value:** `size_t` — actual bytes read.  

### Example code
```c
char buffer[8];
size_t n = Serial.readBytes(buffer, sizeof(buffer));
// Process only buffer[0] through buffer[n - 1].
// No '\0' terminator is added automatically.
```

## 4.2 Serial.readBytesUntil()

**Topic:** Read until a delimiter  
**Purpose / Explain:** Reads until delimiter, buffer limit, or timeout. Delimiter is consumed but not stored.  
**Syntax:** `size_t n = Serial.readBytesUntil(terminator, buffer, length);`  
**Return value:** `size_t` — bytes stored, excluding delimiter.  

### Example code
```c
char line[32];
size_t n = Serial.readBytesUntil('\n', line, sizeof(line) - 1);
line[n] = '\0'; // Terminate as C string
Serial.println(line);
```

## 4.3 Serial.readString()

**Topic:** Read into String  
**Purpose / Explain:** Collects received characters into a String until the Stream timeout ends the operation.  
**Syntax:** `String text = Serial.readString();`  
**Return value:** `String` — collected text.  

### Example code
```c
String text = Serial.readString();
Serial.print("Received: ");
Serial.println(text);
```

**Note:** Can block while waiting; use carefully in real-time firmware.

## 4.4 Serial.readStringUntil()

**Topic:** Read String to delimiter  
**Purpose / Explain:** Collects characters until delimiter or timeout. Delimiter is not included.  
**Syntax:** `String text = Serial.readStringUntil(terminator);`  
**Return value:** `String` — collected text.  

### Example code
```c
String command = Serial.readStringUntil('\n');
Serial.print("Command: ");
Serial.println(command);
```

**Reference:** Arduino Stream reference [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/stream/)

## 5. Parsing and searching

## 5.1 Serial.parseInt()

**Topic:** Parse integer  
**Purpose / Explain:** Skips non-numeric characters and parses an integer; may wait until a number or timeout.  
**Syntax:** `long value = Serial.parseInt();`  
**Return value:** `long` — parsed integer; zero can also indicate no valid non-zero number was parsed.  

### Example code
```c
Serial.println("Send an integer, e.g. -123:");
long value = Serial.parseInt();
Serial.println(value);
```

## 5.2 Serial.parseFloat()

**Topic:** Parse decimal number  
**Purpose / Explain:** Parses a floating-point value from received text; may wait according to timeout.  
**Syntax:** `float value = Serial.parseFloat();`  
**Return value:** `float` — parsed value; zero may also mean no valid number was parsed.  

### Example code
```c
Serial.println("Send 27.125:");
float value = Serial.parseFloat();
Serial.println(value, 3); // Print 3 decimal places
```

## 5.3 Serial.find()

**Topic:** Search received stream  
**Purpose / Explain:** Consumes incoming data while searching for the target sequence.  
**Syntax:** `bool found = Serial.find(target);`  
**Return value:** `bool` — true if found before timeout; otherwise false.  

### Example code
```c
Serial.println("Send a stream containing START:");
bool found = Serial.find("START");
Serial.println(found ? "Found" : "Not found");
```

## 5.4 Serial.findUntil()

**Topic:** Search with stop sequence  
**Purpose / Explain:** Searches for a target, stopping if a terminator is found first or timeout occurs.  
**Syntax:** `bool found = Serial.findUntil(target, terminator);`  
**Return value:** `bool` — true if target is found before stop/timeout; otherwise false.  

### Example code
```c
Serial.println("Send OK or ERROR:");
bool found = Serial.findUntil("OK", "ERROR");
Serial.println(found ? "OK found" : "OK not found");
```

**Reference:** Arduino Stream reference [URL 🔗](https://docs.arduino.cc/language-reference/en/functions/communication/stream/)

## 6. ESP32-specific UART extensions

These methods are core-version-dependent. Check the official ESP32 API for exact signatures and supported hardware.

## 6.1 setPins()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Assign RX/TX GPIO pins.  
**Syntax:** `Serial1.setPins(rxPin, txPin);`  
**Return value:** `bool` on common versions; verify core.  

### Example code

```c
Serial1.setPins(16, 17); // RX=16, TX=17 example pins
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.2 updateBaudRate()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Change baud rate after initialization.  
**Syntax:** `Serial1.updateBaudRate(baud);`  
**Return value:** `void` on common versions.  

### Example code
```c
Serial1.updateBaudRate(19200);
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.3 baudRate()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Read configured baud rate.  
**Syntax:** `uint32_t rate = Serial1.baudRate();`  
**Return value:** `uint32_t` — baud rate.  

### Example code
```c
uint32_t rate = Serial1.baudRate();
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.4 setRxBufferSize()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure RX buffer; normally before begin().  
**Syntax:** `Serial1.setRxBufferSize(size);`  
**Return value:** `Return type/core behavior varies`.  

### Example code
```c
Serial1.setRxBufferSize(1024);
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.5 setTxBufferSize()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure TX buffer where supported.  
**Syntax:** `Serial1.setTxBufferSize(size);`  
**Return value:** `Return type/core behavior varies`.  

### Example code
```c
Serial1.setTxBufferSize(512); // Check support first
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.6 setRxFIFOFull()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure RX FIFO threshold where supported.  
**Syntax:** `Serial1.setRxFIFOFull(bytes);`  
**Return value:** Core-specific; check API.  

### Example code
```c
Serial1.setRxFIFOFull(10); // Example only
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.7 setRxTimeout()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure UART RX inactivity timeout in symbols.  
**Syntax:** `Serial1.setRxTimeout(symbols);`  
**Return value:** Core-specific; check API.  

### Example code
```c
Serial1.setRxTimeout(3); // Example only
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.8 onReceive()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Register a receive callback.  
**Syntax:** `Serial1.onReceive(callback);`  
**Return value:** `void` — registers callback.  

### Example code
```c
void onData() { /*Keep callback short*/ }
Serial1.onReceive(onData); // Exact use depends on core
```
**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.9 onReceiveError()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Register UART error callback.  
**Syntax:** `Serial1.onReceiveError(callback);`  
**Return value:** Core-specific callback type.  

### Example code
```c
// Register a callback matching the installed core API.
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.10 setMode()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure supported UART mode.  
**Syntax:** `Serial1.setMode(mode);`  
**Return value:** Core-specific return type/constants.  

### Example code
```c
// Use only documented mode constants for your core.
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.11 setHwFlowCtrlMode()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Configure RTS/CTS flow control.  
**Syntax:** `Serial1.setHwFlowCtrlMode(mode);`  
**Return value:** Core-specific return type/constants.  

### Example code
```c
// Requires compatible device and RTS/CTS wiring.
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

## 6.12 setRS485Mode()

**Topic:** ESP32 UART configuration  
**Purpose / Explain:** Enable supported RS-485 mode.  
**Syntax:** `Serial1.setRS485Mode(enabled);`  
**Return value:** Core/chip dependent.  

### Example code
```c
Serial1.setRS485Mode(true); // Only if supported
```

**Note:** ESP32-only/implementation-dependent. Verify the installed core's documentation.

Official manual: ESP32 Arduino Serial API [URL 🔗](https://docs.espressif.com/projects/arduino-esp32/en/latest/api/serial.html)

## 7. Blocking behavior and best practices

| Function(s) | Typical behavior | Advice |
| --- | --- | --- |
| available(), read(), peek() | Normally quick when polling | Check availability; handle -1. |
| print(), println(), write() | May wait if TX buffer fills | Limit debug output in time-critical loops. |
| flush() | Waits for outgoing transmission | Use when needed only. |
| readBytes(), | Can wait for data/delimiter or timeout | Check returned byte count. |
| readBytesUntil() | | |
| readString(), parseInt(), | May wait for data/timeout | Avoid in strict real-time loops. |
| parseFloat() | | |
| find(), findUntil() | Consume data and may wait | Use only with known message framing. |

- Match Serial Monitor baud rate with Serial.begin().

- print(65) sends text '65'; write(65) sends one byte 0x41.

- Use returned byte counts and never assume readBytes() fills the whole buffer.

- Reserve space for '\0' when converting bytes into a C string.

- Use explicit framing, length checks, and input validation in production protocols.

- UART logic voltage levels must be compatible; protect 3.3 V-only inputs from 5 V signals.

## 8. Complete commented example sketch

Target: ESP32 Arduino framework. Serial Monitor: 115200 baud, line ending = Newline. Type help, then one command at a time. Commands that request more data should be followed by the data after the prompt appears.

```c
/*
ARDUINO SERIAL FUNCTION DEMO
ESP32 Arduino core: Serial.printf() is ESP32-specific.
Serial Monitor: 115200 baud, Newline ending.
Commands: help, info, peek, read, write, int, float, line, until, bytes, find, finduntil, timeout, flush, printf, end
Teaching note: several methods below can block while waiting for input. Use non-blocking state machines in time-critical firmware.
*/
String getCommand(){
    // Read command characters until newline or Stream timeout.
    String cmd = Serial.readStringUntil('\n');
    cmd.trim(); // Remove surrounding whitespace/CR
    return cmd;
}
void showHelp(){
    Serial.println("Commands: help info peek read write int float line");
    Serial.println(" until bytes find finduntil timeout flush printf end");
}
void setup(){
    Serial.begin(115200); // Initialize Serial at 115200 baud
    Serial.setTimeout(1500); // Timeout for Stream read/parse methods
    delay(300); // Short delay for some USB serial setups
    Serial.println("Serial demo ready.");
    Serial.print("Timeout = ");
    Serial.print(Serial.getTimeout());
    Serial.println(" ms");
    showHelp();
}
void loop(){
    // available() counts bytes in the RX buffer; it does not read them.
    if (Serial.available() <= 0) return;

    String cmd = getCommand();
    if (cmd == "help") {
        showHelp();
    }
    else if (cmd == "info") {
        // getTimeout() reports Stream timeout; availableForWrite() checks TX space.
        Serial.print("Timeout ms: ");
        Serial.println(Serial.getTimeout());
        Serial.print("TX bytes available: ");
        Serial.println(Serial.availableForWrite());
        Serial.print("print() example: ");
        Serial.println("println() adds a line ending.");
    }
    else if (cmd == "peek") {
        Serial.println("Send one character now.");
        while (Serial.available() == 0) { } // Demo-only blocking wait

        int b = Serial.peek(); // Inspect next byte without consuming
        Serial.print("peek() value: ");
        Serial.println(b);
        Serial.println("The byte remains in the RX buffer.");
    }
    else if (cmd == "read") {
        Serial.println("Send one character now.");
        while (Serial.available() == 0) { } // Demo-only blocking wait

        int b = Serial.read(); // Consume one byte
        Serial.print("read() decimal: ");
        Serial.println(b);
        Serial.print("read() character: ");
        Serial.println((char)b);
    }
    else if (cmd == "write") {
        Serial.print("print(65) sends text: ");
        Serial.println(65);
        Serial.print("write(65) sends raw byte: ");
        Serial.write(65); // One byte 0x41 = ASCII 'A'
        Serial.println();
    }
    else if (cmd == "int") {
        Serial.println("Send an integer such as -123.");
        long value = Serial.parseInt(); // Parse integer; may wait until timeout
        Serial.print("Parsed integer: ");
        Serial.println(value);
    }
    else if (cmd == "float") {
        Serial.println("Send a decimal such as 27.125.");
        float value = Serial.parseFloat(); // Parse float; may wait until timeout
        Serial.println(value, 3); // Print 3 decimal places
    }
    else if (cmd == "line") {
        Serial.println("Send a line of text.");
        String line = Serial.readStringUntil('\n'); // Read until newline
        Serial.print("Line: ");
        Serial.println(line);
    }
    else if (cmd == "until") {
        char buffer[40];
        Serial.println("Send text ending in !, e.g. HELLO!");
        // Delimiter is consumed, not stored; may stop at timeout or buffer limit.
        size_t n = Serial.readBytesUntil('!', buffer, sizeof(buffer) - 1);
        buffer[n] = '\0'; // Safely terminate C string
        Serial.print("Bytes read: ");
        Serial.println(n);
        Serial.println(buffer);
    }
    else if (cmd == "bytes") {
        char buffer[4];
        Serial.println("Send four characters, e.g. ABCD.");
        // Reads up to four bytes; timeout may produce a shorter count.
        size_t n = Serial.readBytes(buffer, sizeof(buffer));
        Serial.print("Count: ");
        Serial.println(n);
        Serial.print("HEX: ");
        for (size_t i = 0; i < n; ++i) {
            Serial.print((uint8_t)buffer[i], HEX);
            Serial.print(' ');
        }
        Serial.println();
    }
    else if (cmd == "find") {
        Serial.println("Send data containing START.");
        // find() consumes incoming bytes while searching.
        bool found = Serial.find("START");
        Serial.println(found ? "START found" : "START not found");
    }
    else if (cmd == "finduntil") {
        Serial.println("Send data containing OK or ERROR.");
        // True if OK is found before ERROR/timeout.
        bool found = Serial.findUntil("OK", "ERROR");
        Serial.println(found ? "OK found" : "OK not found before stop/timeout");
    }
    else if (cmd == "timeout") {
        Serial.setTimeout(750); // Set Stream timeout to 750 ms
        Serial.print("New timeout: ");
        Serial.println(Serial.getTimeout());
    }
    else if (cmd == "flush") {
        Serial.println("Waiting for outgoing bytes...");
        Serial.flush(); // Wait for TX data to finish
        Serial.println("flush() returned.");
    }
    else if (cmd == "printf") {
        int voltage = 27;
        float current = 2.5f;
        // printf formatting is an ESP32 Arduino-core extension.
        Serial.printf("Voltage=%d V, Current=%.2f A\n", voltage, current);
    }
    else if (cmd == "end") {
        Serial.println("Stopping Serial. Reset board to restart.");
        Serial.flush(); // Finish final outgoing message
        Serial.end(); // Stop Serial interface
        while (true) { delay(1000); } // Wait until reset
    }
    else if (cmd.length() > 0) {
        Serial.print("Unknown command: ");
        Serial.println(cmd);
        Serial.println("Type help.");
    } // print()/println() produce readable text; write() transmits raw bytes.
}
```

Test procedure: choose the correct ESP32 board and port, upload the sketch, open Serial Monitor at 115200 baud with Newline selected, type help, and test commands individually.

## 9. Official references

- [• Arduino Language Reference](https://docs.arduino.cc/language-reference/)

- [• Serial.begin()](https://docs.arduino.cc/language-reference/en/functions/communication/serial/begin/)

- [• Serial.print()](https://docs.arduino.cc/language-reference/en/functions/communication/serial/print/)

- [• Serial.println()](https://docs.arduino.cc/language-reference/en/functions/communication/serial/println/)

- [• Serial.write()](https://docs.arduino.cc/language-reference/en/functions/communication/serial/write/)

- [• Serial.available()](https://docs.arduino.cc/language-reference/en/functions/communication/serial/available/)

- [• Arduino Stream reference](https://docs.arduino.cc/language-reference/en/functions/communication/stream/)

- [• ESP32 Arduino Serial API](https://docs.espressif.com/projects/arduino-esp32/en/latest/api/serial.html)
