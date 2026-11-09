---
Name: Dumbpipe
Description: Dumbpipe is a small Rust tool built on the iroh peer-to-peer networking library. It connects two machines over a QUIC connection identified by a 256-bit endpoint ID rather than an IP address, using iroh's relay infrastructure for NAT traversal when a direct connection cannot be established. Standard input/output or raw TCP can be piped through the resulting pipe.
Author: elhoim
Created: 2026-11-09
Commands:
  - Command: dumbpipe listen
    Description: Listens for an incoming connection and prints a ticket (containing the node's endpoint ID) that a peer uses to connect. Data piped to its standard input is sent to the connecting peer, and data received is written to standard output.
    Usecase: Exposing a local process (shell, file stream) for an operator to connect into using only an endpoint ID, without an IP address or open inbound port.
    Category: exfiltrate
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: dumbpipe connect <TICKET>
    Description: Connects to the peer identified by the ticket and relays standard input/output over the resulting QUIC connection.
    Usecase: Reaching a dumbpipe listener on a compromised host from the operator side.
    Category: access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: dumbpipe listen-tcp --host <LOCAL_HOST>:<LOCAL_PORT>
    Description: Forwards a local TCP service through the pipe instead of standard input/output.
    Usecase: Tunneling a TCP service (for example a reverse shell listener) over iroh instead of a direct connection.
    Category: access
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS
Full_Path:
  - Filename: dumbpipe
  - Path: cargo-installed/downloaded dumbpipe binary, executed anywhere on the system.
Detection:
  - Domain: 'use1-1.relay.n0.iroh.link'
  - Domain: 'usw1-1.relay.n0.iroh.link'
  - Domain: 'euc1-1.relay.n0.iroh.link'
  - Domain: 'aps1-1.relay.n0.iroh.link'
  - Domain: 'dns.iroh.link'
  - Command: Execution of dumbpipe with listen, connect, listen-tcp or connect-tcp arguments.
  - Command: Outbound QUIC (UDP) traffic to iroh relay infrastructure from a process with no other known networking purpose.
Resources:
  - Link: https://github.com/n0-computer/dumbpipe
---
