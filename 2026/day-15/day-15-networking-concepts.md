# Task 1: DNS – How Names Become IPs
    1.DNS lookup- The browser first checks is own caches to look up the google IP address if not found it sends request to the DNS Server for IP address of google.com
    2.TCP/IP handshake- In TCP IP handshake is three way handshake happend between client and server.
      1.SYN- Browser sends packets to google server in order to establish connection with the server which is synchronization.
      2.SYN-ACK- Browser then ACK(acknowledges) the request and sends SYN (synchronize) request to client.
      3.SYN- Then browser sends the final synchronization.  
    3.SSL/TLS Negotiation- Uses TLS handshake to establish encrypted connection.
    4.HTTP Request & Response- then browser sends GET request for data and google server fulfills the request.
    5.Browser Rendering- Then browser processes the final page which is shown to us with the data provided by google server.
  
# What are the record types?
      The record types are basically extensions we use after dig google.com <ext> and it shows the category of the  information is mapped to that domain:
      1.A- IPv4 address
      2.AAAA-IPv6 address
      3.MX- Mail exchange
      4.NS- Name server
      5.CNAME- canonical name
      6.TXT- Text
      7.SOA- start of authority'
      8.ANY- Requests all available records for a domain
      9.AXFR (Zone Transfer)- Requests a full zone transfer, listing all records.
    
## Command:
  * dig www.google.com A- gives us IPv4 which is 142.250.205.206 and TTL (time to live) is 58 sec till 58 sec the browser can keep the IP cache.

# Task 2: IP Addressing
    1.What is an IPv4 address? How is it structured?
    ==> IPv4 is Internet Protocol version 4 which uses 32 bit structure.
        It is sperated by dots.
        It is a 32 bit structure divided by 8-bit decimal numbers which are also called us ocatets ranging from 0-255.
    2.Difference between public and private IPs
    ==> *Public- A public IP is an IP address available publically or an IP which is available publically.
        *Private- A private IP is and which is used in local network.
  
    3.What are the private IP ranges?
    ==> 1.Class A- 10.0.0.0 - 10.255.255.255
        2.Class B- 172.16.0.0 - 172.31.255.255
        3.Class C- 192.168.0.0 - 192.168.255.255
  # Task 3: CIDR & Subnetting
      1.What does /24 mean in 192.168.1.0/24?
      --> It represents number of bits used for the network.
    
      2.How many usable hosts in a /24? A /16? A /28?
      ==> we can calculate usable host by doing below calculations-
          i.Identify the CIDR notation in this case lets take /24.
          ii.Subtract that from 32bit.
          --32-24=8 i.e h=8
          iii.then apply below formula-
            2raise h-2 which is 254.
       3.Explain in your own words: why do we subnet?
       ==> Subnetting is basically dividing the large network into smaller parts.
    
      4.Excercise-
      CIDR- /24
      Subnet mask- 255.255.255.0
      Total IP- 256
      Usable Hosts- 254
    
      CIDR- /16
      Subnet mask- 255.255.255.0
      Total IP- 65,536
      Usable Hosts- 65,532

# Task 4: Ports – The Doors to Services
    1.What is a port? Why do we need them?
    -Ports are basically doorways which we can open and allow service to enter into our network.
    Port	Service
        22- SSH
        80- HTTP
        443-HTTPS
        53- DNS
        3306- Mysql data base port
        6379- Redis
        27017	Mongo DB
  
    2.Run ss -tulpn — match at least 2 listening ports to their services
    80-Nginx
    8080-Java

# Task 5: Putting It Together
    1. Your app can't reach a database at 10.0.1.50:3306 — what would you check first?
       ==> I will check Inbound rules whether the port 3306 is open or not.
