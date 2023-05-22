
## TL;DR
- essentially is a L7 firewall.
	- stateful, if traffic is allowed out its allowed back in
- locked down to a region /VPC combination.
- one **sg** can be attached to **multiple** **instances**. 
- all **inbound** is **blocked** by **default** 
- all **outbound** **allowed** is **authorised** by **default**.
- **sgs** can reference another **sgs** in **Inbound** or **outbound** rules
- autherized ip ranges

### Troubleshooting
- **timeout** => **sg** **issue**.
- connection refused => application or server error.

### Best practice
- use seperate sg for ssh access.


## Classic ports to know
- 22 = SSH (Secure shell)
- 21 = FTP (File transfer protocol) upload files into a file share
- 22 = SFTP (Secure file transfer protocol)- upload files using ssh
- 80 = HTTP - acess unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a windows instance