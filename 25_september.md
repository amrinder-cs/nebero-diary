Wed Sep 25 2024


# The problem with spam mails and false positives in Postfix

Postfix is a mailserver used to send and recieve emails.

However due to professional use of email technology, its prone to spams. Many services exist to counter it, and they provide extensive lists of known spammers.

However false positives do exist, and it is not possible to just ask the service to un-blacklist an email, that is the mailserver admin's responsibility.

One way it can be done is by manually adding entries into a file and generating a hash list, which tells whether to reject or accept a domain, howeve that is not feasible if we are a provider to a lot of different organizations.


# Introducing email whitelists

Luckily in postfix, there exists a way to whitelist domains.

The theoretical part of the process is provided [Here](https://www.zytrax.com/books/dns/apd/rfc5782.txt)

The practical however depends on the mailservers. For postfix, there exists `permit_dnswl_client`


in the `/etc/postfix/main.cf`, we have an option to add restrictions to ELHO.

# What is ELHO?

ELHO stands for "Extended Low Header Options." It's a term used in email protocols to refer to additional header fields that provide more information about the message, often related to tracking and delivery status.

tl;dr its used for id'ing etc.

# How to configure whitelists


## Postfix basic config
We set the `smtpd_helo_restrictions`, or whatever restriction we may desire to required. It is done via:

`smtpd_helo_required=yes` line in the main.cf

For setting the domain name, we have to set `permit_dnswl_client` to our DNS server. Where to add that varies, but in my case for testing we added it in the front.

smtpd_helo_restrictions = permit_dnswl_client my.dnswl.domain, permit_mynetworks, check_helo_access regexp:/etc/postfix/helo_access, permit_sasl_authenticated, reject_......

Now imagine we are recieving an email from domain: example.com, and example.com has an ip `10.1.1.69`

Postfix would do a reverse of that IP (which it got from A record of example.com) and then lookup `reverse_ip.my.dnswl.domain`,

Here my.dnswl.domain is our DNS server, which we control. It must be added in server's /etc/resolv.conf at the top.


## Whitelisting in our DNS

To whitelist a domain, we first resolve its IP, reverse it and then add any, ANY A record to that entry.

Example:

- the IP is `10.1.1.69`
- we reverse it, so it becomes `69.1.1.10`
- we add an A record for 69.1.1.10.my.dnswl.domain and point it to anything.

Mere existance of an A record for 69.1.1.10.my.dnswl.domain tells postfix that its whitelisted.


# Debugging

to enable debug mode we add a -v flag at the end of `/etc/postfix/master.cf`'s this line:

`smtp      inet  n       -       y       -       -       smtpd`


we just change:

`smtp      inet  n       -       y       -       -       smtpd`

TO

`smtp      inet  n       -       y       -       -       smtpd	-v`

and debug mode is on.


# Sources

[DNSBL (DNS Black List)](https://www.zytrax.com/books/dns/ch9/dnsbl.html)

[DNS Resource Records (RRs)](https://www.zytrax.com/books/dns/ch8/#zone)

[DNS Blacklists and Whitelists](https://www.zytrax.com/books/dns/apd/rfc5782.txt)

[DNS BL](https://www.dnswl.org/?page_id=15#postfix)

[Plesk forums](https://talk.plesk.com/threads/spam-whitelist-before-dnsbl-service-to-allow-override-temporarily-blocked-domains-e-g-from-freemailers.367922/post-920080)

[Serverfault thread](https://serverfault.com/questions/1126422/in-postfix-how-do-i-block-all-clients-whose-reverse-dns-is-in-a-domain)

[Debug mode](https://support.plesk.com/hc/en-us/articles/12377559907095-How-to-enable-or-disable-Postfix-debug-mode)




# Fin End
