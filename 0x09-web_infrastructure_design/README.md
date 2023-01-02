# 0x09. Web Infrastructure design
``DevOps`` ``SysAdmin`` ``web infrastructure``

**Resource**
[Web Server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)
[scale DNS with round-robin DNS](https://www.dnsknowledge.com/whatis/round-robin-dns/)
[How DNS works - Cartoon](https://howdns.works/ep6/)


**Note**
**Server:**  is a piece of computer hardware or software (computer program) that provides functionality (called services) for other programs or devices, called _clients_. Servers are located in datacenters which are building that host hundreds, or even thousands of computers.
Typical servers are database servers, file servers, mail servers, web servers, proxy servers, game servers, and application servers.

Application Server: Hosts web apps (computer programs that run inside a web browser) allowing users in the network to run and use them, without having to install a copy on their own computers.

Database Server: Maintains and shares any form of database (organized collection of data with predefined properties that may be displayed in a table) over a network.

File Server: Shares file and folders, storage space to hold files and folder, or both over a network.

Game Server: Enables several computers or gaming devices to play multiplayer video games.

Mail Server: Makes email communication possible in the same way that a post office makes [snail mail](https://en.wikipedia.org/wiki/Mail) communication possible.

Proxy Server: Acts as an intermediary between a client and a server, accepting incoming traffic from the client and sending it to the server. Reasons for doing so include content control and filtering, improving traffic performance, preventing unauthorized network access or simply routing the traffic over a large and complex network.

Web Server: Hosts and serves web pages. A web server is what makes the World Wide Web possible. World Wide Web commonly known as the **Web**, is an information system enabling documents and other web resources to be accessed over the internet).


**Web Server**  
Web server can refer to hardware of software, or both working together.
1. On the hardware side, a web server is a computer that stores web server software and a website's compontent file (e.g., HTML doc, images, CSS stylesheets and JavaScript files). A web server connects to the internet and supports physical data interchange with other devices connected to the web.
2. On the software side, a web server includes several parts that controls how web users access hosted files. At a minimum, this is an HTTP server. An HTTP server is software that understands URLs and HTTP (the protocol the browser uses to view webpages). An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.

To publish a website, you need either a static or a dynamic web server.  
A **static web server**, or stack, consists of a computer (hardware) with an HTTP server (software) that sends its hosted files as-is to your browser.  
A **dynamic web server** consists of a static web server plus extra software, most commonly an application server and a database to process and updates the hosted files before sending content to your browser via the HTTP server.


**DNS**  
DNS, simply is the technology that translate human-adapted, text-based domain names to machine-adapted, numerical-based IP.  
**DNS record types**  
A: An A (address) record maps a domain name to the _IPv4_ address of the computer hosting the domain. A domain can have many _A_ records, (e.g., example.com could have an A record for www.example.com -> 127.0.0.1, and another for mail.example.com -> 127.0.0.2)  
AAAA record is the _IPv6_ version of _A_ record.  
**You can use ``dig A www.example.com`` to determine the *A* record associated to a domain name**  
CName: A Canonical Name (CNAME) record maps one domain name (an alias) to another (the canonical name). This can prove convenient when running multiple services (like FTP server and web server, each running on different ports) from a single IP address. One can, for example, use CNAME records to point ftp.example.com and www.example.com to the DNS entry for example.com, which in turn has an A record which points to the IP address. Then, if the IP address ever changes, one only has to record the change in one place within the network - in the DNS A record for example.com.
```
Name			Type	Value
bar.example.com		CNAME	foo.example.com
foo.example.com		A	192.0.2.23
```
**bar.example.com** is the alias name for the canonical Name, **foo.example.com**  
MX: A mail exchanger record specifies the mail server responsible for accepting email messages on behalf of a domain name. [Overview](https://en.wikipedia.org/wiki/MX_record#overview)
TXT: A text record provide the ability to associate arbitrary text with a host or other name, such as human readable information about a server, network, data center, or other accounting information.

**The root domain and sub domain - differences**
A root domain is the parent domain to a sub domain, and its name is not, and can not be divided by a dot.  
The dot in the domain name delimits the domain name (This means that the address **my.domain.com** is a sub domain of the root domain, whose name is **domain.com**)  
**Note: www** is also a sub domain [*What's the point in having "www" in a URL*](https://serverfault.com/questions/145777/what-s-the-point-in-having-www-in-a-url)


**Load balancer**  
**Monitoring**  


## Tasks
| Task | File | Description |
|------|------|-------------|
Infrastructure Design | [0-simple_web_stack](./0-simple_web_stack) | design of a one server web infrastructure tha host the website 'www.foobar.com' (*It must use 1 server, 1 web server (Nginx), 1 application server, 1 application files (code base), 1 database (MySQL), 1 domain name (foobar.com) configured with a www record that points to server IP (8.8.8.8)*)
Infrastructure Design | [1-distributed_web_infrastructure](./1-distributed_web_infrastructure) | (*It must add 2 server, 1 web server (Nginx), 1 application server, 1 load-balancer (HAproxy), 1 set of application file (code base) 1 database (MySQL)*)
Infrastructure Design | [2-secured_and_monitored_web_infrastructure](./2-secured_and_monitored_web_infrastructure) | (*It must add 3 firewalls, 1 SSL certificate to serve 'www.foobar.com' over HTTPS, 3 monitoring client (data collector for Sumologic or other monitoring services)*)
Infrastructure Design | [3-scale_up](./3-scale_up) | (*It must add 1 server, 1 load-balancer (HAproxy) configured as cluster with the other one, Split components (web server, application server, database) with their server*)