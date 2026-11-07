| **Function**         | **Header**       | **Purpose**                                                                                                |
| -------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------- |
| `socket()`           | `<sys/socket.h>` | Creates an endpoint for network communication (returns a file descriptor).                                 |
| `bind()`             | `<sys/socket.h>` | Assigns an IP address and port number to our socket.                                                       |
| `listen()`           | `<sys/socket.h>` | Marks the socket as passive, ready to accept incoming connection requests.                                 |
| `accept()`           | `<sys/socket.h>` | Extracts the first connection request on the queue and returns a **new** connected socket file descriptor. |
| `read()` / `write()` | `<unistd.h>`     | Reads raw request bytes from the client socket and writes our HTTP response back.                          |
