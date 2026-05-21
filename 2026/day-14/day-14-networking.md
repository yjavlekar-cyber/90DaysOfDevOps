# Networking For Devops
 ## OSI model
  ###  7.Application-Interaction between application and human.(HTTP/HTTPS/DNS)
  ### 6.Presentation- Decrypts encripted data so that human can understand.
  ### 5.session- This layer handles start,stop and end of the session.
  ### 4.Transport- This layer transports data using TCP snd UDP.(TCP and UDP)
  ### 3.Network: This layer handles the routing through IP addresses.(IP)
  ### 2.Data link- In this layer data moves from devices to devices in local network.
  ### 1.Physical- Physical layer is basically the start point transferring data through physicall cable network.

## TCP/IP Model-
  In this model we have only 4 layers instead of 7 and this is model is practically applied.
    
   ### 4.Application layer-
     7.Application
     6.Presentation
     5.session
   ### 3.Transport- 
     4.Transport 
   
   ### 2.Internet -Network
   ### 1.Network Interface- 2.Data link
      1.Physical



## Protocols and thier respective layer.
    1.HTTP / HTTPS and DNS - Layer 7 Application layer.
    
    2.TCP and UDP - Layer Layer 4 Transport layer.
    
    3.IP- This layer operates on Layer 3 Network layer.

## Commands and their uses:
    I)Identity commands:
      1.hostname -I - If we want to view our Ip address.
      2.ip addr show- with ip address it shows other details as well such as mac address,state up or down etc.
      
    II)Reachibility:
      1.ping- This checks if the server is running or not.
      
    III)Path
      1.traceroute trainwithshubham.com - This commands basically traces the routes and shows the route of the packtes travelled to us on shell.
    
    IV)Ports
      1.sudo netstat -tulpn- gives us the process and on which ports they are listening.
    
    V)Name Resolution:
      1.dig <domain>- This used to findout IP's of DNS.
    
    VI)HTTP Check:
      1.curl -I www.trainwithshubham.com- Gives us Http status code for this website is-HTTP/1.1 301 Moved Permanently
      
    VII)Connections snapshot:
      1.netstat -an- Gives us connected and listening connections.


## Which command gives you the fastest signal when something is broken?
==> ping

## What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?
==> Application layer.

## Two follow-up checks you’d run in a real incident.
==> ping-will check the server is running or not.
    curl -I www.trainwithshubham.co will check the http code.
