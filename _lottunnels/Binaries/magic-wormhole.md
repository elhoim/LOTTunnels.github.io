---
Name: Magic Wormhole
Description: Magic Wormhole is a Python command-line tool that moves files, directories or short text snippets between two computers using short, human-pronounceable one-time codes. A public mailbox server brokers rendezvous and a public transit relay forwards data when a direct connection cannot be made, so transfers work out of most networks without additional setup.
Author: elhoim
Created: 2026-11-09
Commands:
  - Command: wormhole send <FILE_OR_FOLDER>
    Description: Generates a one-time wormhole code and makes the file available for transfer through the public mailbox/relay servers.
    Usecase: Exfiltrating files from a compromised host to an operator-controlled machine.
    Category: exfiltrate
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: wormhole receive <CODE>
    Description: Receives the file or text associated with the given wormhole code.
    Usecase: Pulling a payload or tool onto a compromised host.
    Category: download
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS
Full_Path:
  - Filename: wormhole
  - Path: pip-installed magic-wormhole package, executed anywhere on the system.
Detection:
  - Domain: 'relay.magic-wormhole.io'
  - Domain: 'wormhole-transit.debian.net'
  - Command: Execution of wormhole (or python -m wormhole) with send or receive arguments.
  - Command: Outbound connections to the public mailbox or transit-relay services from a host with no legitimate reason to transfer files that way.
Resources:
  - Link: https://github.com/magic-wormhole/magic-wormhole
  - Link: https://magic-wormhole.readthedocs.io
---
