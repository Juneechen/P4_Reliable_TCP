# P4_Reliable_TCP

Project for CS 5700 Computer Networks by Christo Wilson class taking in Spring 2024.

- COntributors: Ujwal Gupta, Shujun Chen

# Reliable UDP Communication

This project implements a reliable UDP communication protocol between a sender and a receiver. The sender sends messages to the receiver, and the receiver acknowledges the receipt of each message. The sender employs congestion control and timeout-based retransmission mechanisms to ensure reliable delivery of messages.

## High-Level Approach

- **Sender:**
  - Utilizes UDP sockets for communication.
  - Attach checksum to packets.
  - Maintain a `seq_num` and `last_ack_seq` to keep track of packet status.
  - Keep a copy of all `in-flight` packets with meta info including sent time, timeout time, re-transmit or not, etc.
  - Handle accumulative ack and remove packets from `in_flight` list properly.
  - Implements congestion control using a sliding window mechanism.
  - Estimate the RTT with each sample RTT from all non-retranmitted packets.
  - Maintain a `timeout` value, which is dynamictic adjusted by estimating RTT.
  - Dynamically adjust `cwnd` based on acknowledgments and timeouts, in response to various network enviroments and incidents.
  - Simulate TCP Reno's behavior of fast-retransmission.
  - Handles acknowledgments, timeouts, and retransmissions reliably.
- **Receiver:**
  - Binds to a UDP socket to receive messages.
  - Verifies checksums for received packets to detect corruption.
  - Sends cumulative acknowledgments to the sender.
  - Maintain a `next_expected` sequence number.
  - Hold on to all out of order packets in an `recved` dictionary
  - Reconstructs the original message from received packets.

## Challenges Faced

- **Reliability Over UDP:** Implementing reliability over UDP required handling acknowledgments, timeouts, and retransmissions to ensure message delivery.
- **Congestion Control:** Designing an efficient congestion control mechanism to regulate the flow of data while maximizing throughput without causing congestion collapse.
- **Checksum Calculation:** Ensuring accurate checksum calculation to detect corrupted packets while minimizing computational overhead.

## Key Features

- **Reliability:** Implements acknowledgment-based reliability mechanisms to ensure message delivery.
- **Congestion Control:** Utilizes a sliding window and congestion window to regulate the flow of data.
- **Checksum Verification:** Computes and verifies checksums for detecting corrupted packets.
- **Timeout-Based Retransmissions:** Retransmits packets upon timeout to handle packet loss.
- **Cumulative Acknowledgments:** Sends cumulative acknowledgments to acknowledge received packets efficiently.

## Testing Approach

- All tests done using the testing network simulator.
- **Unit Testing:** Conducted extensive unit testing for individual components and functionalities.
- **Integration Testing:** Tested the interaction between sender and receiver to ensure seamless communication.
- **Stress Testing:** Simulated various network conditions and loads to evaluate the robustness and scalability of the protocol.
- **Error Handling Testing:** Tested error handling mechanisms for scenarios such as packet corruption, timeout, and unexpected behavior.
