# webserv
## What's going on ?
I'm going to explain everything about webserv, from the beginning to the end. Don't worry, I'll try to make it as simple as possible and I hope my pedagogical skills will be enough to make you understand everything. Let's start by the beginning, shall we ?

## Understanding the subject
First of all, I decided to read the subject carefully and extract the most important informations from it that I will need to understand in order to complete the project. Here is what I found : HTTP, CGI, Configuration file, sockets, epoll, RFC, errno, server, web, client, request, etc.

## What is the web and a server ?
When I write a URL in my browser and press enter, my browser sends a request to the server that hosts the website I want to access. The server receives the request and do something with it to send back a response to my browser.\
The response contains the data I want to access, like a web page, an image, a video, etc. And sometimes, the server can also send back an error message. Don't worry, there is a lot of possible errors 😂

**Tips :**\
*The client and the server communicate with each other using what you understood in the NetPractice project. You don't need to understand more about it for now. I was greedy about understanding everything from the beginning in the most detailed way possible, but I realized that it is not necessary to understand everything in detail to complete the project. It is better to focus on the most important things first. Otherwise, I would have spent too much time on everything I wanted to understand and I would have been lost in the end.*

## What is HTTP ?
If I want to discuss with you, I can use my mouth to speak, my ears to listen, the air to transmit the sound, and my brain to understand what you say.\
HTTP is a protocol that describes how the client and the server communicate with each other. It is like a language that the client and the server speak to understand each other.

## Our goal
Our goal is to create a program that will act as a server. This program will be able to receive requests from clients, process them, and send back responses.\
As a begining, I want to create a simple program that will be able to receive a request from a client and that's all. I will add more features later.

## What is a request ?
A request is a message sent by the client to the server. It contains informations like the method, the path, the headers, the body, etc. And here is an example :
```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```
But when I use my browser to access a website, I don't see the request. I only write the URL and press enter. The browser does the rest for me.\
I can use a tool like curl to send a request to a server instead of using my browser.\
Here is an example of a request sent with curl :
```bash
curl -X GET http://www.example.com/index.html
```
**How this request is sent to the server ?**\
The client creates a socket and connects to the server. Then, the client sends the request to the server. The server receives the request and processes it. Finally, the server sends back a response to the client.\

## What is a socket ?
A socket is a communication endpoint. It allows two processes to communicate with each other. The sockets are managed by the operating system of each computer.\
They interact with the network interface card (NIC) to send and receive data over the network. A socket is identified by an IP address and a port number.\
If I want to create a socket in C++, I can use the socket() function from the sys/socket.h library :
```cpp
#include <sys/socket.h>

int main(void)
{
	int sockfd = socket(AF_INET, SOCK_STREAM, 0);
	if (sockfd == -1)
	{
		std::cerr << "Error: socket creation failed" << std::endl;
		return 1;
	}
	return 0;
}
```
The socket() function returns a file descriptor that I can use to interact with the socket.\
The first argument of the socket() function is the domain. It can be AF_INET for IPv4 or AF_INET6 for IPv6.\
The second argument is the type. It can be SOCK_STREAM for TCP or SOCK_DGRAM for UDP.\
The third argument is the protocol. It can be 0 for the default protocol of the domain and type.

## How to start ?
I want to send a request to my program using curl and see if my program receives it. I will create a socket, bind it to an address, listen for incoming connections, accept the connection, and receive the request :
```cpp
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>

int main(void)
{
	int sockfd = socket(AF_INET, SOCK_STREAM, 0);
	if (sockfd == -1)
	{
		std::cerr << "Error: socket creation failed" << std::endl;
		return 1;
	}

	struct sockaddr_in addr;
	addr.sin_family = AF_INET;
	addr.sin_addr.s_addr = INADDR_ANY;
	addr.sin_port = htons(8080);

	if (bind(sockfd, (struct sockaddr *)&addr, sizeof(addr)) == -1)
	{
		std::cerr << "Error: bind failed" << std::endl;
		return 1;
	}

	if (listen(sockfd, 10) == -1)
	{
		std::cerr << "Error: listen failed" << std::endl;
		return 1;
	}

	int connfd = accept(sockfd, NULL, NULL);
	if (connfd == -1)
	{
		std::cerr << "Error: accept failed" << std::endl;
		return 1;
	}

	char buffer[1024];
	int n = read(connfd, buffer, sizeof(buffer));
	if (n == -1)
	{
		std::cerr << "Error: read failed" << std::endl;
		return 1;
	}

	std::cout << buffer << std::endl;

	close(connfd);
	close(sockfd);

	return 0;
}
```
== work in progress ==
