Saturday 24 August 2024

# Routing a physical firewall traffic through wireguard mesh network

So today i was provided with a physical device, a firewall. Having done work on a firewall before, I had an idea on how to connect to it and work on it.

The [The Peer to Peer VPN](https://amrinder-cs.github.io/nebero-diary/21_august) which we setup before, i needed to route the firewall through it. Luckily netbird provides an easy way to do so, however before that, i needed to connect my firewall to my node (my laptop in this case), for that we would need to setup a subnet (which would match the firewall's subnet).



# Connecting the firewall via serial cable

Firt i simply connected the firewall to the PC via the USB to tty cable. It would show up as a device in /dev/
Since its a USB to tty, it would show up as ttyUSB(something), to check which one it was i did:

```bash
ls /dev/ | grep USB
```

Output:

```bash
┌─[root][THISPC][~]
└─▪  ls /dev/ | grep USB
ttyUSB0
```

Secondly i needed to connect to it, one way to connect to the serial interface is the screen command. 

```bash
sudo apt install screen

# and then

sudo screen /dev/ttyUSB0 9600
```

9600 was the baud rate.

It connected successfully, so i logged into it by the password provided. However for some reason i had to close that window, which i did. By doing that i did not realize that the screen was still runnning in the background. 

I connected through another screen session and it did not show me some characters, it was skipping some. Upon opening a file it totally broke the output. I assumed the encoding might be wrong but that would be wrong, since if encoding was wrong i would not be able to see any output. 

Turns out, the issue was, multiple running screens in the backgrounds. Some of them were consuming the bits coming to the terminal, which caused it to be distorted.

to test that out:

```bash
sudo screen -ls
```

and i saw a lot of screens.. So i just killed all of them and reconnected, which solved the problem.


Now, i was told to not touch any configuration on the firewall, i only had to know the subnet from it, therefore i did ip a and saw the subnet.

Let's assume the subnet was 10.1.1.0/24, i would replicate it on my laptop and give an IP in that subnet's range by static routing.

so i edited `/etc/network/interfaces` using nano btw, and added the following:


```
auto enp2s0
iface enp2s0 inet static
	address 10.1.1.1
	netmask 255.255.255.0

```

I tried pinging this IP from the firewall through tty, it didn't work. Turns out i was setting the wrong range and reading from the wrong interface, we can see which interface it is by looking at "status UP" in the output:


```
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
```

Anyhow, i setup the correct interface and pinged the host, it worked. Next thing was to setup the route in netbird. It was done simply via GUI, here's how to do so:

- visit {netbird_domain}/network-routes

- Click add routes


This is how you do it:


![How to add routes in netbird](https://nebero.amrinder-singh.me/netbird_routes.png)


I tried pinging my device from another connected with the same wireguard network, it was able to ping and i was able to access services running on the firewall.




# Network Policies

Se needed to have different groups which would be allowed to connect different peers. For that we go to {netbird_domain}/access-control and disable the default policy.
then we "Add Policy"

This is how we manage it:

![Netbird Access Policies](https://nebero.amrinder-singh.me/netbird_access_policies.png)

We can add posture checks if necessary, they are self explanatory:


![Netbird Posture Checks](https://nebero.amrinder-singh.me/netbird_posture_checks.png)


❗❗❗ Remember to disable the default policy, because without it all the other policies would be useless


You can add peers to those groups via the admin console. Click peers and click on the peer you want to assign groups to. This way:



![Editing Groups Peers](https://nebero.amrinder-singh.me/edit_peer_groups.png)

Now only the peers which are assigned particular group can see the others, depending on the policy.
