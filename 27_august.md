Tuesday 27 August 2024

# Getting the server name from the TCP ClientHello packets

We need to get the servername from the packet, because we need this information for logging:

- source IP
- hostname of target
- bytes sent
- bytes recieved

To get this information, we need to process the packet first.

The formatting was inferred from wireshark. Once we got all the bits we compared them to the bits in wireshark, and bit by bit we parsed it.

It was a laborous task so we took some help from our robot friends, anyhow this is what the hex bytes mean:


![client_hello_server_name.png](client_hello_server_name.png)



# Connecting to database


Next we created a constant connection to our postgres database, so we don't have delays while opening and closing the connection.
This allows us to update the database realtime as the data comes, and it frees up the memory quicker.


