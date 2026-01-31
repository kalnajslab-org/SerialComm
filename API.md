# API Documentation

## SerialComm Class
Implements a robust serial (UART) protocol for inter-Arduino messaging.

### Constructor
- `SerialComm(Stream * stream_in)`
  - Initializes the communication on the given stream.

### Methods
- `void UpdatePort(Stream * stream_in)`
  - Change the serial port used for communication.
- `void AssignBinaryRXBuffer(uint8_t * buffer, uint16_t size)`
  - Attach a pre-allocated buffer for binary message reception.
- `void AssignBinaryTXBuffer(uint8_t * buffer, uint16_t size, uint16_t num_bytes)`
  - Attach a pre-allocated buffer for binary message transmission.
- `SerialMessage_t RX()`
  - Receive and parse the next message.
- `void TX_ASCII()`
  - Transmit the current ASCII message.
- `void TX_ASCII(uint8_t msg_id)`
  - Transmit an ASCII message with a specific ID.
- `void TX_Ack(uint8_t msg_id, bool ack_val)`
  - Transmit an ACK/NAK message.
- `bool TX_Bin()`
  - Transmit the current binary message.
- `bool TX_Bin(uint8_t bin_id)`
  - Transmit a binary message with a specific ID.
- `void TX_String(uint8_t str_id, const char * msg)`
  - Transmit a string message.

#### ASCII RX Buffer Interface
- `bool Get_uint8(uint8_t * ret_val)`
- `bool Get_uint16(uint16_t * ret_val)`
- `bool Get_uint32(uint32_t * ret_val)`
- `bool Get_int8(int8_t * ret_val)`
- `bool Get_int16(int16_t * ret_val)`
- `bool Get_int32(int32_t * ret_val)`
- `bool Get_float(float * ret_val)`

#### ASCII TX Buffer Interface
- `bool Add_uint8(uint8_t val)`
- `bool Add_uint16(uint16_t val)`
- `bool Add_uint32(uint32_t val)`
- `bool Add_int8(int8_t val)`
- `bool Add_int16(int16_t val)`
- `bool Add_int32(int32_t val)`
- `bool Add_float(float val)`

#### String RX Buffer Interface
- `bool Get_string(char * buffer, uint16_t buffer_size)`

#### Buffers and State
- `ASCII_MSG_t ascii_rx`, `ascii_tx`
- `BIN_MSG_t binary_rx`, `binary_tx`
- `STRING_MSG_t string_rx`, `string_tx`
- `uint8_t ack_id`, `bool ack_value`, `bool ack_checksum`

---

## Serialize Module
Functions for serializing and deserializing data types into/from buffers.

### Endianness
- `Endianness_t endianness`
  - Global variable to set serialization endianness.

### Buffer Add Functions
- `bool BufferAddUInt8(uint8_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddUInt16(uint16_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddUInt32(uint32_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddInt8(int8_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddInt16(int16_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddInt32(int32_t data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferAddFloat(float data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`

### Buffer Get Functions
- `bool BufferGetUInt8(uint8_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetUInt16(uint16_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetUInt32(uint32_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetInt8(int8_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetInt16(int16_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetInt32(int32_t * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`
- `bool BufferGetFloat(float * data, uint8_t * buffer, uint16_t buffer_size, uint16_t * curr_index)`

---

## MCBComm Class
Extends `SerialComm` for communication between MCB and DIB/PIB.

### Constructor
- `MCBComm(Stream * serial_port)`
  - Initializes the MCBComm interface on the given serial port.

### Methods
- `bool TX_Motion_Status(float reel_pos, float lw_pos, float reel_torque, float reel_temp, float lw_temp)`
- `bool RX_Motion_Status(float * reel_pos, float * lw_pos, float * reel_torque, float * reel_temp, float * lw_temp)`
- `bool TX_Reel_Out(float num_revs, float speed)`
- `bool RX_Reel_Out(float * num_revs, float * speed)`
- `bool TX_Reel_In(float num_revs, float speed)`
- `bool RX_Reel_In(float * num_revs, float * speed)`
- `bool TX_Dock(float num_revs, float speed)`
- `bool RX_Dock(float * num_revs, float * speed)`
- `bool TX_Out_Acc(float acceleration)`
- `bool RX_Out_Acc(float * acceleration)`
- `bool TX_In_Acc(float acceleration)`
- `bool RX_In_Acc(float * acceleration)`
- `bool TX_Dock_Acc(float acceleration)`
- `bool RX_Dock_Acc(float * acceleration)`

---

## Enums and Structs

### SerialMessage_t
- `NO_MESSAGE`, `ASCII_MESSAGE`, `ACK_MESSAGE`, `BIN_MESSAGE`, `STRING_MESSAGE`

### ASCII_MSG_t
- Structure for ASCII messages (ID, params, buffer, checksum)

### STRING_MSG_t
- Structure for string messages (ID, length, buffer, checksum)

### BIN_MSG_t
- Structure for binary messages (ID, length, buffer, checksum)

### MCBMessages_t
- Enum for MCB/DIB/PIB message types

---

For more details, see the header files and example sketches.
