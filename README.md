Red-ring client and backend for abrasive-ducks
----------------------------------------------

Message from the client (e.g. a CCNQ4 application on a voice server) are sent over the `msg` bus (similarly to the socket.io frontend).

Message from the master source towards the client are sent using the subscription channels, to reduce the load on the client.

The following modules are provided:
- `index` — a backend client (usable in a CCNQ4 server application);
- `backend` — a backend plugin for abrasive-ducks.
