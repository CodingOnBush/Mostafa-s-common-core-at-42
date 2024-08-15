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

## How to start ?
A main.cpp file is the best way to start :
```cpp
#include <iostream>

int main(void)
{
	// Create a socket
	// Bind the socket to an address
	// Listen for incoming connections
	// Accept incoming connections
	// Receive data from the client
	// Print the data received
	// Close the connection
	// Close the socket
	return 0;
}
```

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
A socket is a communication endpoint. It allows two processes to communicate with each other.\
When I create a socket, I can use it to send and receive data.\
The sockets are managed by the operating system of each computer.\
They interact with the network interface card (NIC) to send and receive data over the network.\
It's called a socket because it looks like an electrical socket.\
There are different types of sockets, like TCP, UDP, etc.\

