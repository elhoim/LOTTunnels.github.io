---
Name: OnionShare
Description: OnionShare shares files, hosts a simple website, or opens a chat room directly from a local machine over the Tor network, by publishing the content as a Tor onion service. No third-party hosting is involved, and the content is reachable only to someone with the generated .onion address.
Author: elhoim
Created: 2026-11-09
Commands:
  - Command: onionshare-cli --share <FILE_OR_FOLDER>
    Description: Publishes the given file(s) as a one-time-download onion service and prints the .onion URL.
    Usecase: Exfiltrating files from a compromised host via an anonymous, operator-controlled onion address rather than a named third-party service.
    Category: exfiltrate
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS

  - Command: onionshare-cli --receive
    Description: Starts an onion service that accepts uploads from anyone who is given the .onion address.
    Usecase: Standing up a drop site to receive data or tools over Tor.
    Category: upload
    Privileges: User
    OperatingSystem: Windows, Linux, MacOS
Full_Path:
  - Filename: onionshare
  - Filename: onionshare-cli
  - Path: Installed OnionShare application/CLI, executed anywhere on the system.
Detection:
  - Command: Execution of onionshare or onionshare-cli, particularly with --share or --receive.
  - Command: Presence and execution of a Tor client process (tor/tor.exe) spawned by onionshare, and outbound connections to Tor directory authorities or relays from a host that does not normally run Tor.
Resources:
  - Link: https://github.com/onionshare/onionshare
  - Link: https://docs.onionshare.org
---
