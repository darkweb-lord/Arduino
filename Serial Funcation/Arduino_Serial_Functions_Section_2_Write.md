# Arduino Serial Functions

## Section 2 — Write / Short-Response Questions

**Total:** 150 questions — Beginner (50), Intermediate (50), Advanced (50).

Questions are numbered continuously from 1 to 150. Answers are not included.

### Beginner Level

1. Write setup() code to start Serial at 115200 baud.
2. Write code that prints “System ready” followed by a line ending.
3. Print 12 and 34 on the same line with no separator.
4. Print A, B and C on separate lines.
5. Read one byte only if input is available.
6. Read one incoming byte into an int named incoming and print its numeric value.
7. Use peek() to inspect the next received byte without consuming it.
8. Wait for outgoing serial data to finish transmitting.
9. Set the Stream timeout to 250 milliseconds.
10. Read up to 6 bytes into an array named data and store the actual count returned.
11. Use readBytesUntil() to read up to 20 characters or until newline; store the returned count.
12. Read one text field until a comma using readStringUntil().
13. Use readString() to collect incoming text and then print it.
14. Parse an integer command into commandValue and print it.
15. Parse a floating-point sensor reading and print it with two decimal places.
16. Use find() to wait for READY and report whether it was found.
17. Use findUntil() to search for DATA but stop if ! appears first.
18. Show if (Serial) before printing a startup message on a compatible native-USB board.
19. End serial communication and then begin it again.
20. Use write() to send bytes 0x41, 0x42 and 0x43 from an array.
21. Explain print() versus write() with a short example.
22. Explain what available() measures and why it is useful.
23. Explain how availableForWrite() differs from available().
24. Explain the difference between read() and peek().
25. Explain modern flush() behavior and how it differs from clearing input.
26. Explain how setTimeout() affects readBytes() and parsing methods.
27. Describe one use and one limitation of readBytesUntil().
28. Explain the difference between find() and findUntil().
29. Explain what parseInt() does when the stream contains non-numeric characters.
30. Explain what parseFloat() is intended to extract from a serial stream.
31. Explain if (Serial) on a native-USB board and why behavior may vary by board.
32. Describe serialEvent() on cores that support it and one limitation.
33. Write ESP32 code to start Serial2 at 9600 baud using RX_PIN and TX_PIN placeholders.
34. Write an ESP32 snippet that prints Serial.availableForWrite().
35. Send PING over ESP32 Serial2 once per second.
36. Create a line-based command reader that stops at newline and rejects an overlong command.
37. Parse SET,120 followed by newline; validate that the numeric range is 0–255.
38. Receive bytes into a fixed-size array without writing past its capacity.
39. Describe a frame with start marker, command, length, payload and checksum.
40. Explain why a fixed-size buffer parser must handle partial packets.
41. Describe one risk of blocking serial reads in a time-critical control loop.
42. Print decimal 31 in hexadecimal format.
43. Print a float named voltage with two digits after the decimal point.
44. Discard all currently available received bytes.
45. Explain why readBytes() can return fewer bytes than requested.
46. Explain why String-heavy serial parsing may be problematic on a memory-constrained MCU.
47. Read each received byte and echo it using write().
48. Set a 500 ms timeout and then call parseInt().
49. Explain why UART baud rate and frame configuration must be compatible at both ends.
50. Explain why ESP32 UART pin mapping and available UARTs should be checked for the selected board.

### Intermediate Level

51. Add brief comments: Write setup() code to start Serial at 115200 baud.
52. Write code that prints “System ready” followed by a line ending.
53. Print 12 and 34 on the same line with no separator.
54. Print A, B and C on separate lines.
55. Read one byte only if input is available.
56. Read one incoming byte into an int named incoming and print its numeric value.
57. Use peek() to inspect the next received byte without consuming it.
58. Wait for outgoing serial data to finish transmitting.
59. Set the Stream timeout to 250 milliseconds.
60. Read up to 6 bytes into an array named data and store the actual count returned.
61. Add brief comments: Use readBytesUntil() to read up to 20 characters or until newline; store the returned count.
62. Read one text field until a comma using readStringUntil().
63. Use readString() to collect incoming text and then print it.
64. Parse an integer command into commandValue and print it.
65. Parse a floating-point sensor reading and print it with two decimal places.
66. Use find() to wait for READY and report whether it was found.
67. Use findUntil() to search for DATA but stop if ! appears first.
68. Show if (Serial) before printing a startup message on a compatible native-USB board.
69. End serial communication and then begin it again.
70. Use write() to send bytes 0x41, 0x42 and 0x43 from an array.
71. Add brief comments: Explain print() versus write() with a short example.
72. Explain what available() measures and why it is useful.
73. Explain how availableForWrite() differs from available().
74. Explain the difference between read() and peek().
75. Explain modern flush() behavior and how it differs from clearing input.
76. Explain how setTimeout() affects readBytes() and parsing methods.
77. Describe one use and one limitation of readBytesUntil().
78. Explain the difference between find() and findUntil().
79. Explain what parseInt() does when the stream contains non-numeric characters.
80. Explain what parseFloat() is intended to extract from a serial stream.
81. Add brief comments: Explain if (Serial) on a native-USB board and why behavior may vary by board.
82. Describe serialEvent() on cores that support it and one limitation.
83. Write ESP32 code to start Serial2 at 9600 baud using RX_PIN and TX_PIN placeholders.
84. Write an ESP32 snippet that prints Serial.availableForWrite().
85. Send PING over ESP32 Serial2 once per second.
86. Create a line-based command reader that stops at newline and rejects an overlong command.
87. Parse SET,120 followed by newline; validate that the numeric range is 0–255.
88. Receive bytes into a fixed-size array without writing past its capacity.
89. Describe a frame with start marker, command, length, payload and checksum.
90. Explain why a fixed-size buffer parser must handle partial packets.
91. Add brief comments: Describe one risk of blocking serial reads in a time-critical control loop.
92. Print decimal 31 in hexadecimal format.
93. Print a float named voltage with two digits after the decimal point.
94. Discard all currently available received bytes.
95. Explain why readBytes() can return fewer bytes than requested.
96. Explain why String-heavy serial parsing may be problematic on a memory-constrained MCU.
97. Read each received byte and echo it using write().
98. Set a 500 ms timeout and then call parseInt().
99. Explain why UART baud rate and frame configuration must be compatible at both ends.
100. Explain why ESP32 UART pin mapping and available UARTs should be checked for the selected board.

### Advanced Level

101. Include input validation: Write setup() code to start Serial at 115200 baud.
102. Write code that prints “System ready” followed by a line ending.
103. Print 12 and 34 on the same line with no separator.
104. Print A, B and C on separate lines.
105. Read one byte only if input is available.
106. Read one incoming byte into an int named incoming and print its numeric value.
107. Use peek() to inspect the next received byte without consuming it.
108. Wait for outgoing serial data to finish transmitting.
109. Set the Stream timeout to 250 milliseconds.
110. Read up to 6 bytes into an array named data and store the actual count returned.
111. Include input validation: Use readBytesUntil() to read up to 20 characters or until newline; store the returned count.
112. Read one text field until a comma using readStringUntil().
113. Use readString() to collect incoming text and then print it.
114. Parse an integer command into commandValue and print it.
115. Parse a floating-point sensor reading and print it with two decimal places.
116. Use find() to wait for READY and report whether it was found.
117. Use findUntil() to search for DATA but stop if ! appears first.
118. Show if (Serial) before printing a startup message on a compatible native-USB board.
119. End serial communication and then begin it again.
120. Use write() to send bytes 0x41, 0x42 and 0x43 from an array.
121. Include input validation: Explain print() versus write() with a short example.
122. Explain what available() measures and why it is useful.
123. Explain how availableForWrite() differs from available().
124. Explain the difference between read() and peek().
125. Explain modern flush() behavior and how it differs from clearing input.
126. Explain how setTimeout() affects readBytes() and parsing methods.
127. Describe one use and one limitation of readBytesUntil().
128. Explain the difference between find() and findUntil().
129. Explain what parseInt() does when the stream contains non-numeric characters.
130. Explain what parseFloat() is intended to extract from a serial stream.
131. Include input validation: Explain if (Serial) on a native-USB board and why behavior may vary by board.
132. Describe serialEvent() on cores that support it and one limitation.
133. Write ESP32 code to start Serial2 at 9600 baud using RX_PIN and TX_PIN placeholders.
134. Write an ESP32 snippet that prints Serial.availableForWrite().
135. Send PING over ESP32 Serial2 once per second.
136. Create a line-based command reader that stops at newline and rejects an overlong command.
137. Parse SET,120 followed by newline; validate that the numeric range is 0–255.
138. Receive bytes into a fixed-size array without writing past its capacity.
139. Describe a frame with start marker, command, length, payload and checksum.
140. Explain why a fixed-size buffer parser must handle partial packets.
141. Include input validation: Describe one risk of blocking serial reads in a time-critical control loop.
142. Print decimal 31 in hexadecimal format.
143. Print a float named voltage with two digits after the decimal point.
144. Discard all currently available received bytes.
145. Explain why readBytes() can return fewer bytes than requested.
146. Explain why String-heavy serial parsing may be problematic on a memory-constrained MCU.
147. Read each received byte and echo it using write().
148. Set a 500 ms timeout and then call parseInt().
149. Explain why UART baud rate and frame configuration must be compatible at both ends.
150. Explain why ESP32 UART pin mapping and available UARTs should be checked for the selected board.