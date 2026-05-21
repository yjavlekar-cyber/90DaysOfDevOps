# Linux Troubleshooting Runbook (Nginx)
## Envoirnment info
  ### uname -a
    => gives output that OS is linux host name then kernal version number etc details.
    
  ### cat /etc/os-
    release has give me version specific details of the OS.

## CPU
 ### top-
     mostly there is no cpu usage 99.9% cpu is idle

## Memory
 ### free -h
    give the memory details in humansize readable format as per the finding from 3.7gb total 3.2g is still available 
    As per CPU and Memory there shall not be any issue to run nginx.

## Disk_usage
 ### df -h 
      -> as per this disk space is merely used only 2%.

## Networking

 ### ss tuln 
    - Tcp port 80 is listening hence conclusion nginx service is active.
    
 ### curl -i http://localhost
     -Thia confirms by giving below mentioned output that nginx is working fine.
    
    HTTP/1.1 200 OK
    Server: nginx/1.24.0 (Ubuntu)
    Date: Sat, 25 Apr 2026 15:09:09 GMT
    Content-Type: text/html
    Content-Length: 615
    Last-Modified: Mon, 20 Apr 2026 17:44:04 GMT
    Connection: keep-alive
    ETag: "69e665e4-267"
    Accept-Ranges: bytes

## Logs
   ### journalctl -u nginx|head-10 
        output - Apr 25 13:46:51 Profound systemd[1]: Stopping nginx.service - A high performance web server and a reverse proxy server...
        Apr 25 13:46:51 Profound systemd[1]: nginx.service: Deactivated successfully.
        Apr 25 13:46:51 Profound systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy server.
        -- Boot c1ee6a5f965643159804aad491ca896b --
        Apr 25 13:46:52 Profound systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
        Apr 25 13:50:00 Profound systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
        Apr 25 14:36:41 Profound systemd[1]: Stopping nginx.service - A high performance web server and a reverse proxy server...
        Apr 25 14:36:41 Profound systemd[1]: nginx.service: Deactivated successfully.
        Apr 25 14:36:41 Profound systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy server.
        Apr 25 15:05:23 Profound systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
        
        Above logs for nginx shows when the service was deactivate and started again.
        


