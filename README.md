<p align="center">
  <a href="https://example.com/">
    <img src="https://i.imgur.com/4JpMe9r.png" alt="Logo" width=100 height=100>
  </a>

  <h3 align="center">Boreas</h3>

  <p align="center">
  A <b>cute</b> Linda implementation in C++
    <br>
    <a href="https://github.com/aeri/Boreas/blob/master/README.md#Getting-Started">Getting Started</a>
    ·
    <a href="https://github.com/aeri/Boreas/blob/master/README.md#deployment">Deployment</a>
  </p>
</p>

# The project
An implementation in C++ of coordination language Linda in a distributed way, motivated as a project for programming concurrent and distributed systems.

## How it works?
The objective of the project is to carry out a distributed implementation of the Linda coordination system. The system provides the operations: **PN** (post note), **RN** (remove note) and **readN** (read note). For simplicity, the tuples will be flat, that is to say, there are no tuples where one of their elements is another tuple (nested tuples), they will have a maximum length of 6 elements and all the elements will be of string type.

![Linda space system](https://i.imgur.com/BNRPF3y.jpg)


The figure shows an abstraction of the developed system.
The Linda server publishes the interface of the distributed coordination system. This interface offers the remote processes five operations: connect to and disconnect from the service, in addition to the three tuple manipulation operations (PN, RN and readN). A C++ process will use the Linda driver library, which is implemented as part of the solution, to invoke these operations remotely.



On the other hand, the Linda server consists of three servers, possibly running on different machines, responsible for storing and managing the operations involving the truples they store. Specifically, the first server will work with size 1 to 3 tuples, the second with size 4 and 5, while the third will be responsible for size 6 tuples. Internally, the tuples will be stored in memory.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

* To compile the Linda system environment you need an operating system that supports POSIX Threads. Unix-like POSIX-conformant operating systems such as FreeBSD, NetBSD, OpenBSD, Linux, macOS...

* Make (build automation tool)

* gcc version >= 4.8.5 with POSIX thread model


### Compiling
To compile the system it is only necessary to execute the Make command inside the **src** folder.


```
$> make
```

And all files will be compiled consecutively and automatically:

```
g++ -c -I. -ISocket -O2 -std=c++11 -lsockets -Wall LindaDriver.cpp
g++ -c -I. -ISocket -O2 -std=c++11 -lsockets -Wall tuplas.cpp -o tuplas.o
g++ -c -I. -ISocket -O2 -std=c++11 -lsockets -Wall Socket/Socket.cpp -o Socket/Socket.o
g++ -c -I. -ISocket -O2 -std=c++11 -lsockets -Wall mainLindaDriver.cpp
........
```
## Deployment

### Servers
The deployment is made in different levels since the system is modular and can be executed in different machines.

* **Storage Server:** The servers that will store the tuples in memory. Exactly three servers must be run for each deployment; if they are on the same machine, different ports must be used.

```
./servei <Port_LS>
```
><Port_LS>: Storage Server port


* **Linda Server:** The core of this system, the intermediary between clients and distributed tuples storage systems.

```
./servidorLinda <Port_LS> <IP_S1> <Port_S1> <IP_S2> <Port_S2> <IP_S3> <Port_S3>
```
><Port_LS>: Linda server port

><IP_S1>: Storage Server IP 1

><Port_S1>: Storage Server port 1

><IP_S2>: Storage Server IP 2

><Port_S2>: Storage Server port 2

><IP_S3>: Storage Server IP 3

><Port_S3>: Storage Server port 3
  

### Clients

The clients are the ones who will service the Linda coordination service through the Linda Server.

* **Interactive Client:** This is a keyboard playable client that allows you to use the system interactively through a guided sequence of steps.

```
./clienteInteractivo <IP_LS> <Port_LS>
```
     
><IP_LS>: Linda server IP

><Port_LS>: server port Linda


* **Mixed Client:** Semi-atuomatic client, asks the user by keyboard a command and randomly selects an operation PN, ReadNote or RN and generates a tuple to work with. The process is repeated indefinitely.

```
./clienteMixto <IP_LS> <Port_LS>
```
     
><IP_LS>: Linda server IP

><Port_LS>: server port Linda

* **Bruteforce:** Automatically upload tuples to tuple servers for stress, memory and access time testing.

```
./bruta <IP_LS> <Port_LS>
```
     
><IP_LS>: Linda server IP

><Port_LS>: server port Linda


## Authors

See the list of [contributors](https://github.com/aeri/Boreas/graphs/contributors) who participated in this project.

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details
