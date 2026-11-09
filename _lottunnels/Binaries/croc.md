---
Name: Croc
Description: Croc is a command-line file transfer tool that moves files directly between two computers using a relay for rendezvous and NAT traversal, falling back to relaying the data itself when a direct peer-to-peer connection cannot be made. Transfers are encrypted end-to-end using a short human-readable code, and croc's public relay is reachable from most networks without any configuration.
Author: elhoim
Created: 2026-11-09
Commands:
  - Command: croc send <FILE_OR_FOLDER>
    Description: Generates a one-time code phrase and makes the file available for transfer through croc's public relay (or a self-hosted one).
    Usecase: Exfiltrating files from a compromised host to an operator-controlled machine without installing a dedicated server.
    Category: exfiltrate
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: croc <CODE_PHRASE>
    Description: Receives the file associated with the given code phrase.
    Usecase: Pulling a payload or tool onto a compromised host.
    Category: download
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: croc relay
    Description: Runs a self-hosted relay server (default TCP 9009-9013), letting an operator avoid the public croc.schollz.com relay entirely.
    Usecase: Standing up a private relay to avoid detections keyed on the public service.
    Category: exfiltrate
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS
Full_Path:
  - Filename: croc
  - Filename: croc.exe
  - Path: Downloaded/installed croc binary, executed anywhere on the system.
Detection:
  - Domain: 'croc.schollz.com'
  - Command: Execution of croc with send, or a positional code-phrase argument to receive, or the relay subcommand.
  - Command: Outbound TCP to ports in the 9009-9013 range, or CROC_SECRET/CROC_RELAY/CROC_PASS environment variables set for a process.
Resources:
  - Link: https://github.com/schollz/croc
---
