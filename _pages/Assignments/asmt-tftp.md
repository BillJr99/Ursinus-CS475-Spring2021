---
layout: assignment
permalink: /Assignments/TFTP
title: "CS475: Computer Networks - TFTP Protocol"
excerpt: "CS475: Computer Networks - TFTP Protocol"

info:
  coursenum: CS475
  points: 100
  goals:
    - To implement a protocol according to its RFC
  rubric:
    - weight: 60
      description: Algorithm Implementation
      preemerging: The algorithm fails on the test inputs due to major issues, or the program fails to compile and/or run
      beginning: The algorithm fails on the test inputs due to one or more minor issues
      progressing: The algorithm is implemented to solve the problem correctly according to given test inputs, but would fail if executed in a general case due to a minor issue or omission in the algorithm design or implementation
      proficient: A reasonable algorithm is implemented to solve the problem which correctly solves the problem according to the given test inputs, and would be reasonably expected to solve the problem in the general case
    - weight: 30
      description: Code Quality and Documentation
      preemerging: Code commenting and structure are absent, or code structure departs significantly from best practice, and/or the code departs significantly from the style guide
      beginning: Code commenting and structure is limited in ways that reduce the readability of the program, and/or there are minor departures from the style guide
      progressing: Code documentation is present that re-states the explicit code definitions, and/or code is written that mostly adheres to the style guide
      proficient: Code is documented at non-trivial points in a manner that enhances the readability of the program, and code is written according to the style guide
    - weight: 10
      description: Writeup and Submission
      preemerging: An incomplete submission is provided
      beginning: The program is submitted, but not according to the directions in one or more ways (for example, because it is lacking a readme writeup)
      progressing: The program is submitted according to the directions with a minor omission or correction needed, and with at least superficial responses to the bolded questions throughout
      proficient: The program is submitted according to the directions, including a readme writeup describing the solution, and thoughtful answers to the bolded questions throughout
      
tags:
  - tftp
  
---

## A tftp Server
You should construct a file transfer server that is using the TFTP protocol ([RFC 1350](https://tools.ietf.org/html/rfc1350)). Part one of this assignment involves constructing the server, while part two involves constructing the client.

Your programs should adhere to the published specifications so that they can inter-operate with existing clients and servers.

You could test your server with the tftp client available under most Unix (and Unix-like) operating systems (e.g. Solaris, Linux, OpenBSD, etc.). [Here](https://linuxhint.com/install_tftp_server_ubuntu/) is an article describing how to install and configure tftp on Ubuntu.  However, if you do, note that some extensions to tftp are implemented by modern clients, rendering this spec non-backwards compatible. You'll need to implement slightly different message formats to do so (look at the tftp OACK extensions).  You might, instead, copy your server implementation and write a small client for testing instead, which is also acceptable.

It is a requirement that the server should be able to accommodate multiple clients at the same time (i.e. it should be able to exchange data with more than one client). Having a client wait until the transfer with another client is complete is not acceptable.  You can accomplish this by putting your server code into a threaded routine, and starting the thread with the connection socket as soon as a connection is made by the primary server socket in `main()`.  

### Notes
The tftp service is using port 69 which requires superuser (administrator) access rights. Since you want to be able to run your server on machines where you may not have superuser privileges, you should include the option to run the server from another (non-privileged) port.