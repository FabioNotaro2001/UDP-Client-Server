# UDP Client-Server File Transfer

A network programming project developed for a university course that implements a **UDP-based client-server architecture** for reliable file transfer. The system supports listing, uploading, and downloading files between client and server using a custom control-message protocol.

## Features

- Built on **UDP sockets** (connectionless)
- Custom message-based communication protocol (HELLO, OK, FAIL, DATA, DONE)
- Support for file **upload (`put`)**, **download (`get`)**, and **listing (`list`)**
- **Concurrent client support** using threading
- Graceful **exit** handling per client
- **File transfer of large files** via chunked messages
- **Command validation** and robust error handling
- Transfer **time statistics**
- Tested using **Wireshark** and across separate hosts with IP forwarding

## Project Structure
UDP-Client-Server/
├── client.py # UDP client
├── server.py # UDP server (multi-client threaded)
└── response.py # Constants and protocol message definitions

## Protocol Overview

| Message | Sender        | Purpose                                           |
|---------|---------------|---------------------------------------------------|
| HELLO   | Client        | Initiate communication                            |
| OK      | Client/Server | Acknowledge valid message                         |
| FAIL    | Server        | Signal error occurred                             |
| DATA    | Client/Server | Transmit actual file content                      |
| DONE    | Client/Server | Indicate completion of a file transfer operation  |

## Server States

The server maintains states per client to manage concurrent interactions:
- `OPENING`
- `REGULAR`
- `WAIT_FOR_FILE_STATUS`
- `WAIT_FOR_FILE_DATA`
- `SEND_FILE_STATUS`
- `SEND_FILE_DATA`
- `SEND_COMPLETE`
- `CLOSED`

Each state determines how the server processes the next message and transitions between operations.

## Getting Started

### Prerequisites

- Python 3.x
- Any Python IDE (e.g., Spyder, VS Code) or terminal

### How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/FabioNotaro2001/UDP-Client-Server.git
   cd UDP-Client-Server
Start the server in one terminal:
python server.py
Start the client in another terminal:
python client.py
    Make sure to start the server before the client.

Client Commands

    list – Lists available files on the server

    get <filename> – Downloads a file from the server

    put <filename> – Uploads a file to the server

    exit – Closes the connection from client-side

Error Handling & Validation

Client command input is carefully validated. Examples of handled errors:

    Unknown commands

    Wrong command syntax (e.g., list extra)

    Requesting files that don't exist

    Uploading files already on the server

    Illegal file paths or names

    Case-insensitive command parsing

Notes on Deployment

To test across real hosts:

    Replace localhost with your server’s actual IP

    Enable port forwarding on the server’s router if on different networks

Authors

    Andrea Bedei – andrea.bedei2@studio.unibo.it

    Giacomo Leo Bertuccioli – giacomo.bertuccioli@studio.unibo.it

    Fabio Notaro – fabio.notaro2@studio.unibo.it

License

This project is licensed for educational purposes.

Let me know if you'd like to add badges (e.g., Python version), images (Wireshark screenshots), or Docker support instructions.
