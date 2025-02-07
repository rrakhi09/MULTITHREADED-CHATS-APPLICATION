# MULTITHREADED-CHATS-APPLICATION

COMPANY: CODTECH IT SOLUTIONS

NAME: RAKHI RATHI

INTERN ID: CT080FA

DOMAIN: JAVA PROGRAMMING

DURATION: 4 WEEKS

MENTOR:NEELA SANTOSH

DESCRIPTION OF TASK:

The given code represents a basic chat application in Java where both server and client functionalities are implemented within a single program. This application allows multiple clients to connect to a central server and exchange messages in real-time. It uses Java's networking and multi-threading features to enable communication between the server and multiple clients.

Imports:

java.io.*: Used for input/output operations, including reading and writing data streams.
java.net.*: Used for networking tasks such as creating sockets for communication.
java.util.*: Provides utility classes like Scanner for reading user input.
java.util.concurrent.CopyOnWriteArraySet: A thread-safe collection used to store client output writers.
Main Class (ChatApp):

The ChatApp class contains the main method, which serves as the entry point of the program. This method prompts the user to choose between running the server or the client and proceeds to call the respective method (startServer() or startClient()).
Server Code (startServer() method):

The startServer() method is responsible for initializing the server. It listens on port 5050 using a ServerSocket object. The server is designed to handle multiple clients by spawning a new ClientHandler thread whenever a client connects.
Inside the infinite while(true) loop, the server continuously waits for client connections using serverSocket.accept(). When a client connects, it creates a new ClientHandler thread, which handles communication with that specific client.
ClientHandler Class (Inner Class):

The ClientHandler class extends Thread, allowing each connected client to be handled in a separate thread. It manages communication between the client and the server using PrintWriter (for writing messages to the client) and BufferedReader (for reading messages from the client).
The run() method continuously reads messages from the client. When a message is received, it is broadcast to all connected clients using a synchronized set (clientWriters), which contains all PrintWriter objects of connected clients.
If a client disconnects or encounters an error, the cleanup() method is called, which removes the client from the list of writers and closes the socket.
Client Code (startClient() method):

The startClient() method connects to the server by creating a Socket object that connects to localhost on port 5050.
Once connected, the client starts a new thread (the Reader thread) that continuously listens for incoming messages from the server and displays them on the console.
In the main loop, the client allows the user to type messages. If the message is "exit", the client sends a disconnect message and terminates the connection. Otherwise, it sends the message to the server, which will broadcast it to all other connected clients.
Reader Class (Inner Class):

The Reader class implements the Runnable interface. It reads messages sent by the server using the BufferedReader object and prints them to the console. This is done in a separate thread to allow the client to send and receive messages concurrently.
If the connection is lost or closed, the Reader thread stops, and the socket is closed.
Key Concepts Used:
Sockets: The program utilizes Java sockets to establish a communication link between the server and clients. ServerSocket is used on the server side to accept incoming client connections, while Socket is used on the client side to connect to the server.
Multi-threading: The server and each client run in separate threads, allowing them to perform tasks concurrently. The server creates a new ClientHandler thread for each client, while the client spawns a Reader thread to receive messages.
Thread-safe Collection: A CopyOnWriteArraySet is used to store the list of PrintWriter objects representing the output streams of connected clients. This collection is thread-safe, meaning multiple threads can safely add/remove writers without causing data inconsistency.
BufferedReader and PrintWriter: These are used for reading and writing messages between the server and client. BufferedReader reads input from the network, while PrintWriter sends output to the network.
Conclusion:
This chat application demonstrates the fundamentals of client-server communication, multi-threading, and message broadcasting. It allows multiple clients to send and receive messages to/from each other via the server. The code is designed to handle client connections efficiently and manage multiple clients simultaneously by using threads and a thread-safe data structure.
