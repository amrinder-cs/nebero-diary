Monday 19 August 2024
# Nat Punching using natpunchgo

Nat punching is used for UDP communication between two devices behind NAT and in different networks.
The repository provided for its implementation was [Nat-punch-go](https://github.com/malcolmseyd/natpunch-go?tab=readme-ov-file)


Nat punching requires one server and 2 'clients' which connect to the server. This is the basic idea of Nat hole punching:

![Nat punching](https://upload.wikimedia.org/wikipedia/commons/8/85/UDP_hole_punching.png)


## initial setup

- Since nat punching requires devices behind NAT, we had to simulate it somehow in virtual machines. for that 2 virtual machines `alpine1` and `alipne2` were created in Virtual Box with NAT network (which is default)

- The script uses Wireguard, therefore wireguard was installed on the main machine, acting as the server and on virtual machines `alpine1` and `alipne2`, which were to connect to the server.

- for easy installation of wireguard, [this](https://github.com/angristan/wireguard-install) script was used.

- `alpine1` got the ip `10.66.66.2` and `alpine2` got the ip `10.66.66.3` in the wireguard interface. the main server has the IP `10.66.66.1` in wireguard and `10.1.1.69` otherwise.


## Setup of the natpunch-go script

- compiled client and the server after installing golang on the system, using `cd client && go build -o client` and similar for the server.

- from /etc/wireguard/private.key, copied the wireguard private key



## Attempts to nat-punch:

### Attempt 1:

- on main server (with ip 10.66.66.1), ran the server script using command: `./server 1234 [Key  from /etc/wireguard/private.key]` (syntax mentioned in natpunch-go documentation is: ./server PORT WIREGUARD_PRIVATE_KEY)

- It showed the public key after running the above command.

- on virtual machines (with IPs 10.66.66.2 and 10.66.66.3), ran client script with `./client wg0 10.66.66.1:1234 WIREGUARD_PUBLIC_KEY`

	- Expected outcome:
		- For both the clients to discover each other
	- Actual Outocome:
		- Both clients being able to connect to the server however unable to discover each other.
- Logs of the errors encountered:


From server:


```
→ ./server 1234 sL4JBoo4Y4vAq3J6vdXakuJatySvvOVIgACj081WT2k=
Starting nat-punching server on port 1234
Public key: BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND

```


From client 1:


```
┌─[root][alpine1][~/natpunch-go/client]
└─▪ ./client wg0 10.66.66.1:1234 BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
Resolving 1 peers
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
```


From client 2:

```
[root@alpine2 client]# ./client wg0 10.66.66.1:1234 BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
Resolving 1 peers
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
```



### unusual observation:

- When the client is ran on the "server" itself, which otherwise does not make sense, the server is able to resolve both clients, and both clients are able to resolve the server.

- Furthermore, both clients are able to see each other's ports open, once scanned via nmap.

- Logs of above:

Server:


```
(10:05:35) _ [user@nebero] ~/.../natpunch-go/server (master ?:3 _) 
_ ./server 1234 sL4JBoo4Y4vAq3J6vdXakuJatySvvOVIgACj081WT2k=
Starting nat-punching server on port 1234
Public key: BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: NOT FOUND
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: NOT FOUND
pJrGu8GakllEFD+f ==> g2kX+NzXd8f3b/jg: CONNECTED
pJrGu8GakllEFD+f ==> rdMXY8OzXn/8P4KF: CONNECTED
rdMXY8OzXn/8P4KF ==> pJrGu8GakllEFD+f: CONNECTED
g2kX+NzXd8f3b/jg ==> pJrGu8GakllEFD+f: CONNECTED
```


Client running on the server itself:


```
(10:06:10) ± [user@nebero] ~/.../natpunch-go/server (master ?:3 ✗) 
→ sudo ../client/client wg0 10.66.66.1:1234 BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
[sudo] password for user: 
Resolving 2 peers
(0/2) g2kX+NzXd8f3b/jg: 10.66.66.2:56460
(1/2) rdMXY8OzXn/8P4KF: 10.66.66.3:51126
Resolved 2 peers
```

Client 1:


```
┌─[root][alpine1][~/natpunch-go/client]
└─▪ ./client wg0 10.66.66.1:1234 BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
Resolving 1 peers
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: 10.66.66.1:54600
Resolved 1 peer

```


client 2:


```
[root@alpine2 client]# ./client wg0 10.66.66.1:1234 BZ4de/xfnpwDAemiZ6SxVHINjm/dpR5qTFJkFSadUUw=
Resolving 1 peers
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: not found
(0/1) pJrGu8GakllEFD+f: 10.66.66.1:54600
Resolved 1 peer

```

### Nmap results after above:

From client 1:


```
...
...
(0/1) pJrGu8GakllEFD+f: 10.66.66.1:54600
Resolved 1 peer

┌─[root][alpine1][~/natpunch-go/client]
└─▪ nmap -sU -p 51126 10.66.66.3
Starting Nmap 7.95 ( https://nmap.org ) at 2024-08-20 10:09 IST
Nmap scan report for 10.66.66.3
Host is up (0.0011s latency).

PORT      STATE         SERVICE
51126/udp open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 0.55 seconds

```

From client 2:


```
[root@alpine2 client]# nmap -sU -p 56460 10.66.66.2
Starting Nmap 7.95 ( https://nmap.org ) at 2024-08-20 10:10 IST
Nmap scan report for 10.66.66.2
Host is up (0.0012s latency).

PORT      STATE         SERVICE
56460/udp open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 0.67 seconds
[root@alpine2 client]# 

```


The above nmap logs tells us that both of the clients are able to see each other's open UDP ports, however they seem filtered.
