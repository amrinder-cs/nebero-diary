Wednesday 21 August 2024

# Looking for alternatives to natpunch, since it needed to go

The self hosted solution explored earlier was not user friendly to use at all. It was just a simple proof of concept script, which meant even if it worked (which it didn't), we would have to build an entire application for it, which is not viable and requires a lot of unnecessary organization resources.

I looked for alternatives but it wasn't easy to search them. I looked at the issues tab of natpunch-go [Success Report](https://github.com/malcolmseyd/natpunch-go/issues/12) and found someone who was successful in setting it up. Other than that the original maintainer of the code has been long inactive. I reached out to [Taras Glek](https://taras.glek.net/) via discord and he suggested me to use netbird instead.


# Introducing Netbird

Netbird is an open source wireguard peer to peer based VPN provider. That means everything you do on your machines, stay on your machines. It uses a modified version of WebRTC to communicate between two hosts, however if it isn't possible, it has a fallback to [TURN](https://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT) protocol.

Having read about TURN previously, this is exactly what we were looking for, so i went to test it.

# Issues while using netbird cloud.

So i went to test the netbird cloud, however their [servers](https://app.netbird.io) seemed to be down at that moment (though now it seems to be working agian)

So i did what an average network enthusiast would do, run it on my own homelab server (my old crappy - but trusty laptop i use as a server)

# Installation and setup of netbird server

I followed this guide for installation of netbird server: [Click me](https://docs.netbird.io/selfhosted/selfhosted-quickstart)

I already had all the requirements satisfied, however for future sake it requires:

- Docker
- jq
- curl
- A publiclly accessible domain
- Ability to open ports in your firewall/router.
- The machine should be publicly accessible on TCP ports 80, 443, 33073 and 10000; and UDP ports: 3478, 49152-65535.

To download and run the script we use this simple command:
```
export NETBIRD_DOMAIN=netbird.example.com; curl -fsSL https://github.com/netbirdio/netbird/releases/latest/download/getting-started-with-zitadel.sh | bash
```

If you wish to add your own users, you have to do it at {your domain}/ui/console.

Netbird uses [Zitadel](https://zitadel.com/), yet another free and open source identity provider for simple logins.


And that was it, i logged into the dashboard with the password provided to me by the install script and volia! we were up and running.

I installed the client on my debian machine, and also two of my android servers. It worked!!

Just for testing purposes, i started my apache2 server on my debian machine and tried acessing it on my laptop, it again worked

![It works Frodo Baggins](https://media.makeameme.org/created/it-works-it-5bff9f.jpg)
