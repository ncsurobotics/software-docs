# Serial Messages, CRCs, and Acknowledgements

## Why serial details matter

Mission code only works if the Jetson and electronics boards agree on exactly what every byte means. A serial protocol is that agreement: a structured stream of bytes sent over a device connection.

## Beginner mental model

A frame needs a beginning, an end, a payload, and a way to detect corruption. SW9S uses start/end bytes, escapes special bytes that occur inside a message, and appends a **CRC**. A CRC, or cyclic redundancy check, is a compact calculation used to detect accidental transmission corruption. An **acknowledgement** is the receiver saying it recognized a particular message.

## SW9S implementation

`src/comms/auv_control_board/` provides the reusable `AUVControlBoard` framing layer used by the control board and MEB. Frames use start byte `253`, end byte `254`, escape byte `255`, a big-endian message ID, payload, and CRC-16/CCITT-FALSE. `MessageId` correlates sent requests with returned ACKs.

The writer is protected by an async mutex; background readers decode frames and populate response maps. `GetAck` waits by polling the matching ACK entry.

## Interactions and limits

This framing layer is below missions but above the serial device. `ControlBoard` builds motion/configuration commands on top of it; `MEB` builds status/payload commands.

**Source-derived caution:** many ACK waits have no intrinsic timeout, reader tasks are detached, and malformed inputs have limited validation. Raw binary logs are useful debugging evidence but should not automatically be treated as exact wire captures without confirming the logging behavior.

## Debugging

Trace a command from its high-level board method to `write_out`/`write_out_basic`, then inspect the corresponding response parser. Add parser tests before changing protocol layout. Never test a changed board command on a powered vehicle without a review and a recovery procedure.

## Last verified against SW9S

Source-derived from `fc780a1`; firmware command semantics need team confirmation.
