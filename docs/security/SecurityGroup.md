
## TL;DR
- essentially is a **L7** firewall.
	- **Stateful**, if traffic is allowed out its allowed back in
- Locked down to a region /VPC combination.
- One **SG** can be attached to **multiple** **instances**. 
- All **inbound** is **blocked** by **default**.
- All **outbound** **allowed** is **authorized** by **default**.
- **SG** can reference another **SG** in **Inbound** or **outbound** rules.
- Authorized IP ranges.

### Troubleshooting
- **timeout** → **SG** **issue**.
- Connection refused → application or server error.

### Best practice
- use separate SG for SSH access.


## Classic ports to know
- 22 = SSH (Secure shell)
- 21 = FTP (File transfer protocol) to **upload** files into a file share
- 22 = SFTP (Secure file transfer protocol)- upload files using SSH.
- 80 = HTTP – access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a windows instance