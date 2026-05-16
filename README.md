Distributed Storage Grid (DSG)
A modular, fault‑tolerant, cost‑saving distributed storage system built in C++

Overview
Distributed Storage Grid (DSG) is a C++‑based system designed to help organizations dramatically reduce storage costs while increasing data security and redundancy. Instead of relying solely on centralized servers or expensive cloud storage, DSG leverages the unused disk space on employees’ laptops and PCs to create a distributed, resilient storage network.

The system follows a master–slave architecture:

A Linux‑based master node exposes a shared folder.

Files dropped into this folder are automatically split into data packets.

Packets are distributed across multiple slave nodes (employee machines) over the company network.

Data is stored redundantly using RAID 0+1–style mirroring and striping to ensure both performance and fault tolerance.

This approach transforms ordinary company hardware into a secure, distributed storage grid — without requiring new infrastructure.

Key Features
Master–Slave Architecture
The master node handles packetization, distribution, redundancy logic, and metadata.

Slave nodes store data packets and respond to read/write requests.

Dynamic Plug‑and‑Play Slave Modules
Slave nodes support hot‑swappable modules.

New functionality can be added on the fly without restarting the system.

Ideal for extending storage logic, monitoring, encryption, compression, etc.

RAID 0+1‑Inspired Redundancy
Data is striped across multiple machines for performance.

Each stripe is mirrored to another machine for safety.

Ensures that even if a laptop goes offline, data remains intact.

Linux NBD Integration
The master uses the Linux Network Block Device (NBD) interface.

This allows the master filesystem to interact with DSG as if it were a local block device.

The NBD layer forwards read/write operations into the DSG logic, which distributes them across slaves.

UDP‑Based Communication
Data flows through the company network using UDP.

Reduces overhead and network congestion.

Optimized for high‑throughput, low‑latency packet distribution.

Custom Request Execution Framework
A lightweight framework handles:

File operations

Packet routing

Slave availability

Error handling

Redundancy checks

Designed for scalability and easy extension.

How It Works
1. File Input
Users simply drag and drop files into the master’s shared folder.

2. Packetization
The master splits the file into fixed‑size packets.

3. Distribution
Packets are sent to slave nodes using UDP.
Each packet is:

Stored on a primary slave

Mirrored to a secondary slave

4. Storage
Slave nodes store packets locally and register metadata with the master.

5. Retrieval
When a file is read:

The master requests packets from slaves.

Missing packets are reconstructed from mirrors.

The file is reassembled and served to the user.
