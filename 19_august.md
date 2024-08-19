Monday 19 August 2024 05:53:28 PM IST
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

