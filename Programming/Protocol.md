2025-03-29
Tags: [[Streaming]] [[ETL]] [[Data Engineering]] [[Programming]] [[Network]]

Protocol is a set of rules that determine how data is moved between devices in a network.

Some examples of protocols:
- [[FTP]] -> File Transfer Protocol.
	- Used to transfer files between a client and a server.
- [[HTTP]] -> Hypertext Transfer Protocol.
	- Used for transmitting web pages and other content over the internet
- [[JDBC]] -> Java database connectivity.
	- Example: Retrieving data from a PostgreSQL database using Java
- [[SCP]] -> Secure Copy Protocol
	- Method for transferring files between computers over SSH
		- Example: Copying a backup file from a local machine to a server using the command:```
```sh
scp backup.sql user@server:/backup/
```

- [[UDP]] -> Connectionless oriented protocol that prioritizes speed and efficiency over reliability. It sends data packets (called datagrams) without establishing a connection first and doesn't guarantee delivery, order or error correction. 

- [[TCP]] -> Connection oriented protocol, prioritizes reliability and data integrity. Before sending any data, it establishes a connection between sender and receiver in a "handshake". TCP protocol ensures data integrity, if a packet is corrupted or there are errors, the protocol will resend it. 
	- This protocol is used when data accuracy is crucial -> email, file transfer, data base transactions


UDP vs TCP -> Speed vs reliability 

*All ICMP - IPv4* -> ICMP (Internet Control Message Protocol) is used for network diagnostics and communication, not data transfer

*IPSec Tunnel (IKE)* v1 and v2 

*SSTP Tunnel*


----
### Reference

ChatGPT conversation
Claude conversation