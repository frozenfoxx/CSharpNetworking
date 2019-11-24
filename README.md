# C# Networking
This project is the basic implementation of these low level networking protocols

- **TCP** (\r\n terminated)
- **WebSocket**
- ~~**UDP**~~ *(Not yet)*

## Interfaces
Each protocol implements interfaces IServer or IClient which require that the protocol launches the following events when:

### IServer\<T>
- `OnListen(object server)` When the server is started and listening for clients
- `OnAccepted(object server, T client)` When a client connects to the server
- `OnMessage(object server, Message<T> message)` When server receives a message from a client
- `OnDisconnected(object server, T client)` When a client disconnects from the server
- `OnStopListening(object server)` When the server stops listening for clients
- `OnError(Exception exception)` When there is an exception on the server

### IClient
- `OnConnected(object client)` When the client connects to the server
- `OnMessage(object client, Message message)` When the client receives a message from the server
- `OnDisconnected(object client)` When the client disconnects from the server
- `OnError(Exception exception)` When there is an exception on the client

## Message and Message\<T> Classes
The Message and Message\<T> classes contain the data transferred between server and client. It contains the following fields:

- `string data` A UTF8 encoded message
- `byte[] rawData` An array of bytes representing the message
- `T client` A generically typed client (only on Message\<T>)